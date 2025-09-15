# Hands-on Activity: HTTP Requests with curl and VS Code REST Client

This activity will help you understand how HTTP works by sending 
HTTP requests and inspecting responses.  
You will use two tools:
- **curl** (command line)
- **REST Client** extension in **Visual Studio Code**


## Introduction to curl and REST Client
### What is curl?
- **curl** is a command-line tool for making network requests.  
- It supports many protocols (HTTP, HTTPS, FTP, etc.), but we’ll use it mainly for **HTTP APIs**.  
- It’s fast, lightweight, and available on almost all systems.  
- Perfect for practicing and automating API requests directly from the terminal.

**Example:**
```bash
curl https://jsonplaceholder.typicode.com/posts/1
```
This fetches data for the post with `ID` `1` and prints it in the terminal.

### What is the REST Client (VS Code Extension)?
- A Visual Studio Code extension that lets you send HTTP requests right from your editor.
- Requests are written in plain text files (.http), making them easy to save, share, and reuse.
- Responses show up in a side panel in VS Code, with support for JSON formatting and syntax highlighting.
- Great for who prefer a GUI-like experience inside VS Code rather than the terminal.
## About JSONPlaceholder
For this lab, we will use [JSONPlaceholder](https://jsonplaceholder.typicode.com/), a **free online fake REST API** for practice.

### What is JSONPlaceholder?
- A simple API designed for **learning, testing, and prototyping**.  
- Provides fake data such as posts, comments, albums, photos, todos, and users.  
- Perfect for beginners to safely try out HTTP methods without setting up their own server.  

### How It Works:
- **GET** requests → Always return fake data.  
- **POST, PUT, DELETE** requests → Pretend to modify data but changes are not saved (sandbox mode).  
- **Responses** come in **JSON (JavaScript Object Notation)** format, the standard data format for APIs.  

### Example:
Request:
```
GET https://jsonplaceholder.typicode.com/posts/1
```

Response:
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati",
  "body": "quia et suscipit..."
}
```

Think of JSONPlaceholder as a **playground for APIs**, like a driving simulator for programmers. You can practice making requests without worrying about breaking anything.

## How Requests and Responses Work
```
+-----------+         HTTP Request          +-------------------+
|           |  ------------------------->   |                   |
|   Client  |                               |       Server      |
| (curl or  |   <-------------------------  | (JSONPlaceholder) |
| REST API) |         HTTP Response         |                   |
+-----------+                               +-------------------+

```
---


## 1. Prerequisites

### Operating System Setup

#### Ubuntu / Linux
- `curl` is usually pre-installed. If not:
  ```bash
  sudo apt update
  sudo apt install curl -y
  ```
- Inside VS Code, install the **REST Client** extension from the Extensions Marketplace.

---

#### Windows
- Install **curl**:
  - If you are using **Windows 10 or later**, `curl` is already included.
  - Check with:
    ```powershell
    curl --version
    ```
- Open VS Code → Extensions → Search for **REST Client** → Install.

---

#### macOS
- `curl` is pre-installed.
- To confirm:
  ```bash
  curl --version
  ```
- Install the **REST Client** extension in VS Code.

---

## 2. Activity 1 – Sending HTTP Requests with curl

### Step 1: Basic GET Request
```bash
curl https://jsonplaceholder.typicode.com/posts/1
```

### Step 2: Show Headers with Response
```bash
curl -i https://jsonplaceholder.typicode.com/posts/1
```

### Step 3: Send a POST Request (Create Resource)
```bash
curl -X POST https://jsonplaceholder.typicode.com/posts -H "Content-Type: application/json" -d '{"title":"My First Post","body":"Hello REST!","userId":1}'
```

### Step 4: Send a DELETE Request
```bash
curl -X DELETE https://jsonplaceholder.typicode.com/posts/1
```

---

## 3. Activity 2 – Sending HTTP Requests with VS Code REST Client

### Step 1: Setup
- Create a new file: `requests.http`.

### Step 2: Add the Following Requests
```http
### Get all posts
GET https://jsonplaceholder.typicode.com/posts

### Get a specific post
GET https://jsonplaceholder.typicode.com/posts/1

### Create a new post
POST https://jsonplaceholder.typicode.com/posts
Content-Type: application/json

{
  "title": "VS Code Test",
  "body": "Hello from REST Client!",
  "userId": 99
}

### Delete a post
DELETE https://jsonplaceholder.typicode.com/posts/1
```

### Step 3: Run Requests
- Hover over a request and click **"Send Request"**.
- The response will appear in a new VS Code panel.

---

## 4. Activity 3 – Observe Live HTTP in Browser

1. Open **Developer Tools → Network tab** in your browser.  
2. Visit [https://example.com](https://example.com).  
3. Inspect the **GET request** and note:
   - Request headers
   - Response headers
   - Status code
   - Body (HTML)

---

## 5. Reflection

- **What differences did you notice between GET, POST, and DELETE requests?**  
- **How do status codes help you understand what happened?**  
- **Which tool did you find more beginner-friendly: curl or REST Client? Why?**

---

By completing this activity, you’ve learned:
- How HTTP request/response works
- How to send requests with different methods
- How to observe status codes, headers, and bodies


---

## Sending Requests Programmatically

So far, you’ve learned how to send HTTP requests using **curl** and the **REST Client extension**.  
But in real-world projects, developers usually send requests **programmatically** from inside their code.

### Why Send Requests in Code?
- To **integrate with APIs** (e.g., weather data, payment services, social media).  
- To **automate tasks** (e.g., fetching data every hour).  
- To **connect different applications** (e.g., your app talking to a database or external service).  

---

### Example in JavaScript (using `fetch`)
```javascript
// Fetch a post from JSONPlaceholder
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error("Error:", error);
  });
```

### Example in Python (using requests)
```python
import requests

# Fetch a post from JSONPlaceholder
response = requests.get("https://jsonplaceholder.typicode.com/posts/1")

if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print("Request failed:", response.status_code)
```
These code snippets do the same thing as the `curl` or `REST Client` examples: 
- they send an HTTP `GET` request and print the response.
- But here, you can use the data in your program, not just view it.

---

## When to Use curl, REST Client, or Code?

Each tool has its own strengths. Here’s a quick guide:

| Tool            | Best For | Pros | Cons |
|-----------------|----------|------|------|
| **curl**        | Quick testing in the terminal | Fast, works everywhere, good for automation in shell scripts | Harder to read/write for complex requests |
| **REST Client** | Learning & manual testing inside VS Code | Easy to use, readable request files, nice formatted responses | Only works inside VS Code |
| **Code (Python/JS/etc.)** | Building real applications | Can reuse data in programs, automate workflows, connect APIs | Requires coding knowledge, more setup |

---

Think of it like this:  
- **curl** → Quick, command-line experiments  
- **REST Client** → Beginner-friendly exploration inside VS Code  
- **Programming** → Real apps where your code actually *uses* the data
