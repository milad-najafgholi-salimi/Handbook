An **API**—short for **Application Programming Interface**—is a set of rules and tools that allows different software systems to **communicate with each other**.

---

## What an API Does

An API allows one program to:

- Request data from another program
    
- Send data to another program
    
- Trigger actions in another system
    

All without exposing how the internal system is built.

---

## How APIs Work (Simple Flow)

1. A client sends a **request** (usually over the internet)
    
2. The request includes:
    
    - An **endpoint** (URL)
        
    - A **method** (GET, POST, PUT, DELETE, etc.)
        
    - Optional data (JSON)
        
3. The server processes the request
    
4. The server sends back a **response**, usually in JSON format
    

Example:

`GET https://api.weather.com/v1/city/Tehran`

Response:
```
{
  "temperature": 18,
  "condition": "Cloudy"
}
```

---

## Common Types of APIs

### 1. **REST APIs** (Most common)

- Use HTTP methods (GET, POST, PUT, DELETE)
    
- Stateless
    
- Data usually in JSON
    

### 2. **SOAP APIs**

- Older, XML-based
    
- Very strict structure
    
- Often used in enterprise systems
    

### 3. **GraphQL APIs**

- Client asks for exactly the data it needs
    
- Reduces over-fetching and under-fetching
    

### 4. **WebSocket APIs**

- Real-time communication (chat apps, live updates)
    

---

## Why APIs Are Important

- Enable **integration** between systems
    
- Allow **scalability** and modular design
    
- Power **mobile apps, websites, IoT, AI tools**
    
- Make software **reusable and flexible**
    