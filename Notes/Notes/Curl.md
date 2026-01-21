The **`curl` command** is a powerful **command-line tool** used to **send and receive data from servers** using URLs. It’s most commonly used to **test APIs**, download data, or automate web requests.

---
## What `curl` Does

`curl` can:

- Send HTTP/HTTPS requests
    
- Fetch data from APIs
    
- Upload files
    
- Download files
    
- Test endpoints without a browser
    
- Work with many protocols (HTTP, HTTPS, FTP, SFTP, etc.)
    

It’s widely used by developers, system admins, and DevOps engineers.

---

## Basic Syntax

`curl [options] URL`

Example:

`curl https://example.com`

This sends a **GET request** and prints the response to the terminal.

---

## Common `curl` Use Cases

### GET Request (Fetch Data)

`curl https://api.example.com/users`

This retrieves data from the server.

---

### POST Request (Send Data)
```
curl -X POST https://api.example.com/users \
     -H "Content-Type: application/json" \
     -d '{"name":"John","age":25}'
```

- `-X POST` → HTTP method
    
- `-H` → header
    
- `-d` → data payload
    

---

### Send Authorization Token
```
curl -H "Authorization: Bearer YOUR_TOKEN" https://api.example.com/profile
```

Used for authenticated APIs.

---

### Download a File

`curl -O https://example.com/file.zip`

Or save with a custom name:

`curl -o myfile.zip https://example.com/file.zip`

---

### See Full Request & Response (Debugging)

`curl -v https://example.com`

Very useful for debugging API issues.

---

### Send Form Data
```
curl -X POST -F "file=@image.jpg" https://example.com/upload
```

---

## Commonly Used Options

|Option|Meaning|
|---|---|
|`-X`|Specify HTTP method|
|`-H`|Add request header|
|`-d`|Send data|
|`-o`|Save output to file|
|`-O`|Save with original filename|
|`-v`|Verbose output|
|`-I`|Fetch headers only|

---

## Why Developers Use `curl`

- Lightweight and fast
    
- Works on almost every OS
    
- Great for testing APIs
    
- Scriptable (used in automation & CI/CD)
    
- No GUI required