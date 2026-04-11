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

### Request Headers

Request Headers allow extra information to be conveyed to the web server about the request.

**Common Request Headers**

- HOST : `Host: tryhackme.com`
- USER-AGENT : `Mozilla/5.0`
- Referer : `https://www.google.com/`
- Cookie: `user_type=student; room=introtowebapplication; room_status=in_progress`
- Content-Type: `application/json`

### Request Body
In HTTP requests such as POST and PUT, where data is sent to the web server as opposed to requested from the web server, the data is located inside the HTTP Request Body. The formatting of the data can take many forms, but some common ones are `URL Encoded`, `Form Data`, `JSON`, or `XML`.

- **URL Encoded (application/x-www-form-urlencoded)**
    - A format where data is structured in pairs of key and value where (key=value). Multiple pairs are separated by an (&) symbol, such as `key1=value1&key2=value2`. Special characters are percent-encoded.
```bash
      POST /profile HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 33

name=Aleksandra&age=27&country=U
```

- **Form Data (multipart/form-data)**
  - Allows multiple data blocks to be sent where each block is separated by a boundary string. The boundary string is the defined header of the request itself. This type of formatting can be used to send binary data, such as when uploading files or images to a web server.

```shell
POST /upload HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="username"

aleksandra
----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
Content-Type: image/jpeg

[Binary Data Here representing the image]
----WebKitFormBoundary7MA4YWxkTrZu0gW--
```

- **JSON (application/json)**
  - In this format, the data can be sent using the JSON (JavaScript Object Notation) structure. Data is formatted in pairs of name : value. Multiple pairs are separated by commas, all contained within curly braces { }.
 
```json
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/json
Content-Length: 62

{
    "name": "Aleksandra",
    "age": 27,
    "country": "US"
}
```
- **XML (application/xml)**
  - In XML formatting, data is structured inside labels called tags, which have an opening and closing. These labels can be nested within each other.

```xml
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/xml
Content-Length: 124

<user>
    <name>Aleksandra</name>
    <age>27</age>
    <country>US</country>
</user>
```

## HTTP Response

When you interact with a web application, the server sends back an HTTP response to let you know whether your request was successful or something went wrong.

The first line in every HTTP response is called the Status Line. It gives you three key pieces of info:
1. **HTTP Version**: This tells you which version of HTTP is being used.
2. **Status Code**: A three-digit number showing the outcome of your request.
3. **Reason Phrase**: A short message explaining the status code in human-readable terms.

### Status Codes and Reason Phrases
The Status Code is the number that tells you if the request succeeded or failed, while the Reason Phrase explains what happened.
- These codes fall into five main categories:
  1. **Informational Responses (100-199)**
      - These codes mean the server has received part of the request and is waiting for the rest. It’s a "keep going" signal.

  2. **Successful Responses (200-299)**
      - These codes mean everything worked as expected. The server processed the request and sent back the requested data.

  3. **Redirection Messages (300-399)**
      - These codes tell you that the resource you requested has moved to a different location, usually providing the new URL.

  4. **Client Error Responses (400-499)**
      - These codes indicate a problem with the request. Maybe the URL is wrong, or you’re missing some required info, like authentication.

  5. **Server Error Responses (500-599)**
      - These codes mean the server encountered an error while trying to fulfil the request. These are usually server-side issues and not the client’s fault.

> [More about Status code](https://github.com/dolo65o/cybersecurity-foundations/blob/f74f43aba5d72ac8c2695a6155491080e638b134/Web/HTTP-in-detail.md)

### Response Headers

<img width="1236" height="742" alt="Response headers" src="https://github.com/user-attachments/assets/05e88a30-f243-40d0-ac59-1926468c696b" />

When a web server responds to an HTTP request, it includes HTTP response headers, which are basically key-value pairs.

**Required Response Headers**

Some response headers are crucial for making sure the HTTP response works properly.

Example:- 
- `DATE` :- `Fri, 23 Aug 2024 10:43:21 GMT`
    - the exact date and time when the response was generated by the server.
- `Content-Type` :- `text/html; charset=utf-8`
    - what kind of content it’s getting, like whether it’s HTML, JSON, or something else.
- `Server` :- `nginx`
    - what kind of server software is handling the request.
 
**Other Common Response Headers**

Besides the essential ones, there are other common headers that give additional instructions to the client or browser and help control how the response should be handled.

Example:-
- `Set-Cookie: sessionId=38af1337es7a8`
    - This one sends cookies from the server to the client, which the client then stores and sends back with future requests. To keep things secure, make sure cookies are set with the `HttpOnly` flag (so they can’t be accessed by JavaScript) and the `Secure` flag (so they’re only sent over HTTPS).
- `Cache-Control: max-age=600`
    - This header tells the client how long it can cache the response before checking with the server again. It can also prevent sensitive info from being cached if needed (using `no-cache`).
- `Location: /index.html`
    - This one’s used in redirection (3xx) responses. It tells the client where to go next if the resource has moved.
 
---

## Web Security — HTTP Security Headers

### Overview

HTTP Security Headers improve the overall security of web
applications by providing mitigations against attacks like:
- Cross-Site Scripting (XSS)
- Clickjacking
- Protocol downgrade attacks
- Information leakage

> Use **https://securityheaders.io/** to analyse the
> security headers of any website

---

### Content-Security-Policy (CSP)

#### What it does
An additional security layer that helps mitigate against
**Cross-Site Scripting (XSS)** attacks.

> Malicious code could be hosted on a separate website
> and injected into a vulnerable website. CSP lets
> administrators define exactly which domains/sources
> are considered safe.

#### Example CSP Header
```
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'
```

#### CSP Directives Breakdown

| Directive | Value | Meaning |
|-----------|-------|---------|
| `default-src` | `'self'` | Only load content from the same domain |
| `script-src` | `'self' https://cdn.tryhackme.com` | Scripts allowed from self + CDN |
| `style-src` | `'self'` | CSS stylesheets only from same domain |



### Strict-Transport-Security (HSTS)

#### What it does
Ensures web browsers **always connect over HTTPS** —
never plain HTTP.

#### Example HSTS Header
```
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```

#### Directives Explained

**`max-age`**
- Expiry time in **seconds** for this setting
- `63072000` = 2 years
- Browser remembers to use HTTPS for this duration

**`includeSubDomains`** *(optional)*
- Applies HSTS to **all subdomains** of the site
- e.g. `sub.example.com` also gets forced HTTPS

**`preload`** *(optional)*
- Allows website to be included in browser **preload lists**
- Browsers enforce HTTPS even **before** first visit
- Must be submitted to: https://hstspreload.org

---

### X-Content-Type-Options

#### What it does
Instructs browsers **not to guess** the MIME type of a
resource — only use the declared `Content-Type` header.

#### Example Header
```
X-Content-Type-Options: nosniff
```

#### Directive Breakdown

| Directive | Meaning |
|-----------|---------|
| `nosniff` | Browser must NOT sniff or guess the MIME type |

### Why it matters
Without this header, browsers try to "sniff" what type
of file they received. Attackers can exploit this by
uploading a malicious file disguised as an image — the
browser might execute it as JavaScript.

> `nosniff` = "Trust only what the server says this file is"

---

### Referrer-Policy

### What it does
Controls **how much information** is sent to the destination
server when a user clicks a link and gets redirected.

> Controls what goes in the HTTP `Referer` header
> (tells the destination where the user came from)

#### Example Headers

```
Referrer-Policy: no-referrer
Referrer-Policy: same-origin
Referrer-Policy: strict-origin
Referrer-Policy: strict-origin-when-cross-origin
```

#### Directives Explained

**`no-referrer`**
- Completely disables referrer information
- Most private option — destination never knows where you came from

**`same-origin`**
- Sends referrer info only when staying on the **same website**
- Useful for internal analytics without leaking to external sites

**`strict-origin`**
- Only sends the **origin** (not full URL) as referrer
- Only when protocol stays same: HTTPS → HTTPS 
- NOT sent when: HTTPS → HTTP 

**`strict-origin-when-cross-origin`**
- For **same-origin** requests → sends full URL path
- For **cross-origin** requests → sends only the origin
- Most balanced option between privacy and functionality
