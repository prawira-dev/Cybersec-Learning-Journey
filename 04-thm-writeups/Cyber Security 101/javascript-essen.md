# JavaScript Essentials
## Intro
* **Overview:** Introduces JavaScript (JS) as a core scripting language used alongside HTML and CSS to add dynamic interactivity—such as user validation, click actions, and animations—to web pages.
* **Cybersecurity Perspective:** The room focuses on understanding JavaScript fundamentals from an offensive perspective, specifically examining how hackers leverage legitimate scripting functionalities to achieve malicious goals.
* *Prerequisites & Learning Objectives:*
    * Recommends foundational Linux and web application knowledge.
    * Covers JS basics, HTML integration, abusing dialogue functions, bypassing control flow statements, and analyzing minified files.
* **Lab Environment:** Highlights that the lab machine (jsessential1.1-badr) includes pre-written practice scripts located in the desktop exercise folder on the attached virtual machine for hands-on learning.

## Essential Concepts
* **Variables:** Containers used to store data values. JavaScript provides three keywords for variable declaration: `var` (function-scoped), `let` (block-scoped), and `const` (block-scoped constant values).
* **Data Types:** Define the classification of values a variable can hold, including strings, numbers, booleans, null, undefined, and objects (such as arrays).
* **Functions:** Reusable blocks of code designed to perform specific tasks, helping to organize logic and avoid repetitive code by accepting arguments and returning outputs.
* **Loops:** Control structures (such as `for`, `while`, and ``...while`) that allow a block of code to run multiple times repeatedly as long as a specified condition remains true.
* **Request-Response Cycle:** The fundamental mechanism of web communication where a client's browser sends a request to a web server, and the server processes it and sends back the corresponding resources or data.

## JavaScript Overview
* **Client-Side Execution:** JavaScript primarily runs inside the user's web browser on the client side, allowing web applications to respond to user actions instantly without needing to constantly query the backend server.
* **The Document Object Model (DOM):** JS interacts directly with the DOM, which represents the page's structure as a tree of objects. This enables scripts to dynamically modify elements, change styles, or update content on the fly.
* **Asynchronous Processing (AJAX/Fetch):** JavaScript uses asynchronous capabilities (such as `fetch` and AJAX) to send and receive data from servers in the background, updating parts of a webpage without requiring a full page reload.
* **Security Implications:** Because JavaScript code executes entirely on the client side, attackers can easily view, modify, or debug it. This means developers should never rely solely on client-side validation or logic for security, as it can be easily bypassed.

## Integrating JavaScript in HTML
* **Internal JavaScript:** Involves embedding JS code directly inside the HTML document using `<script>` tags, typically placed in the `<head>` or `<body>` section. This approach is great for beginners to see how code interacts with the Document Object Model (DOM) elements on a single page.
* **External JavaScript:** Involves storing JS code in a separate file with a `.js` extension, keeping the HTML file clean and organized. The external file is linked inside the HTML using the src attribute within a `<script>` tag, which also allows the same script to be easily reused across multiple web pages.
* **Verification & Reconnaissance:** During web application penetration testing, you can determine how a page integrates JavaScript by viewing the page source (`Ctrl+U` or right-click -> View Page Source). Code inside standard `<script>` tags indicates internal scripts, while a `<script src="...">` tag indicates an external script file being loaded.

## Abusing Dialogue Functions
* **Overview:** Explores JavaScript's built-in interactive dialogue functions —`alert`, `prompt`, and `confirm`— and how they can be manipulated or abused in malicious files (like a spoofed invoice.html) to cause browser disruption or annoyance.
* **Key Functions:**
    * `alert()`: Displays a message box with an "OK" button to convey warnings or information.
    * `prompt()`: Opens a dialogue box to gather user input, returning the typed string or null if cancelled.
    * `confirm()`: Shows a box with "OK" and "Cancel" buttons, returning a boolean (true or false) based on user choice.
* **Security Implications:** Attackers can embed loops containing these functions (e.g., repeating an `alert` hundreds of times) within standalone HTML files to spam the victim, freeze the browser tab, or create a frustrating user experience.

## Bypassing Control Flow Statements
* **Overview:** Explores how control flow structures (like `if-else` conditional statements) govern program logic and execution order, and demonstrates how client-side authentication logic can be reviewed and bypassed.
* **Conditional Statements:** Control structures check whether specific expressions evaluate to true or false to determine which code block runs. For example, an age verification script uses an `if (age >= 18)` statement to display one message for adults and another for minors.
* **Client-Side Security Flaws:** Because JavaScript executes entirely within the user's browser, any authentication checks or hardcoded credential validations performed via client-side scripts can be easily inspected, manipulated, or bypassed by reviewing the source code.

## Best Practices
* **Avoid Relying Solely on Client-Side Validation:** Because users can easily disable or manipulate JavaScript in their browsers, developers must always implement server-side validation alongside client-side checks.
* *Refrain from Adding Untrusted Libraries:* Avoid blindly including third-party JavaScript libraries via external `<script>` sources, as malicious actors frequently publish fake or lookalike libraries containing malicious code.
* **Avoid Hardcoded Secrets:** Never embed sensitive information like API keys, access tokens, or credentials directly into JavaScript source code, where anyone can view them via the browser.
* **Minify and Obfuscate Code:** While not a foolproof security control, minifying and obfuscating production code reduces file size, improves performance, and adds a layer of complexity to deter casual reverse engineering.