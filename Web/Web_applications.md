## HTTP Messages

<img width="1705" height="393" alt="645b19f5d5848d004ab9c9e2-1728786920770" src="https://github.com/user-attachments/assets/a7bd2939-7885-47e6-9e5b-9d556195dda8" />

HTTP messages are packets of data exchanged between a user (the client) and the web server. These messages are very important for understanding how web applications work because they show how users' requests and the server's responses are communicated.

Imagine an example of an HTTP Request and an HTTP Response, where you can see key parts like the method, URL, headers, and status codes. These are what make the client-server interaction possible.

There are two types of HTTP messages:
- HTTP Requests: Sent by the user to trigger actions on the web application.
- HTTP Responses: Sent by the server in response to the user’s request.

**1. Start Line**
- The introduction of the message. It tells you what kind of message is being sent—whether it's a request from the user or a response from the server.
  
**2. Headers**
- Headers are made up of key-value pairs that provide extra information about the HTTP message.
  
**3. Empty Line**
- The empty line is a little divider that separates the header from the body. It’s essential because it shows where the headers stop and where the actual content of the message begins.
  
**4. Body**
- The body is where the actual data is stored.

---

## HTTP Request

An HTTP request is what a user sends to a web server to interact with a web application and make something happen. Since these requests are often the first point of contact between the user and the web server.

<img width="1140" height="600" alt="5f04259cf9bf5b57aed2c476-1730445201524" src="https://github.com/user-attachments/assets/e8037fd0-8dc0-4eff-a404-7c4d9307872a" />

> HTTP request showing the key parts like the method (e.g., GET or POST), path (e.g., /login), and version (e.g., HTTP/1.1). These elements make up the basics of how a client (user) communicates with a server.

### Request Line
The request line (or start line) is the first part of an HTTP request and tells the server what kind of request it’s dealing with. It has three main parts: the HTTP method, the URL path, and the HTTP version.
- Example: `METHOD /path HTTP/version`

### HTTP Methods

The HTTP method tells the server what action the user wants to perform on the resource identified by the URL path.
- Most common Methods:-
  - `GET` : Used to fetch data from the server without making any changes.
  - `POST` : Sends data to the server, usually to create or update something.
  - `PUT` : Replaces or updates something on the server.
  - `DELETE` : Removes something from the server.

-  Few others used in specific cases:
  - `PATCH` : PATCH is an HTTP method used to apply partial modifications to a resource on a server.
  - `HEAD` : Works like GET but only retrieves headers, not the full content. It’s handy for checking metadata without downloading the full response.
  - `OPTIONS` : Tells you what methods are available for a specific resource, helping clients understand what they can do with the server.
  - `TRACE` : Similar to OPTIONS, it shows which methods are allowed, often for debugging.
  - `CONNECT` : Used to create a secure connection, like for HTTPS. It’s not as common but is critical for encrypted communication

> PATCH requests should be validated to avoid inconsistencies, and OPTIONS and TRACE should be turned off if not needed to avoid possible security risks.

### URL Path

The URL path tells the server where to find the resource the user is asking for. For instance, in the URL `https://tryhackme.com/api/users/123`, the path `/api/users/123` identifies a specific user.

### HTTP Version

The HTTP version shows the protocol version used to communicate between the client and server.
- `HTTP/1.1` **(1997)** : Brought persistent connections, chunked transfer encoding, and better caching. It’s still widely used today. 
- `HTTP/2` **(2015)** : Introduced features like multiplexing, header compression, and prioritisation for faster performance.
- `HTTP/3` **(2022)** : Built on HTTP/2, but uses a new protocol (QUIC) for quicker and more secure connections.

> Although HTTP/2 and HTTP/3 offer better speed and security, many systems still use HTTP/1.1 because it’s well-supported and works with most existing setups. However, upgrading to HTTP/2 or HTTP/3 can provide significant performance and security improvements as more systems adopt them.

## Request Headers

Request Headers allow extra information to be conveyed to the web server about the request.

Some common headers
