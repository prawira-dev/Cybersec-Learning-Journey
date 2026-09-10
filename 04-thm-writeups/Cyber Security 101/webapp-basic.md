# Web Application Basics
## Intro
* Overview: Provides a foundational walkthrough of key web application elements, ideal for beginners or those working with web apps.
* Core Concepts Covered:
    * How web applications function within a web browser.
    * Breaking down URL components and their role in accessing resources.
    * The mechanics of HTTP requests and responses.
    * Different types of HTTP request methods and response status codes.
    * The function of HTTP headers, specifically their importance for security.

## Web Application Overview
The planet analogy explains the core components of Web Application Basics:
### Front End
The visible elements users interact with inside the browser.
* **HTML (Hypertext Markup Language):** The foundational code that instructs the browser on what to display.
* **CSS (Cascading Style Sheets):** Controls the standard appearance, layout, and colors.
* **JavaScript (JS):** Enables complex activity, interactions, and dynamic decisions on the page.

### Back End
The unseen underlying engine and infrastructure that enables the application to function.
* Database: The repository where information is stored, modified, and retrieved.
* Infrastructure: The web servers, storage, and networking devices that support the application.
* WAF (Web Application Firewall): An optional protective layer that filters out dangerous traffic to secure the web server.

## Uniform Resource Locator
* Overview: A URL is a web address that guides your browser to a specific resource on the internet. Understanding its anatomy is crucial for web browsing, development, and security troubleshooting.
![url-anatomy](../images/url-anatomy.png)
Source: TryHackMe
* Anatomy of a URL:
    * Scheme (Protocol): Defines how the resource is accessed. The most common are HTTP and HTTPS. HTTPS is highly recommended as it encrypts the communication.
    * User: Historically used to include login credentials in the URL, but this is a major security risk and rarely used today.
    * Host/Domain: The unique address of the website. Attackers often use typosquatting (registering misspelled versions of popular domains) for phishing attacks.
    * Port: Directs the browser to the correct service on the server. Common ports are 80 (HTTP) and 443 (HTTPS).
    * Path: Acts as a roadmap pointing to the exact file or page on the server.
    * Query String: Starts with a question mark (?) and passes additional information like search terms or form inputs. It must be handled securely to prevent injection attacks.
    * Fragment: Starts with a hash (#) and points the browser to a specific section or heading on that webpage. Like query strings, these must be secured against injections.

## HTTP Message
* **Overview:** HTTP messages are the packets of data exchanged between a client (user) and a web server. Understanding them is critical for diagnosing web communication issues and implementing strong security measures.
* **Types of HTTP Messages:**
    * **HTTP Requests:** Sent by the user/client to trigger an action on the web application.
    * **HTTP Responses:** Sent back by the web server after processing the user's request.
* **Message Structure:** Every HTTP message follows a specific format to ensure smooth communication:
    * **Start Line:** The introduction that indicates whether it is a request or a response, along with important handling details.
    * **Headers:** Key-value pairs providing instructions and extra information (like security settings or content types) to the client or server.
    * **Empty Line:** A crucial divider that separates the headers from the body. Without it, the client or server might misinterpret the message.
    * **Body:** Contains the actual data being transferred (e.g., login form data in a request, or the requested webpage/API data in a response).

## HTTP Request: Request Line and Methods
An HTTP request is the initial communication sent by a user's browser to a web server to initiate an action. The first part of this request is the Request Line, which consists of three core components:
* **HTTP Method:** Defines the requested action.
    * **GET:** Retrieves data. Security note: Do not use for sensitive data like passwords, as they can appear in plaintext.
    * **POST:** Submits data. Security note: Always validate input to prevent attacks like SQL injection or XSS.
    * **PUT & DELETE:** Updates or removes data. Security note: Requires strict authorization checks.
    * **Other Methods:** PATCH (partial updates), HEAD (retrieves headers only), OPTIONS (lists allowed methods), TRACE (debugging), and CONNECT (HTTPS setup). For security, OPTIONS and TRACE should often be disabled if unnecessary.
* **URL Path:** Specifies the exact location of the resource on the server (e.g., `/api/users/123`). This must be strictly validated and sanitized to prevent injection attacks and unauthorized access.
* **HTTP Version:** Indicates the protocol version in use. While HTTP/2 and HTTP/3 provide enhanced speed and security, HTTP/1.1 remains the most widely adopted version due to its broad compatibility and introduction of features like persistent connections.

## HTTP Request: Headers and Body
### Request Headers
Headers provide the web server with additional instructions and context about the incoming request. Key headers include:
* **Host:** Specifies the domain name of the target web server.
* **User-Agent:** Identifies the client's web browser and operating system.
* **Referer:** Indicates the URL that linked to or initiated the current request.
* **Cookie:** Sends stored data back to the server to maintain session states (like tracking if a user is logged in).
* **Content-Type:** Declares the format of the data being sent in the request body.

### Request Body
Used primarily with methods like POST and PUT, the body contains the actual data being sent to the server. Common data formats include:
* **URL Encoded (`application/x-www-form-urlencoded`):** The default format for basic web form submissions. It structures data as key-value pairs separated by ampersands (e.g., name=Aleksandra&age=27).
* **Form Data (`multipart/form-data`):** Best suited for sending binary data, such as file or image uploads. It separates different blocks of data using a defined boundary string.
* **JSON (`application/json`):** A highly common format that structures data in name-value pairs enclosed within curly braces {}.
* **XML (`application/xml`):** Structures data hierarchically using nested opening and closing tags.

## HTTP Response
### HTTP Response Status Line
When a server replies to a client, the very first line of that response is the Status Line. It provides three critical pieces of information:
* **HTTP Version:** Identifies the version of the protocol being used.
* Status Code: A 3-digit numerical code indicating whether the request succeeded or encountered an error.
* **Reason Phrase:** A short, human-readable text explanation accompanying the status code.

### Categories of Status Codes
* **100-199 (Informational):** Indicates that the server has received the request and is continuing the process.
* **200-299 (Successful):** Confirms that the request was successfully received, understood, and processed (e.g., `200 OK`).
* **300-399 (Redirection):** Tells the client that further action is needed to complete the request, usually involving a new URL (e.g., `301 Moved Permanently`).
* **400-499 (Client Error):** Points out an issue with the client's request, such as a missing parameter, lack of authorization, or a mistyped URL (e.g., `404 Not Found`).
* **500-599 (Server Error):** Signals that the server failed to fulfill a seemingly valid request due to a server-side issue (e.g., `500 Internal Server Error`).

## HTTP Response: Headers and Body
* **Overview:** Focuses on the structure of HTTP responses sent back by the server, highlighting the role of response headers and the response body in delivering data and maintaining security.
* **Key Response Headers:**
    * **Date:** Displays the exact date and time the server generated the response.
    * **Content-Type:** Tells the client what format the response content is in (e.g., HTML, JSON) along with the character set.
    * **Server:** Reveals software details about the web server handling the request.
    * **Set-Cookie:** Transmits cookies to the client. To secure these, security flags like HttpOnly (blocks JavaScript access to mitigate XSS) and Secure (ensures transmission only over HTTPS) must be applied.
    * **Cache-Control:** Dictates client-side caching rules and freshness lifespans.
    * **Location:** Used in 3xx redirection responses to point the client to a new resource path.
* **Response Body:** Contains the actual payload data sent by the server, such as HTML documents, JSON payloads, or images. Proper input sanitization and escaping within the response body are essential to prevent vulnerabilities like Cross-Site Scripting (XSS).

## Security Headers
* **Overview:** Security headers act as an additional defense layer to protect web applications against common web vulnerabilities like Cross-Site Scripting (XSS), clickjacking, and MIME-sniffing attacks.
* **Key Security Headers:**
    * **Content-Security-Policy (CSP):** Allows administrators to control which domains and content sources are deemed safe. Properties like `default-src` set a baseline rule, while `script-src` and `style-src` define specific loading origins (e.g., using `'self'` for the current domain).
    * **Strict-Transport-Security (HSTS):** Enforces secure HTTPS connections over time using parameters like `max-age` (duration in seconds), `includeSubDomains` (applies the policy to all subdomains), and `preload` (inclusion in browser preload lists).
    * **X-Content-Type-Options:** Prevents MIME-sniffing attacks. Setting it to `nosniff` forces the browser to strictly follow the declared Content-Type instead of guessing file types.
* **Referrer-Policy:** Manages how much referrer information is shared when a user navigates away via hyperlinks, offering privacy levels such as `no-referrer`, `same-origin`, `strict-origin`, and `strict-origin-when-cross-origin`.

## Practical Task: Making HTTP Requests
* **Overview:** A hands-on exercise utilizing a built-in static site emulator to test your understanding of HTTP request methods and API endpoint interactions.
* **Practical Challenges & Objectives:**
    * **GET Request (`/api/users`):** Retrieves the list of current users from the application to test standard data fetching.
    * **POST Request (`/api/user/2`):** Submits updated payload data to modify an existing resource—specifically changing user Bob's country from "UK" to "US".
    * **DELETE Request (`/api/user/1`):** Sends a removal request targeting a specific user ID to test resource deletion workflows.
* **Goal:** Successfully execute each HTTP request inside the emulator interface to uncover and capture the respective flag for each question.