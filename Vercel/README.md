---

## Vercel Configuration (`vercel.json`)

### **`builds` Property**

- **Purpose:** Specifies how to build specific source files.
- **Components:**
  - **`src`:** Source file for the build step (e.g., `server.js`).
  - **`use`:** Builder to use for the source file (e.g., `@vercel/node`).

```json
{
  "builds": [
    {
      "src": "server.js",
      "use": "@vercel/node"
    }
  ]
}
```

### **`routes` Property**

- **Purpose:** Defines routing rules for incoming requests.
- **Components:**
  - **`src`:** Regular expression pattern to match incoming request URLs (e.g., `/.*` to match all URLs).
  - **`dest`:** Destination file to handle the matched requests (e.g., `server.js`).

```json
{
  "routes": [
    {
      "src": "/.*",
      "dest": "server.js"
    }
  ]
}
```

### **Complete `vercel.json` Example**

Combines `builds` and `routes` properties:

```json
{
  "builds": [
    {
      "src": "server.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/.*",
      "dest": "server.js"
    }
  ]
}
```

### **How It Works**

1. **Build Step:**
   - Vercel uses `@vercel/node` builder to handle `server.js`.
   - Sets up a Node.js environment and runs `server.js`.

2. **Routing Step:**
   - Matches any URL with `/.*` and routes to `server.js`.
   - `server.js` handles the request and sends back the response.

### **Example of `server.js`**

A simple Express.js application:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.get('/api', (req, res) => {
  res.json({ message: 'Hello from the API!' });
});

const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```

### **Concepts and Topics**

- **Vercel Configuration:** `vercel.json` configures how Vercel builds and serves your application.
- **Builds:** Defines how Vercel should build your application.
- **Routes:** Defines how incoming requests are routed to your application's handlers.
- **Node.js Builder:** `@vercel/node` allows deploying Node.js applications on Vercel.
- **Express.js:** A web framework for Node.js used to handle HTTP requests and define routes in `server.js`.
- **Environment Variables:** `process.env.PORT` retrieves the port number from environment variables, useful for configuring the port in different environments.

---