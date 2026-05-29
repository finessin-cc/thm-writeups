# TryHackMe: How Websites Work

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Web Fundamentals            |
| Difficulty    | Beginner                    |
| Date          | July 10, 2021               |

## Task 1: How Websites Work

Websites operate through a client-server model where browsers make requests to web servers for page information. The two major components of a website are:

- **Front End (Client-Side)**: How the browser renders a website
- **Back End (Server-Side)**: A server that processes requests and returns responses

**Question:** What term best describes the component of a web application rendered by your browser?
- **Answer:** Front End

## Task 2: HTML

HTML (HyperText Markup Language) is the primary language for creating websites. Key components include:

- `<!DOCTYPE html>`: Defines HTML5 document type
- `<html>`: Root element of the HTML page
- `<head>`: Contains page metadata
- `<body>`: Contains visible content
- `<h1>`: Large heading element
- `<p>`: Paragraph element

HTML elements can have attributes:
- `class`: Used for styling
- `src`: Specifies image location
- `id`: Unique identifier for elements

**Questions:**
- One of the images on the cat website is broken - fix it, and the image will reveal the hidden text answer!
  - **Answer:** HTMLHERO
- Add a dog image to the page by adding another img tag on line 11. The dog image location is img/dog-1.png. What is the text in the dog image?
  - **Answer:** DOGHTML

## Task 3: JavaScript

JavaScript enables interactive web pages by:
- Dynamically updating content in real-time
- Adding functionality to buttons and events
- Controlling page behavior based on user actions

JavaScript can be embedded in HTML using `<script>` tags or loaded externally with the `src` attribute:
```html
<script src="/location/of/javascript_file.js"></script>
```

Event handling examples:
```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

```html
<button onclick='document.getElementById("demo").innerHTML = "Button Clicked";'>Click Me!</button>
```

**Questions:**
- Click the "View Site" button on this task. On the right-hand side, add JavaScript that changes the demo element's content to "Hack the Planet"
  - **Answer:** JSISFUN

## Task 4: Sensitive Data Exposure

Sensitive Data Exposure occurs when websites fail to properly protect or remove sensitive clear-text information from frontend source code. This includes:

- Login credentials
- Hidden links to private sections
- Other sensitive data in HTML or JavaScript

Attackers can leverage this information to gain unauthorized access to web applications or backend components.

**Question:** View the website on this link (opens in new tab). What is the password hidden in the source code?
- **Answer:** testpasswd

## Task 5: HTML Injection

HTML Injection is a vulnerability that occurs when unfiltered user input is displayed on a webpage. Key points include:

- Unfiltered user input can be used to inject HTML code
- User input should never be trusted
- Input sanitization is crucial for security
- Attackers can manipulate page appearance and functionality

The vulnerability works because user input is directly used in JavaScript functions without proper sanitization.

**Question:** View the website on this task and inject HTML so that a malicious link to http://hacker.com is shown.
- **Answer:** HTML_INJ3CTI0N
