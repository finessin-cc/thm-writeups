# TryHackMe: HTTP in Detail

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | HTTP Fundamentals           |
| Difficulty    | Beginner                    |
| Date          | July 10, 2021               |

## Task 1: What is HTTP(S)?

### HTTP (HyperText Transfer Protocol)
- Protocol for communicating with web servers
- Developed by Tim Berners-Lee (1989-1991)
- Used for transmitting webpage data (HTML, Images, Videos, etc.)

### HTTPS (HyperText Transfer Protocol Secure)
- Secure version of HTTP
- Encrypts data transmission
- Provides assurance of correct web server identification

**Questions:**
- What does HTTP stand for?
  - **Answer:** HyperText Transfer Protocol
- What does the S in HTTPS stand for?
  - **Answer:** secure
- On the mock webpage on the right there is an issue, once you've found it, click on it. What is the challenge flag?
  - **Answer:** `THM{INVALID_HTTP_CERT}`

## Task 2: Requests And Responses

### URL Structure
URL components include:
- **Scheme**: Protocol (HTTP, HTTPS, FTP)
- **User:Password**: Authentication credentials
- **Host**: Domain name or IP address
- **Port**: Connection port (80 for HTTP, 443 for HTTPS)
- **Path**: Resource location
- **Query String**: Additional parameters
- **Fragment**: Page reference

### HTTP Request Example
```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

### HTTP Response Example
```http
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

**Questions:**
- What HTTP protocol is being used in the above example?
  - **Answer:** HTTP/1.1
- What response header tells the browser how much data to expect?
  - **Answer:** Content-Length

## Task 3: HTTP Methods

HTTP methods define the action to be performed on a resource:

- **GET**: Retrieve information from server
- **POST**: Submit data to server (create new records)
- **PUT**: Update existing information on server
- **DELETE**: Remove information/records from server

**Questions:**
- What method would be used to create a new user account?
  - **Answer:** POST
- What method would be used to update your email address?
  - **Answer:** PUT
- What method would be used to remove a picture you've uploaded to your account?
  - **Answer:** DELETE
- What method would be used to view a news article?
  - **Answer:** GET

## Task 4: HTTP Status Codes

Status codes are grouped into five ranges:

**100-199**: Information Response (rarely used)
**200-299**: Success
**300-399**: Redirection
**400-499**: Client Errors
**500-599**: Server Errors

Common status codes:
- **200 OK**: Request completed successfully
- **201 Created**: Resource created successfully
- **301 Moved Permanently**: Permanent redirect
- **302 Found**: Temporary redirect
- **400 Bad Request**: Client request error
- **401 Not Authorized**: Authentication required
- **403 Forbidden**: Access denied
- **404 Not Found**: Resource doesn't exist
- **500 Internal Server Error**: Server-side error
- **503 Service Unavailable**: Server overloaded or down

**Questions:**
- What response code might you receive if you've created a new user or blog post article?
  - **Answer:** 201
- What response code might you receive if you've tried to access a page that doesn't exist?
  - **Answer:** 404
- What response code might you receive if the web server cannot access its database and the application crashes?
  - **Answer:** 503
- What response code might you receive if you try to edit your profile without logging in first?
  - **Answer:** 401

## Task 5: Headers

Headers provide additional information in HTTP requests and responses.

### Common Request Headers
- **Host**: Identifies target website
- **User-Agent**: Browser information
- **Content-Length**: Size of request body
- **Accept-Encoding**: Supported compression methods
- **Cookie**: Stored session information

### Common Response Headers
- **Set-Cookie**: Cookie data to store
- **Cache-Control**: Browser caching instructions
- **Content-Type**: Type of returned data
- **Content-Encoding**: Compression method used

**Questions:**
- What header tells the web server what browser is being used?
  - **Answer:** User-Agent
- What header tells the browser what type of data is being returned?
  - **Answer:** Content-Type
- What header tells the web server which website is being requested?
  - **Answer:** Host

## Task 6: Cookies

Cookies are small pieces of data stored on the client's computer that persist between visits to websites.

### Cookie Functionality
- Store user session information
- Maintain authentication state
- Remember preferences and settings
- Track user behavior

### Cookie Flow
1. Server sends `Set-Cookie` header
2. Browser stores cookie data
3. Subsequent requests include cookie data in `Cookie` header
4. Server uses cookie data to identify user

**Question:**
- Which header is used to save cookies to your computer?
  - **Answer:** Set-Cookie

## Task 7: Making Requests

Using the HTTP request emulator, various HTTP operations can be performed:

**Questions:**
- Make a GET request to /room page
  - **Answer:** `THM{YOU'RE_IN_THE_ROOM}`
- Make a GET request to /blog page and set the id parameter to 1
  - **Answer:** `THM{YOU_FOUND_THE_BLOG}`
- Make a DELETE request to /user/1 page
  - **Answer:** `THM{USER_IS_DELETED}`
- Make a PUT request to /user/2 page with the username parameter set to admin
  - **Answer:** `THM{USER_HAS_UPDATED}`
- Make a POST request to /login page with the username of thm and a password of letmein
  - **Answer:** `THM{HTTP_REQUEST_MASTER}`
