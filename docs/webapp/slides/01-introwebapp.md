## Introduction to Web Applications

---

#### Overview

- Introduction to web applications.
- Key components: web server, application server, and database.
- The role of the HTTP protocol in web communication.

---

#### Components

- In a web application, several components work together:
  - **Web Server**: Serves static content (e.g., HTML, CSS, JavaScript).
  - **Application Server**: Executes dynamic code (e.g., Servlets, JSP).
  - **Database**: Stores and manages data.

---

#### Web Server

- The web server handles static content like HTML and CSS.
- It responds to client requests by serving files from the file system.

- **Example HTML File Served by the Web Server:**
```html []
<!-- Sample HTML File (index.html) -->
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to My Website</title>
</head>
<body>
    <h1>Hello, Web!</h1>
</body>
</html>
```

---

#### Application Server

- The application server processes dynamic content and logic.
- It executes server-side code (e.g., Servlets, JSP) in response to client requests.

- **Example Servlet Handling a Request:**
```java []
@WebServlet("/greet")
public class GreetingServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String message = "Hello, Web!";
        response.getWriter().write(message);
    }
}
```

---

#### Database

- Databases store and manage data for web applications.
- Application servers connect to databases to fetch and store information.

- **Example SQL Query to Retrieve User Information:**
```sql []
SELECT username, email FROM users WHERE user_id = 123;
```