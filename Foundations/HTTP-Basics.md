# Technical Reference: HTTP Fundamentals
**Source:** TryHackMe - HTTP in Detail Room
**Focus:** Skill #5 (Security Standards) & Skill #4 (Developer Collaboration)

## 📌 Executive Summary
Understanding the HTTP protocol is the baseline for all Product Security. This reference covers the request-response lifecycle, headers, and status codes—the "language" used to identify and remediate web vulnerabilities.

---

## 🛠 Key Technical Concepts

### 1. The Request-Response Lifecycle
Every action in a web app starts with a **Request** and ends with a **Response**. 
* **Key takeaway:** Security vulnerabilities often live in how the server *interprets* the request data (like URL parameters or Headers).
* Basic terms
* HTTP - HyperText Transfer Protocol
* HTTPS - HyperText Transfer Protocol | Secure - Data is encrypted and assures you that you are talking to the correct website.
* Scheme - this instructs on what protocol to use for accessing the resource, such as HTTP, HTTPS.. ETC
* User - Some services require authentication to log in; you can put a username and password into the URL to log in.
* Host - The domain name or IP address of the Servers you wish to access.
* Port - The Port that you are going to connect to, usually 80 for HTTP and 443 for HTTPS. But it could be hosted on any port between 1 and 65535.
* Query string - Bits of information that can be sent to the requested path. Example /blog?id=1 would tell the path that you wish to receive the blog article with the id of 1.
* Fragment - this is a reference to a location that can be sent to the requested path. Common for pages with long content.

* ### EXAMPLE REQUEST ###
*  GET / HTTP/1.1

*  Host: tryhackme.com
*  User-Agent: Mozilla/5.0 Firefox/87.0
*  Referer: https://tryhackme.com/

*  ### EXAMPLE RESPONSE ###
*  HTTP/1.1 200 OK

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

### 2. HTTP Methods (Verbs)
| Method | Purpose | Security Context |
| :--- | :--- | :--- |
| **GET** | Retrieve data | Sensitive data should NEVER be in a GET request (it stays in browser history/logs). |
| **POST** | Submit data | Used for logins/forms. Requires CSRF protection. |
| **PUT/DELETE** | Modify/Remove | If these are enabled without strict Auth, it leads to "Broken Access Control." |

### 3. Status Codes (The "Health" of the App)
* **100-199:** Information Response - this tells the client the first part of their request has been accepted and they should continue sending the rest. These codes are not common anymore. 
* **200-299:** Request successful.
* **300-399:** Redirect:** Can be abused for "Open Redirect" attacks.
* **400-499:** Client Errors. 401 means "Who are you?" (Unauthenticated). 403 means "I know who you are, but you can't go here" (Unauthorized).
* **500-599:** Internal Server Error:** Often leaks stack traces, which helps an attacker map the technology stack.

  ### Common HTTP Status Codes ###
  * 200 - Ok - Request was successful
  * 201- Created - a resource has been created
  * 301 - Moved Permanently - redirects the client's browser to a new webpage.
  * 302 - Found - Similar to the above permanent redirect, but as the name suggests, this is only a temporary change.
  * 400 - Bad Request - tells the browser that something was either wrong or missing in their request.
  * 401 - Not Authorized - you are not currently allowed to view the resource until you have authorized with the web application.
  * 403 - Forbidden - You don't have permission, whether you are logged in or not.
  * 404 - Page Not Found - the page/resource you requested does not exist.
  * 500 - Internal Service Error - The Server has encountered some kind of error with your request that it doesn't know how to handle properly.
  * 503 - Service Unavailable - This server cannot handle your request as it's either overloaded or down. 

### 4. Headers 
### Common Request Headers ###
Host: Some web servers host multiple websites, so by providing the host headers, you can tell it which one you require; otherwise, you'll just receive the default website for the server.

User-Agent: This is your browser software and version number, telling the web server your browser software helps it format the website properly for your browser and also some elements of HTML, JavaScript and CSS are only available in certain browsers.

Content-Length: When sending data to a web server, such as in a form, the content length tells the web server how much data to expect in the web request. This way the server can ensure it isn't missing any data.

Accept-Encoding: Tells the web server what types of compression methods the browser supports so the data can be made smaller for transmitting over the internet.


Cookie: Data sent to the server to help remember your information (see cookies task for more information).
Common Response Headers

These are the headers that are returned to the client from the server after a request.

Set-Cookie: Information to store which gets sent back to the web server on each request (see cookies task for more information).

Cache-Control: How long to store the content of the response in the browser's cache before it requests it again.

Content-Type: This tells the client what type of data is being returned, i.e., HTML, CSS, JavaScript, Images, PDF, Video, etc. Using the content-type header the browser then knows how to process the data.

Content-Encoding: What method has been used to compress the data to make it smaller when sending it over the internet.  

---
