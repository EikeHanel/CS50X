# HTML, CSS, JavaScript
- **Notes:** https://cs50.harvard.edu/x/2024/notes/8/git

- HTML AND CSS are languages for presentation
  - Markup languages
- JavaScript 
  - Programing language which is very commoly used with the context of browsers
    - Interactive Interfaces
    - Server side

## 1. Acronomys
- **IP** - Internet Protocol
  - IP addresses (**IPv4**) 32bit ~4,000,000,000 possible addresses
    - Every computer has an unique address
    - Addresses have this layout: #.#.#.#
  - At the moment we gradually chage to the **IPv6** - 128bit
- **TCP** - Transmission Control Protocol
  - TCP is one of the core protocols of the internet. It ensures reliable, ordered, and error-checked delivery of data between applications communicating over a network. It is part of the TCP/IP suite, which forms the foundation of internet communication.
  - **Reliable Transmission**: 
    - Ensures all data packets are received in the correct order. If a packet is lost, it will be resent.
  - **Connection-Oriented**: 
    - Establishes a connection between the sender and receiver before data transfer begins, ensuring both parties are ready for communication.
  - **Error Detection and Correction**: 
    - Identifies issues in data transmission and rectifies them to ensure accuracy.
- **TCP Ports**
  - Numerical identifiers (0–65535 (16-Bit)) that act as endpoints in a TCP connection.
  - Ports help route incoming and outgoing traffic to the correct application or service.
  - TCP communication pairs an IP address with a port number (e.g., `192.168.1.1:80`)
  - **Common Port Numbers**:
    - 80 - HTTP - Standard web traffic.
    - 443 - HTTPS - Encrypted web traffic (via SSL/TLS).
    - ...
  - **DNS** - Domain Name System
    - The Domain Name System (DNS) is like the phonebook of the internet. It translates human-readable domain names (e.g., www.example.com) into IP addresses (e.g., 192.168.1.1) that computers use to identify each other on the network. Like a dictionary - key/value pairs.
  - Root DNS Servers:
    - The top of the DNS hierarchy. There are 13 sets of root servers globally.
- **DHCP** - Dynamic Host Configuration Protocol
  - The Dynamic Host Configuration Protocol (DHCP) is a network protocol used to automatically assign IP addresses and other configuration parameters (e.g., subnet mask, default gateway, DNS servers) to devices on a network.

### 1.1 HTML Acronyms
- **HTML** - HyperText Markup Language
  - The standard language used to create the structure of web pages. It defines elements like headings, paragraphs, links, and more.
- **DOM** - Document Object Model
  - A programming interface that represents the structure of a webpage as a tree of objects. JavaScript uses it to manipulate and interact with the page.
- **URL** - Uniform Resource Locator
  - The address used to access resources on the web (e.g., `https://www.example.com`).
- **HTTP** - HyperText Transfer Protocol
  - The protocol used for communication between a client (browser) and a server on the web.
- **HTTPS** - HyperText Transfer Protocol Secure
  - An encrypted version of HTTP that ensures secure communication over the web.

### 1.2 CSS Acronyms:
- **CSS** - Cascading Style Sheets
  - The language used to style and layout HTML elements, including colors, fonts, spacing, and more.
- **RGB** - Red, Green, Blue
  - A color model used in CSS to define colors in terms of red, green, and blue values.
- **HSL** - Hue, Saturation, Lightness
  - Another color model in CSS that represents colors based on hue (color type), saturation (intensity), and lightness (brightness).
- **ID** - Identifier
  - A unique identifier in CSS or HTML used to target specific elements.
- **EM** - Element Measurement 
  - A relative unit in CSS, often used for font sizes, where 1em equals the size of the parent element.

## 1.3 JavaScript Acronyms:
- **JS** - JavaScript
  - A programming language used to add interactivity and dynamic behavior to webpages.
- **AJAX** - Asynchronous JavaScript and XML
  - A technique that allows webpages to load data in the background without refreshing the page.
- **JSON** - JavaScript Object Notation
  - A lightweight data format used for exchanging data between a server and a client.
- **API** - Application Programming Interface 
  - A set of functions and protocols that allow interaction with external software or services.
- **ES** - ECMAScript
  - The standard that JavaScript follows. Different versions (e.g., ES6) introduce new features.
- **DOM** (again, as it's part of JavaScript as well as HTML)

## 1.4 General Acronyms Related to Web Development:
- **CSSOM** - CSS Object Model
  - Similar to the DOM, it represents the styles and rules of a webpage.
- **SEO** - Search Engine Optimization
  - Techniques used to make websites rank higher in search engine results.
- **CDN** - Content Delivery Network
  - A distributed network of servers that delivers web content more quickly by serving it from servers close to the user.
- **UI** - User Interface
  - The part of a website or application that users interact with.
- **UX** - User Experience
  - How users feel and interact with the website or application.


## 2. HTTPS

- **https://www.example.com/**
  - **Last /** means: Give me the Root of the website (Default folder)
  - **/...** is called a path
    - maybe a file maybe a folder etc.+
    - **/file.html** - file path
    - **/folder/** represents a folder
  - **www.example.com**: Fully qualified domain name
  - **www.** typically called a host name
    - wherein the domain lives (www. hosts the domain example.com)
  - **.com** - top level domain 
  - **https** - scheme/protocol

# 3. Request GET POST

- **GET Method**:
  - The **GET** method is used to retrieve data from a server. It sends data in the URL (query string) and is used for requests that do not modify data.
- **POST Method**:
  - The POST method is used to send data to a server to create or update resources. It sends data in the request body and is used for actions that modify server data.

From Browser to Server:
- GET / HTTP/2
- Host: www.harvard.edu
- ...

Response from the Server
- HTTP/2 200 - acknowledgement of the version used / a Status code
- Content-Type: text/html
- ...

### 3.1 Developer Tools / Status codes
- Network Tab
  - Diagnostic information specific to the web
  - https://www.harvard.edu/
    - 200 - OK
  - https://harvard.edu/
    - 301 - Moved Permanently
  - https://www.harvard.edu/cats
    - 404 - File Not Found

## 4. HTML
```html
<!DOCTYPE html>

<html lan="en">
    <head>
        <title>
            hello, title
        </title>
    </head>
    <body>
        hello, body
    </body>
</html>
```
- `<!DOCTYPE html>`
  - Signales the HTML version used
- `<html lang="en">`
  - This **Tag** signals that the beginning of the htmp page
  - Everything after the **Tag** is an **Attribute**, here lang="en" (Key Value Pair)
- `</html>`
  - This is the closing/end **Tag** signals that the html page is finished
- `<head> </head>`
  - Head element, the very top of it
- `<title> </title>`
  - Simple text 
- `<body> </body>`
  - Body element, the body of the page


There a basically two concepts:
- **tags**
  - An HTML tag is a code element used to define and structure content on a webpage. Tags are enclosed in angle brackets (e.g., `<h1>` for a heading or `<p>` for a paragraph) and usually come in pairs: an opening tag and a closing tag (e.g., `<p>Content</p>`).
- **attributes**
  - An HTML attribute is a modifier for an HTML tag, providing additional information about an element. Attributes are written inside the opening tag and usually consist of a name and value pair (e.g., `class="header"` or `href="https://example.com"`).


### 4.1 Tags

- `<head></head>`
  - Head 
- `<body></body>`
  - body
- `<p></p>`
  - paragraph
- `<ul></ul>` / `<ol></ol>`
  - unlisted - ordered list
- `<li></li>`
  - list element
- `<table></table>`
  - table
- `<tr></tr>`
  - table row
  - `<td></td>`
    -  table data (cell)
- `<img alt="test textfor test image" src="test.jpg">`
  - image
- `<video controls muted><source src="video.mp4" type="video/mp5"></video>`
  - video
- `<a href"www.google.com">google hyperlink</a>`
  - hyperlink
- `<meta name="viewport" content="initial-scale=1, width=device-width">`
  - placed in the head.
  - useful to automatically scale to your device screen size
  - meta can also be used to show a preview when coping the link into e.g. a facebook post
- `<form action="www.google.com" method=get></form>`
  - start of a form e.g. searchbar
  `<input>`
    - basically the searchbar takes input
    - attributes:
      - autocomplete="off"
      - autofocus
      - name="q"
      - placeholder="Query"
      - type="search"
  - `<button>test</button>`
    - button

# 5. regular expressions (regexes)

- Avaiable in most modern programming languages
- A way to use pattern to validate inputs
- Or extract information from strings
---
```html
<input autocomplete="off" autofocus name="email" pattern=".+@+\.edu" placeholder="Email" type="email">
```
- Here the pattern is used to set a regexes with some expressions
- The pattern used:
  - . any name for the email
  - +@ at least one @ in the email
  - + \\.edu should contain the dot edu as well. the backslash dot = to a string dot
- A short cheat sheet:
  - . - any single character(except line terminators)
  - \* - zero or more times
  - \+ - one or more times
  - ? - 0 or 1 time
  - {n} - n occurrences
  - {n, m} - at least n occurrences, at most m occurrences
  - ...

## 6. CSS
- **Properties** (attributes)
  - CSS properties define the style rules that control how HTML elements are displayed (e.g., `color`, `font-size`, ``margin``).
- Type selector
  - Targets HTML elements based on their type or tag name (e.g., `p` for paragraphs or `h1` for headings).
- Class selector
  - Targets elements with a specific ``class`` attribute. It is denoted by a dot (``.``) followed by the class name (e.g., ``.button``).
- ID selector
  - Targets a single element with a unique ``id`` attribute. It is denoted by a hash (``#``) followed by the ID name (e.g., ``#header``).
- Attribute seelctor
  - Targets elements based on the presence or value of an attribute. 
  - **Examples**:
    - ``[type="text"]`` selects input fields with ``type="text"``.  
    - ``[href]`` selects all elements with an ``href`` attribute.

## 7. JavaScript
JavaScript is a lightweight, interpreted programming language used to create interactive and dynamic content on web pages (e.g., animations, form validation, API calls).

1. **Variables**
   - Store data values.
     - Example: ``let name = "Alice";``

2. **Data Types**
   - Common types: ``string``, ``number``, ``boolean``, ``object``, ``array``, ``null``, ``undefined``.

3. **Functions**
   - Reusable blocks of code.
     - Example:
        ```js
        function greet() {
            console.log("Hello!");
        }
        greet();
        ```
4. **Conditionals**
   - Control flow based on conditions.
     - Example:
        ```js
        if (age > 18) {
            console.log("Adult");
        } else {
            console.log("Minor");
        }
        ```
5. **Loops**
   - Repeat a block of code.
     - Example:
        ```js
        for (let i = 0; i < 5; i++) {
            console.log(i);
        }
        ```

6. **Events**
   - Respond to user actions like clicks or keypresses.
     - Example:

        ```js
        document.querySelector("button").addEventListener("click", () => {
            alert("Button clicked!");
        });
        ```

7. Objects
   - Store related data and methods.
     - Example:
        ```js
        const car = { brand: "Toyota", model: "Corolla", start: function() { console.log("Starting..."); } };
        car.start();
        ```

8. Arrays
   - Hold collections of data.
     - Example:
        ```js
        const fruits = ["Apple", "Banana", "Cherry"];
        console.log(fruits[0]); // Apple
        ```
        
9. DOM Manipulation
   - Dynamically update HTML elements.
     - Example:
        ```js
        document.getElementById("title").textContent = "New Title";
        ```

10. Promises & Async/Await
    - Handle asynchronous operations.
      - Example:
        ```js
        fetch("https://api.example.com")
            .then(response => response.json())
            .then(data => console.log(data))
            .catch(error => console.error(error));

        // Async/Await
        async function fetchData() {
            try {
                const response = await fetch("https://api.example.com");
                const data = await response.json();
                console.log(data);
            } catch (error) {
                console.error(error);
            }
        }
        ```

11. ES6 Features
    - New syntax and features in modern JavaScript:
      - Arrow functions: ``const add = (a, b) => a + b;``
      - Template literals: ``console.log('Hello, ${name}')``;



