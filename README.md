# Hands-on Activity: HTTP Requests with curl and VS Code REST Client

This activity will help you understand how HTTP works by sending 
HTTP requests and inspecting responses.  
You will use two tools:
- **curl** (command line)
- **REST Client** extension in **Visual Studio Code**

---
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
