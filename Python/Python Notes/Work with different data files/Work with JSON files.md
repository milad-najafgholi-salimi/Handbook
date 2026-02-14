## What is JSON?

JSON (JavaScript Object Notation) is a lightweight data interchange format that's easy for humans to read and write, and easy for machines to parse and generate. It's widely used for APIs, configuration files, and data storage.

---
## Python's `json` Module

Python includes a built-in `json` module that makes working with JSON data simple. Here are the key operations:

### Basic JSON to Python Conversion
```
import json

# JSON string to Python dictionary (deserialization)
json_string = '{"name": "Milad", "age": 22, "city": "Tehran"}'
python_dict = json.loads(json_string)
print(python_dict)  # {'name': 'Milad', 'age': 22, 'city': 'Tehran'}
print(type(python_dict))  # <class 'dict'>

# Python dictionary to JSON string (serialization)
python_dict = {"name": "Faraz", "age": 22, "city": "Tehran"}
json_string = json.dumps(python_dict)
print(json_string)  # '{"name": "Faraz", "age": 22, "city": "Tehran"}'
```
### Working with JSON Files
```
import json

# Reading JSON from a file
with open('data.json', 'r') as file:
    data = json.load(file)  # Note: load() not loads()

# Writing JSON to a file
with open('output.json', 'w') as file:
    json.dump(data, file)  # Note: dump() not dumps()
```

---
## JSON to Python Type Mapping
| JSON          | Python |
| ------------- | ------ |
| object        | dict   |
| array         | list   |
| string        | str    |
| number (int)  | int    |
| number (real) | float  |
| true          | True   |
| false         | False  |
| null          | None   |

---
## Pretty Printing JSON
```
import json

data = {"name": "Milad", "age": 22, "hobbies": ["reading", "workout"]}

# Pretty print with indentation
pretty_json = json.dumps(data, indent=4)
print(pretty_json)
# Output:
# {
#     "name": "Charlie",
#     "age": 35,
#     "hobbies": [
#         "reading",
#         "workout"
#     ]
# }
```

---
## Handling Non-Serializable Objects

Sometimes you need to serialize custom objects:
```
import json
from datetime import datetime

class Person:
    def __init__(self, name, birth_date):
        self.name = name
        self.birth_date = birth_date

# Custom encoder for datetime objects
def datetime_encoder(obj):
    if isinstance(obj, datetime):
        return obj.isoformat()
    raise TypeError(f"Object of type {type(obj)} is not JSON serializable")

person = Person("Milad", datetime(2003, 3, 15))

# Using default parameter to handle datetime
json_str = json.dumps(person.__dict__, default=datetime_encoder)
print(json_str)  # '{"name": "Milad", "birth_date": "2003-03-15T00:00:00"}'
```

---
## Sorting Keys and Controlling Output
```
import json

data = {"c": 3, "a": 1, "b": 2}

# Sort keys alphabetically
sorted_json = json.dumps(data, sort_keys=True, indent=2)
print(sorted_json)
# {
#   "a": 1,
#   "b": 2,
#   "c": 3
# }

# Remove whitespace (minify)
minified = json.dumps(data, separators=(',', ':'))
print(minified)  # {"c":3,"a":1,"b":2}
```

---
## Error Handling
```
import json

invalid_json = '{"name": "Milad", age: 22}'  # Invalid: age not in quotes

try:
    data = json.loads(invalid_json)
except json.JSONDecodeError as e:
    print(f"Invalid JSON: {e}")
    print(f"Error at line {e.lineno}, column {e.colno}")
```

---
## Common Use Cases

1. **API Responses**
```
import json
import requests  # Third-party library for HTTP requests

response = requests.get('https://api.example.com/data')
data = response.json()  # Automatically parses JSON response
```
2. **Configuration Files**
```
import json

# config.json
config_data = {
    "database": {
        "host": "localhost",
        "port": 5432,
        "name": "myapp"
    },
    "debug": True
}

with open('config.json', 'w') as f:
    json.dump(config_data, f, indent=4)
```
3. **Data Exchange Between Systems**  
    JSON is perfect for sending data between different programming languages or systems.
    
---
## Tips and Best Practices

1. Use `indent` for human-readable JSON files
    
2. Use `separators=(',', ':')` for compact JSON in production
    
3. Always validate JSON before parsing
    
4. Handle encoding properly (JSON is UTF-8 by default)
    
5. Use `default` parameter for custom object serialization
    

The `json` module is simple yet powerful, making it one of the most frequently used modules in Python for data interchange!