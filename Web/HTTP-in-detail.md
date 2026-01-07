# HTTP (HyperText Transfer Protocol)

Hypertext Transfer Protocol (HTTP) is the protocol that specifies how a web browser and a web server communicate.HTTP is the set of rules used for communicating with web servers for the transmitting of webpage data, whether that is HTML, Images, Videos, etc.

#### What is HTTPS? (HyperText Transfer Protocol Secure)
HTTPS is the secure version of HTTP. HTTPS data is encrypted so it not only stops people from seeing the data you are receiving and sending, but it also gives you assurances that you're talking to the correct web server and not something impersonating it.

## What is a URL? (Uniform Resource Locator)

A URL is a full instruction on how to access a specific resource on the web — from which server, on which port, using which protocol, with optional login and extra info.

<img width="1140" height="270" alt="url features" src="https://github.com/user-attachments/assets/59182bad-a439-4af5-91fd-f237c800bfce" />

- Scheme: What protocol to use for accessing the resource such as HTTP, HTTPS, FTP (File Transfer Protocol).
- User: Some services require authentication to log in.
- Host: The domain name or IP address of the server you wish to access.
- Port: The Port that you are going to connect to, usually 80 for HTTP and 443 for HTTPS.
- Path: A Query String is a part of a URL that provides additional parameters to the server when accessing a specific resource. It typically follows a '?' in the URL and consists of key-value pairs separated by '&'. 
- Query String: Extra bits of information that can be sent to the requested path. For example, /blog?id=1 would tell the blog path that you wish to receive the blog article with the id of 1.
- Fragment: This is a reference to a location on the actual page requested. This is commonly used for pages with long content and can have a certain part of the page directly linked to it, so it is viewable to the user as soon as they access the page.

### Making a Request

It's possible to make a request to a web server with just one line GET / HTTP/1.1.But for a much richer web experience, you’ll need to send other data as well. This other data is sent in what is called headers, where headers contain extra information to give to the web server you’re communicating with.

> Example Request:

```
GET / HTTP/1.1

Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/

```

Key Lines:

* GET / → Ask for homepage using GET method.
* Host → Target domain.
* User-Agent → Browser making the request.
* Referer → Page we came from (optional).
* Blank Line → Marks end of request.

> Example Response:

```
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98


<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>
```

Key Lines:

* HTTP/1.1 200 OK → Protocol + status code (success).
* Server → Web server software used.
* Date → Timestamp of response.
* Content-Type → Tells browser how to handle data.
* Content-Length → Size of the body (bytes).
* HTML → The actual content (web page).

## HTTP methods

HTTP methods are a way for the client to show their intended action when making an HTTP request. There are a lot of HTTP methods but we'll cover the most common ones, although mostly you'll deal with the GET and POST method.

GET Request

> This is used for getting information from a web server.

POST Request

> This is used for submitting data to the web server and potentially creating new records

PUT Request

> This is used for submitting data to a web server to update information

DELETE Request

> This is used for deleting information/records from a web server.

## HTTP Status Codes
HTTP server responds, the first line always contains a status code informing the client of the outcome of their request and also potentially how to handle it. These status codes can be broken down into 5 different ranges:

| Code Range  | Meaning                                                                                      |
| ----------- | -------------------------------------------------------------------------------------------- |
| **100–199** | Informational – Request received, continue processing. Rarely seen.                          |
| **200–299** | Success – Request was received and processed successfully.                                   |
| **300–399** | Redirection – Further action needs to be taken (redirect to another page or site).           |
| **400–499** | Client Error – There was an issue with the request sent by the client (your browser/tool).   |
| **500–599** | Server Error – The server failed to fulfill a valid request. Usually a problem on their end. |

Common HTTP Status Codes:

- 200 OK – Everything worked.
- 201 Created – New resource was created.
- 301 Moved Permanently – Page has been moved forever.
- 302 Found – Temporary redirect. Client should try the new location just this time.
- 400 Bad Request – The request was invalid, malformed, or missing parameters.
- 401 Unauthorized – You must log in first. No/invalid credentials provided.
- 403 Forbidden – You’re not allowed to access this, even if logged in.
- 404 Not Found – The server can’t find the page or file you asked for.
- 405 Method Not Allowed – You used the wrong HTTP method (like using GET when POST is expected).
- 500 Internal Server Error – Something crashed or misfired on the server. Usually not your fault
- 502 Bad Gateway – Server got an invalid response from another server it was trying to reach.
- 503 Service Unavailable – Server is temporarily overloaded or under maintenance.

> great [http.cat](https://http.cat/) resource to study status codes.

## Headers

Headers are key-value pairs sent along with HTTP requests/responses.They carry extra metadata that helps the client and server handle the request/response correctly.

### Common Request Headers (Client → Server)

- Host: Tells the server which domain you want (important when multiple domains are hosted on one IP).
- User-Agent: Describes your browser and version (e.g., Mozilla/5.0 Chrome/115).
- Content-Length: Tells the server how much data you're sending (used in POST/PUT requests).
- Accept-Encoding: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.
- Cookie: Sends stored cookies (e.g., session tokens) to the server.

### Common Response Headers (Server → Client)

- Set-Cookie: Instructs browser to store a cookie (used for login sessions, tracking, etc.).
- Cache-Control: Tells the browser how long to keep the content cached.
- Content-Type: Specifies data format (HTML, JSON, CSS, image/jpeg, etc.).
- Content-Encoding: Tells how the content was compressed before sending (e.g., gzip).

> *Cookies can be used for many purposes but are most commonly used for website authentication. The cookie value won't usually be a clear-text string where you can see the password, but a token (unique secret code that isn't easily humanly guessable).
