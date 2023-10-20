## Servlets

---

#### Introduction to Servlets

- **What are Servlets?**
  - Servlets are Java classes used for extending the capabilities of web servers.
  - They handle requests and generate dynamic responses.

---

#### The Servlet Life Cycle

- **Servlet Life Cycle**
  - Initialization: Servlet is loaded and initialized.
  - Service: Handles client requests (e.g., doGet, doPost).
  - Destruction: Servlet is removed from memory.

---

#### Configuring Servlets

- **Configuring Servlets**
  - Servlets are typically configured in the `web.xml` file.
  - Servlet mapping defines URLs to servlet classes.

```xml []
<servlet>
    <servlet-name>HelloServlet</servlet-name>
    <servlet-class>com.example.HelloServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>HelloServlet</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

---

#### Handling HTTP Methods

- **Handling HTTP Methods**
  - Servlets can handle different HTTP methods (GET, POST, etc.).
  - The `doGet` and `doPost` methods process requests.

```java []
@WebServlet("/greet")
public class GreetingServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        // Handle GET request
    }
    
    protected void doPost(HttpServletRequest request, HttpServletResponse response) {
        // Handle POST request
    }
}
```

---

#### Servlet Response

- **Servlet Response**
  - Servlets generate dynamic responses.
  - Use the `HttpServletResponse` object to send data to the client.

```java []
response.setContentType("text/html");
PrintWriter out = response.getWriter();
out.println("<html><body>Hello, Web!</body></html>");
```

---

#### Redirecting Requests

- **Redirecting Requests**
  - Servlets can redirect requests to other resources.
  - Useful for forwarding requests or sending users to another URL.

```java []
response.sendRedirect("/new-page");
```

---

#### Key HTTP Headers and Their Purposes

- **HTTP Headers** are important components of an HTTP request or response. They provide metadata and instructions to browsers and servers.

---

#### Common HTTP Headers

- **Host**:
  - Purpose: Specifies the domain name of the server (used for virtual hosting).
  - Example: `Host: www.example.com`
- **User-Agent**:
  - Purpose: Identifies the user's browser and device.
  - Example: `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36`

---


- **Content-Type**:
  - Purpose: Defines the type of data in the response (e.g., HTML, JSON, XML).
  - Example: `Content-Type: text/html; charset=UTF-8`

- **Content-Length**:
  - Purpose: Specifies the length of the response body in bytes.
  - Example: `Content-Length: 1024`

---

- **Location**:
  - Purpose: Used in redirection responses to indicate the new location.
  - Example: `Location: https://www.example.com/new-page`

- **Authorization**:
  - Purpose: Contains credentials for accessing a resource.
  - Example: `Authorization: Basic YWxhZGRpbjpvcGVuc2VzYW1l`

---

HTTP headers convey vital information and instructions between clients and servers, facilitating the exchange of data and resources.

---

#### HttpServletRequest Methods

- **HttpServletRequest** is an important class for handling HTTP requests in Java servlets. It provides access to various request information.

---

#### Key Methods of HttpServletRequest

- **getRequestURL()**:
  - Returns the URL of the request, including the protocol, server name, port, and URI.

- **getParameter(String name)**:
  - Retrieves the value of a request parameter by name.

- **getMethod()**:
  - Returns the HTTP method used for the request (e.g., GET, POST).

---

- **getSession(boolean create)**:
  - Retrieves the current session or creates a new one if it doesn't exist.

- **getAttribute(String name)**:
  - Retrieves an attribute stored in the request.

- **getHeader(String name)**:
  - Returns the value of an HTTP header from the request.

---

- **getInputStream()**:
  - Gets the input stream for reading the request body.

- **getReader()**:
  - Gets a buffered reader for reading the request body as character data.

- **getRemoteAddr()**:
  - Returns the IP address of the client making the request.

---

#### HttpServletResponse Methods

- **HttpServletResponse** is a crucial class for handling HTTP responses in Java servlets. It provides control over the response to be sent to the client.

---

#### Key Methods of HttpServletResponse

- **setContentType(String type)**:
  - Sets the content type of the response (e.g., "text/html" or "application/json").

- **getWriter()**:
  - Returns a `PrintWriter` for sending character text to the client.

- **getOutputStream()**:
  - Returns an `OutputStream` for sending binary data to the client.

---

- **setStatus(int sc)**:
  - Sets the status code for the response (e.g., 200 for success, 404 for not found).

- **sendRedirect(String location)**:
  - Redirects the client to a different URL.

- **addHeader(String name, String value)**:
  - Adds an HTTP header to the response.

---

- **setHeader(String name, String value)**:
  - Sets an HTTP header, overwriting any previous value.

- **sendError(int sc, String msg)**:
  - Sends an error response with the specified status code and message.

- **setCharacterEncoding(String charset)**:
  - Sets the character encoding of the response.

---

#### Content Type and MIME Type

- **Content Type** specifies the type of data in an HTTP response, ensuring the client interprets it correctly.

- **MIME Type (Multipurpose Internet Mail Extensions)** is a standard used to define types of data on the Internet.

---

#### Key Content Types/MIME Types

- **text/html (MIME Type: text/html)**:
  - Used for HTML web pages.
  - Example: `<html><body><h1>Hello, World!</h1></body></html>`

- **application/json (MIME Type: application/json)**:
  - Used for sending structured data in JSON format.
  - Example: `{ "name": "John", "age": 30 }`

---

- **application/xml (MIME Type: application/xml)**:
  - Used for XML data.
  - Example: `<person><name>John</name><age>30</age></person>`


- **text/plain (MIME Type: text/plain)**:
  - Used for plain text.
  - Example: "Hello, World!"

- **image/jpeg (MIME Type: image/jpeg)**:
  - Used for JPEG images.
  - Example: (Image data)

---

- **application/pdf (MIME Type: application/pdf)**:
  - Used for PDF documents.
  - Example: (PDF data)

- **audio/mpeg (MIME Type: audio/mpeg)**:
  - Used for MP3 audio files.
  - Example: (Audio data)

---

By specifying the correct Content Type and associated MIME Type, you ensure proper data interpretation by the client.

---

#### HTTP Status Codes

- **HTTP Status Codes** are three-digit numbers returned by a server to indicate the outcome of a client's request. They provide information about the status of the request and response.

---

#### Key HTTP Status Codes

- **200 OK**:
  - Purpose: Request was successful.
  - Example: `HTTP/1.1 200 OK`
- **301 Moved Permanently**:
  - Purpose: Resource has been permanently moved to a new URL.
  - Example: `HTTP/1.1 301 Moved Permanently`
- **400 Bad Request**:
  - Purpose: The request is malformed or invalid.
  - Example: `HTTP/1.1 400 Bad Request`

---

- **404 Not Found**:
  - Purpose: The requested resource does not exist.
  - Example: `HTTP/1.1 404 Not Found`
- **500 Internal Server Error**:
  - Purpose: The server encountered an error while processing the request.
  - Example: `HTTP/1.1 500 Internal Server Error`
- **503 Service Unavailable**:
  - Purpose: The server is temporarily unable to handle the request.
  - Example: `HTTP/1.1 503 Service Unavailable`

---

#### Generating Dynamic Images with HttpServlet

- **Dynamic images** can be generated on-the-fly in Java web applications using HttpServlet.

---

#### Code Example: Dynamic Image Servlet

```java []
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.Color;
import java.awt.Graphics;
import java.awt.image.BufferedImage;
import java.io.IOException;

public class DynamicImageServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        // Set content type to image
        response.setContentType("image/jpeg");

        // Create a blank image
        int width = 300;
        int height = 200;
        BufferedImage image = new BufferedImage(width, height, BufferedImage.TYPE_INT_RGB);

        // Get graphics context
        Graphics g = image.getGraphics();

        // Fill the background
        g.setColor(Color.WHITE);
        g.fillRect(0, 0, width, height);

        // Draw custom content
        g.setColor(Color.RED);
        g.drawString("Dynamic Image", 100, 100);

        // Write the image to the response
        javax.imageio.ImageIO.write(image, "jpeg", response.getOutputStream());
    }
}
```