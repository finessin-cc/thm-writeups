# TryHackMe: Putting it all together

## Room Metadata

| Field         | Value                       |
|---------------|-----------------------------|
| Platform      | TryHackMe                   |
| Type          | Web Fundamentals            |
| Difficulty    | Beginner                    |
| Date          | July 10, 2021               |

## Task 1: Putting It All Together

When requesting a webpage, several components work together:
1. DNS resolution to find the server's IP address
2. HTTP protocol communication between client and web server
3. Web server returns HTML, JavaScript, CSS, Images, etc.
4. Browser formats and displays the website

Additional components that enhance web functionality:
- Load balancers for traffic management
- CDNs for content delivery optimization
- Databases for data storage
- WAFs for security protection

## Task 2: Other Components

### Load Balancers
When website traffic increases or requires high availability, load balancers distribute requests across multiple servers. They perform:
- **Health checks**: Periodic verification of server status
- **Load distribution**: Using algorithms like round-robin or weighted distribution
- **Failover capability**: Redirecting traffic away from unresponsive servers

### CDN (Content Delivery Networks)
CDNs host static files across thousands of global servers to:
- Reduce latency by serving content from geographically closer locations
- Decrease traffic to origin servers
- Improve website performance and user experience

### Databases
Websites often require data storage capabilities. Common database types include:
- MySQL
- MSSQL
- MongoDB
- Postgres
Databases range from simple text files to complex multi-server clusters providing speed and resilience.

### WAF (Web Application Firewall)
WAFs protect web servers by:
- Analyzing web requests for attack patterns
- Validating requests come from legitimate browsers
- Implementing rate limiting to prevent abuse
- Blocking malicious requests before they reach the web server

**Questions:**
- What can be used to host static files and speed up a client's visit to a website?
  - **Answer:** CDN
- What does a load balancer perform to make sure a host is still alive?
  - **Answer:** health check
- What can be used to help against the hacking of a website?
  - **Answer:** WAF

## Task 3: How Web Servers Work

### What is a Web Server?
A web server is software that listens for incoming connections and delivers web content using the HTTP protocol. Common web server software includes:
- Apache
- Nginx
- IIS
- NodeJS

Web servers serve files from a root directory defined in software settings:
- Linux: `/var/www/html`
- Windows: `C:\inetpub\wwwroot`

### Virtual Hosts
Web servers can host multiple websites with different domain names using virtual hosts. The server checks HTTP headers for the requested hostname and matches against configured virtual hosts. Each virtual host can have its own root directory mapping.

**Examples:**
- `one.com` mapped to `/var/www/website_one`
- `two.com` mapped to `/var/www/website_two`

### Static vs Dynamic Content
- **Static content**: Never changes (images, JavaScript, CSS, unchanging HTML)
- **Dynamic content**: Changes based on requests (blog posts, search results)

Dynamic content is processed by backend systems using programming languages like:
- PHP
- Python
- Ruby
- NodeJS
- Perl

Backend processing happens behind the scenes - clients cannot see backend code in HTML source.

**Questions:**
- What does web server software use to host multiple sites?
  - **Answer:** Virtual Hosts
- What is the name for the type of content that can change?
  - **Answer:** Dynamic
- Does the client see the backend code? Yay/Nay
  - **Answer:** Nay

## Task 4: Quiz

Using knowledge from previous modules, the correct order of how a website request works is:
1. Client makes HTTP request
2. DNS resolution to find IP address
3. Request reaches web server
4. Web server processes request
5. Response returned to client
6. Browser renders content

**Question:** Flag
- **Answer:** `THM{YOU_GOT_THE_ORDER}`
