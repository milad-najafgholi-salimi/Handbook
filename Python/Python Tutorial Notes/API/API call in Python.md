An API call in Python is a request made to an external service or server to retrieve or send data.

---
## What is an API Call?

API (Application Programming Interface) calls allow your Python program to communicate with other software applications, services, or databases over the internet. It's like ordering food at a restaurant - you (your program) make a request, and the kitchen (the API server) returns what you asked for.

---
## **Making API Calls in Python**

### 1. Using the `requests` Library (Most Common)

The `requests` library is the go-to choice for API calls in Python:
```
import requests

# Basic GET request
response = requests.get('https://api.github.com/users/octocat')

# Check if request was successful
if response.status_code == 200:
    data = response.json()  # Parse JSON response
    print(data)
else:
    print(f"Error: {response.status_code}")
```
### 2. Common HTTP Methods
```
import requests

# GET - Retrieve data
response = requests.get('https://api.example.com/users')

# POST - Create new data
new_user = {'name': 'John', 'email': 'john@example.com'}
response = requests.post('https://api.example.com/users', json=new_user)

# PUT - Update existing data
updated_user = {'name': 'John Updated'}
response = requests.put('https://api.example.com/users/1', json=updated_user)

# DELETE - Remove data
response = requests.delete('https://api.example.com/users/1')

# PATCH - Partial update
response = requests.patch('https://api.example.com/users/1', json={'email': 'new@email.com'})
```
### 3. Adding Headers and Authentication
```
import requests

# Headers
headers = {
    'User-Agent': 'MyApp/1.0',
    'Accept': 'application/json'
}

# API Key authentication
headers['Authorization'] = 'Bearer YOUR_API_KEY'

# Or using auth parameter
response = requests.get(
    'https://api.example.com/data',
    headers=headers,
    auth=('username', 'password')  # Basic auth
)

# Query parameters
params = {
    'q': 'python',
    'page': 1,
    'per_page': 10
}
response = requests.get('https://api.github.com/search/repositories', params=params)
```
### 4. Error Handling
```
import requests
from requests.exceptions import RequestException

try:
    response = requests.get('https://api.example.com/data', timeout=5)
    response.raise_for_status()  # Raises exception for 4XX/5XX status codes
    data = response.json()
    
except requests.exceptions.Timeout:
    print("The request timed out")
except requests.exceptions.ConnectionError:
    print("Failed to connect to the API")
except requests.exceptions.HTTPError as err:
    print(f"HTTP error occurred: {err}")
except RequestException as e:
    print(f"An error occurred: {e}")
except ValueError as e:  # JSON decoding error
    print(f"Failed to parse JSON: {e}")
```
### 5. Working with Different Response Formats
```
import requests

response = requests.get('https://api.example.com/data')

# Get response as text
text_content = response.text

# Parse JSON (most common)
json_data = response.json()

# Get raw content (for images, files, etc.)
raw_content = response.content

# Response headers
headers = response.headers
content_type = response.headers.get('content-type')

# Response metadata
status_code = response.status_code
url = response.url
encoding = response.encoding
```

---
## Real-World Example

Here's a practical example using the OpenWeatherMap API:
```
import requests
import os
from dotenv import load_dotenv

load_dotenv()  # Load environment variables

def get_weather(city):
    api_key = os.getenv('OPENWEATHER_API_KEY')
    base_url = "http://api.openweathermap.org/data/2.5/weather"
    
    params = {
        'q': city,
        'appid': api_key,
        'units': 'metric'  # For Celsius
    }
    
    try:
        response = requests.get(base_url, params=params, timeout=10)
        response.raise_for_status()
        
        weather_data = response.json()
        
        # Extract relevant information
        temperature = weather_data['main']['temp']
        description = weather_data['weather'][0]['description']
        humidity = weather_data['main']['humidity']
        
        return {
            'city': city,
            'temperature': temperature,
            'description': description,
            'humidity': humidity
        }
        
    except requests.exceptions.RequestException as e:
        print(f"Error fetching weather data: {e}")
        return None
    except KeyError as e:
        print(f"Unexpected response format: {e}")
        return None

# Usage
weather = get_weather("London")
if weather:
    print(f"Weather in {weather['city']}:")
    print(f"Temperature: {weather['temperature']}°C")
    print(f"Conditions: {weather['description']}")
    print(f"Humidity: {weather['humidity']}%")
```

---
## Best Practices

1. **Always handle exceptions** - Network calls can fail
    
2. **Set timeouts** - Prevent hanging requests
    
3. **Use environment variables** for API keys
    
4. **Respect rate limits** - Check API documentation
    
5. **Cache responses** when appropriate
    
6. **Log requests** for debugging
    
7. **Use session objects** for multiple requests:
