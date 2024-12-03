# Flask

- **Notes:** https://cs50.harvard.edu/x/2024/notes/9/

- Web Applications
  - Applications take input and give an output

- Flask is a mini framework and with the command line you can start your website
  - flask run 


 How does a folder for a flask website look:
 - app.py
 - requirements.txt
   - libraries
 - static/
   - css/images
 - templates/
   - html


## 1. First example
- app.py
    ```py
    from flask import Flask, render_template, request

    app = Flask(__name__)


    @app.route("/")
    def index():
        return render_template("index.html")
    ```
- index.html
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>hello</title>
    </head>
    <body>
            <p>Hello, world</p>
    </body>
    </html>
    ```

# 2. request.args

- {{ variable }}
  - this makes the html a **template** in which you can use variables and some code
- **app.py**
    ```py
    from flask import Flask, render_template, request

    app = Flask(__name__)

    @app.route("/")
    def index():
        name = request.args["name"]
        return render_template("index.html", placeholder=name)
    ```
- **index.html**
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>hello</title>
    </head>
    <body>
            <p>Hello, {{ placeholder }}</p>
    </body>
    </html>
    ```

For the placeholder to be replaced, the end of the website url need to be changed:
- /?name=Eike
- with this the placeholder will be changed to Eike
- without the variable an error will occur
---
- This error can be avoided by using:
    ```py
    @app.route("/")
    def index():
        name = request.args.get("name", "world")
        return render_template("index.html", placeholder=name)
    ```

## 3. Layout.html
A layout.html will work as your main page template. In there you define the part that should be changeable with `{% block body %}{% endblock %}`. Naming convention is: use the name of which tag you want to be changeable!
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>hello</title>
</head>
    <body>
        {% block body %}{% endblock %}
    </body>
</html>
```
Now with this code the other to pages index.html and greet.html have way less lines of code:
- **index.html**
    ```html
    {% extends "layout.html" %}

    {% block body %}

        <form action="/greet" method="get">
            <input autocomplete="off" autofocus name="name" placeholder="Name" type="text">
            <button type="submit">Greet</button>
        </form>

    {% endblock %}
    ```

- **greet.html**
    ```
    {% extends "layout.html" %}

    {% block body %}

        hello, {{ name }}

    {% endblock %}
    ```
This will be very helpful if you have multiple pages all using the same header and footer. You can then easily change the deatils for the header or footer in just one file and it changes on every page!

## 4. GET and POST

### GET Method
- **Purpose:** Used for retrieving data from the server without causing any side effects. It is generally used for search forms or when data retrieval doesn't modify server data.
- **How it works:** The data entered in the form is appended to the URL as query parameters.
  - Example: Submitting a form might produce a URL like: <br> `https://example.com/submit?name=John&age=25`
- **Python:** 
  - The code to get the value through the GET method uses:
    - `request.args.get()`
- **Characteristics:**
  1. Data is visible in the URL.
  2. Limited data size due to URL length restrictions.
  3. Can be bookmarked and shared because the data is part of the URL.
  4. Less secure since data is visible in the browser and logs.

---

### POST Method
- **Purpose:** Used for sending data to the server that can result in changes (e.g., submitting a form to create, update, or delete a resource).
- **How it works:** Data is sent in the body of the HTTP request rather than in the URL.
- **Python:** 
  - The code to get the value through the POST method uses:
    - `request.form.get()`
  - While, also at the route must be chaged, as only GET is default.
    - `@app.route("/home", methods=["POST"])`
- **Characteristics:**
  1. Data is not visible in the URL.
  2. More secure than GET, but still not encrypted unless used with HTTPS.
  3. Can handle larger amounts of data.
  4. Cannot be bookmarked or cached as it doesn't use the URL for data transmission.

### Key Differences:
Feature	| GET | POST
--------|-----|-----
Data in URL	| Yes, appended as query parameters	| No, sent in the request body
Security | Less secure, visible in URL |More secure (with HTTPS)
Data Size |Limited by URL length | No size limitation
Use Case | Retrieve data (e.g., search)	| Modify data (e.g., login, signup)

### When to Use:
- **GET:** When you want to retrieve data, allow bookmarking, or need no sensitive data (e.g., search forms).
- **POST:** When sending sensitive data or performing operations that modify the server's state (e.g., login, registration).

## 5. MVC

Model-View-Controller (MVC) is a software design pattern commonly used for developing user 
interfaces and applications that separate the application logic, 
user interface, and data into distinct components. 
This separation makes applications more modular, maintainable, and scalable.

---

### 5.1 Model (M)
- **Role**: Handles the data and business logic of the application.
- **Responsibilities**:
  - Manages the data, database interactions, and any logic related to the application's core functionality.
  - Represents the state of the application.
  - Notifies the View of any data changes.
- **Example in Python**:
  ```py
  class ProductModel:
      def __init__(self):
          self.products = []
      
      def add_product(self, product):
          self.products.append(product)
      
      def get_products(self):
          return self.products
  ```

---

### 5.2 View (V)
- **Role**: Displays data and sends user actions to the controller.
- **Responsibilities**:
  - Handles the visual representation of the data.
  - Updates the user interface when data in the Model changes.
  - Does not contain business logic.
- **Example in HTML**:
  ```html
  <!-- A simple view to display products -->
  <html>
  <body>
      <h1>Product List</h1>
      <ul id="product-list"></ul>
  </body>
  </html>
  ```
- **Dynamic rendering** (using a Python framework like Flask or Django):
  ```py
  from flask import Flask, render_template

  app = Flask(__name__)

  @app.route("/")
  def index():
      products = ["Apples", "Oranges", "Bananas"]
      return render_template("products.html", products=products)
  ```

---

### 5.3 Controller (C)
- **Role**: Acts as an intermediary between the Model and the View.
- **Responsibilities**:
  - Accepts user input from the View.
  - Communicates with the Model to retrieve or update data.
  - Determines which View to display.
- **Example in Python**:
  ```py
  class ProductController:
      def __init__(self, model):
          self.model = model
      
      def add_product(self, product):
          self.model.add_product(product)
      
      def get_products(self):
          return self.model.get_products()
  ```

--- 

### How It All Fits Together
1. **User Interaction**: The user interacts with the View (e.g., clicks a button or submits a form).
2. **Controller Handling**: The Controller processes the user input and determines what to do next (e.g., retrieve data, update the model).
3. **Model Updates**: The Controller updates or retrieves data from the Model.
4. **View Rendering**: The View displays the updated data or user interface.

---

### 5.4 Full Example: simple Flask MVS Application
```py
# Model
class ProductModel:
    def __init__(self):
        self.products = []

    def add_product(self, product):
        self.products.append(product)

    def get_products(self):
        return self.products

# Controller
from flask import Flask, render_template, request, redirect

app = Flask(__name__)
model = ProductModel()

@app.route("/")
def index():
    return render_template("index.html", products=model.get_products())

@app.route("/add", methods=["POST"])
def add_product():
    product_name = request.form["product"]
    model.add_product(product_name)
    return redirect("/")

# View (index.html)
'''
<!DOCTYPE html>
<html>
<body>
    <h1>Product List</h1>
    <form action="/add" method="post">
        <input type="text" name="product" placeholder="Enter product" required>
        <button type="submit">Add</button>
    </form>
    <ul>
        {% for product in products %}
        <li>{{ product }}</li>
        {% endfor %}
    </ul>
</body>
</html>
'''

# Run the Flask app
if __name__ == "__main__":
    app.run(debug=True)
```

---

### Advantages of MVC:
- **Separation of concerns**: Each component has a distinct responsibility.
- **Reusability**: Easy to reuse and test individual components.
- **Scalability**: Simplifies adding new features.
### Disadvantages of MVC:
- **Complexity**: May introduce additional complexity for small applications.
- **Tight coupling**: Controllers can become tightly coupled with Models or Views if not designed properly.



## 6. Cookies and Sessions

Cookies and sessions are mechanisms used in web development to store 
and manage data about a user's interaction with a website.

### 6.1 Cookies

#### 6.1.1 **Definition**:
A cookie is a small piece of data stored on the user's browser by a website. 
It is sent with every HTTP request to the server.

#### 6.1.2 **Key Features**:
- Stored in the browser: Cookies are saved locally on the user's device.
- Used for state management: Since HTTP is stateless, cookies help track user sessions, preferences, and other information across requests.
- Expiration: Cookies can have an expiration date. If not specified, they are considered session cookies and are deleted when the browser closes.
- Accessible via JavaScript: Cookies can be accessed and modified via JavaScript unless marked as `HttpOnly`.

#### 6.1.3 How They Work:
1. **Set by the server**: The server sends a `Set-Cookie` header in an HTTP response.

    ```html
    Set-Cookie: session_id=123abc; HttpOnly; Secure; SameSite=Strict; Expires=Fri, 08 Dec 2024 00:00:00 GMT
    ```

2. **Stored in the browser**: The browser saves the cookie.
3. **Sent with requests**: On subsequent requests to the same domain, 
the browser includes the cookie in the Cookie header.

    ```html
    Cookie: session_id=123abc
    ```

#### 6.1.4 Use Cases:
- User authentication (e.g., storing session tokens)
- Saving user preferences (e.g., language or theme)
- Tracking (e.g., analytics and advertisements)


### 6.2 Sessions

#### 6.2.1 Definition:
A session is a mechanism to store information on the server about a user's 
interaction with a website. Unlike cookies, session data is stored 
server-side, and a unique identifier (session ID) is shared with the client.

#### 6.2.2 Key Features:
- Stored on the server: All user-specific data resides on the server.
- Short-lived: Sessions often expire after a period of inactivity or when the user logs out.
- Linked to a session ID: A cookie (or other means like URL query parameters) contains the session ID.

#### 6.2.3 How They Work:
1. Session initialization:
   - The server creates a session for a user and assigns it a unique ID.
   - This session ID is shared with the client, usually via a cookie (`Set-Cookie`).
2. Client interaction:
   - On subsequent requests, the client sends the session ID in a cookie or other parameter.
3. Server validation:
   - The server retrieves the associated session data using the session ID and processes the request.
4. Session expiration:
   - Sessions can expire due to inactivity or explicit logout.

#### 6.2.4 Use Cases:
- User login and authentication
- Shopping carts for e-commerce
- Storing temporary user data (e.g., a multi-step form)

### 6.3 Comparison: Cookies vs. Sessions

| **Aspect**           | **Cookies**                              | **Sessions**                            |
|-----------------------|------------------------------------------|-----------------------------------------|
| **Storage Location**  | Client-side (browser)                   | Server-side                             |
| **Security**          | Less secure (can be stolen via XSS)     | More secure (data stays on the server)  |
| **Expiration**        | Can be persistent (set expiration time) | Usually short-lived                     |
| **Capacity**          | Limited to ~4KB per cookie              | Larger capacity (server-dependent)      |
| **Usage**             | Tracking, preferences, lightweight data | Sensitive and temporary data            |


### 6.4 Best Practices
Use cookies for non-sensitive client-side data.
Use sessions for sensitive or large data.
Secure cookies with attributes like `HttpOnly`, `Secure`, and `SameSite`.
Use HTTPS to encrypt data in transit.
Implement session timeout to enhance security.


## 7. AJAX
AJAX (Asynchronous JavaScript and XML) is a technique used in web development 
to allow web pages to update dynamically by communicating with the server 
asynchronously. It enables data exchange and updates specific parts of a 
webpage without requiring a full reload.

---

### 7.1 Main Points about AJAX
1. **Asynchronous Communication**:
   - Data is sent and received in the background, allowing the user to continue interacting with the page without interruption.

2. **Uses XMLHttpRequest or Fetch API**:
   - These APIs handle requests to and responses from the server.

3. **Data Formats**:
   - Commonly uses JSON, XML, or plain text for data exchange.

4. **Partial Page Updates**:
   - Allows updating only specific parts of a webpage instead of reloading the entire page.

5. **Improves User Experience**:
   - Provides smoother and faster interactions by reducing server load and eliminating page refreshes.

6. **Supported in Most Modern Browsers**:
   - Widely compatible with browser-side technologies, including JavaScript, HTML, and CSS.

---

### 7.2 Advanced Features and Insights
1. **Modern Alternative: Fetch API**:
   - While `XMLHttpRequest` was the original AJAX tool, the `Fetch` API is more modern and simpler to use. It provides promises for better asynchronous handling.

2. **Cross-Origin Resource Sharing (CORS)**:
   - AJAX requests must comply with the browser's same-origin policy. To communicate with different domains, servers must support CORS.

3. **Error Handling**:
   - AJAX operations can fail due to network issues or server errors. Proper error handling using `.catch()` (for Fetch) or `onerror` (for XMLHttpRequest) is crucial.

4. **AJAX Libraries**:
   - Frameworks like **jQuery** simplify AJAX with easy-to-use methods like `$.ajax()`, `$.get()`, and `$.post()`.

5. **Browser Compatibility**:
   - Most modern browsers support AJAX, but older browsers may have limitations or require polyfills.

6. **Security Concerns**:
   - Be cautious about exposing sensitive data in requests. Use HTTPS and sanitize server-side inputs to prevent attacks like **cross-site scripting (XSS)** or **cross-site request forgery (CSRF)**.

7. **Real-Time Data Updates**:
   - AJAX is often used for real-time applications like live searches, chat applications, and dashboards.

8. **Integration with Frameworks**:
   - Frontend frameworks like React, Angular, and Vue make AJAX easier to manage by integrating it into their component-based architectures.

9. **Can Be Combined with WebSockets**:
   - For true real-time communication (e.g., stock price updates), WebSockets might be a better option. However, AJAX is a good choice for periodic updates.

10. **JSON is the Standard**:
    - While the name includes XML, JSON is the preferred data format due to its simplicity and compatibility with JavaScript.

11. **Performance Optimization**:
    - Overusing AJAX can lead to excessive server calls and higher load. Implement caching and throttle frequent requests to optimize performance.

12. **Debugging Tools**:
    - Modern browsers offer developer tools for debugging AJAX requests (e.g., Chrome DevTools > Network Tab).

13. **Fallback Strategies**:
    - Plan for scenarios where JavaScript or AJAX may fail (e.g., slow networks or disabled JavaScript). Graceful degradation ensures basic functionality still works.

14. **Event Handling**:
    - AJAX responses can be tied to event listeners to trigger additional behavior, like displaying messages or updating UI elements.

---

### 7.3 Best Practices
- Use JSON over XML for simplicity and speed.
- Minimize the size of AJAX responses to reduce load times.
- Always validate and sanitize inputs on the server-side to ensure security.
- Monitor and debug AJAX calls using browser developer tools.
- Use asynchronous frameworks to manage complex workflows (e.g., `async/await` or Promises).


