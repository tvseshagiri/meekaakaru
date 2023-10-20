
## JavaServer Pages Standard Tag Library (JSTL)

---

#### Introduction to JSTL

- **JavaServer Pages Standard Tag Library (JSTL)** is a set of tags and functions that simplify the development of JSP pages.

---

#### Key Features of JSTL

- **Core Tags**:
  - Provides tags for flow control, looping, conditionals, and more.

- **Formatting Tags**:
  - Offers tags for date, number, and message formatting.

- **SQL Tags**:
  - Allows database operations without writing Java code.

---

- **XML Tags**:
  - Enables XML processing and manipulation.

- **Custom Tags**:
  - Supports the creation of custom tags and tag libraries.

---

#### Core Tags: `<c:forEach>`

- **`<c:forEach>`**:
  - Used for looping and iterating over collections.

- Example:

  ```jsp []
  <c:forEach items="${userList}" var="user">
      <p>${user.name}</p>
  </c:forEach>
  ```

- This code iterates through the `userList` and displays each user's name.

---

#### Core Tags: `<c:if>`

- **`<c:if>`**:
  - Used for conditional execution of code.

- Example:

  ```jsp []
  <c:if test="${user.age > 18}">
      <p>This user is an adult.</p>
  </c:if>
  ```

- The code inside the `<c:if>` tag executes only if the condition is true.

---

#### Formatting Tags: `<fmt:formatDate>`

- **`<fmt:formatDate>`**:
  - Used for formatting dates.

- Example:

  ```jsp []
  <fmt:formatDate value="${user.birthDate}" pattern="yyyy-MM-dd" var="formattedDate" />
  <p>Date of Birth: ${formattedDate}</p>
  ```

- The tag formats the date and stores it in the `formattedDate` variable.

---

#### More JSTL Core Tags

- **JSTL Core Tags** provide additional functionality for JSP development.

---

#### Core Tags: `<c:choose>` and `<c:when>`

- **`<c:choose>` and `<c:when>`**:
  - Used for conditional branching.

- Example:

  ```jsp []
  <c:choose>
      <c:when test="${user.age < 18}">
          <p>This user is a minor.</p>
      </c:when>
      <c:otherwise>
          <p>This user is an adult.</p>
      </c:otherwise>
  </c:choose>
  ```
- The code inside `<c:when>` is executed when the condition is met, or `<c:otherwise>` is executed if none of the conditions are true.

---

#### Core Tags: `<c:set>`

- **`<c:set>`**:
  - Used to set or update variables in JSP.

- Example:

  ```jsp []
  <c:set var="isRegistered" value="true" />
  <p>User is registered: ${isRegistered}</p>
  ```

- The tag sets the variable `isRegistered` to `true`.

---

#### Core Tags: `<c:import>`

- **`<c:import>`**:
  - Used to include content from another URL.

- Example:

  ```jsp []
  <c:import url="http://example.com/external-content.html" />
  ```

- This tag includes content from the specified URL in the JSP page.

---

#### Core Tags: `<c:out>`

- **`<c:out>`**:
  - Used for displaying content, escaping HTML, and formatting.

- Example:

  ```jsp []
  <c:out value="${user.bio}" escapeXml="true" default="No bio available" />
  ```

- The tag displays the user's biography, escapes HTML, and provides a default value.

---

#### Core Tags: `<c:forEach varStatus>`

- **`<c:forEach varStatus>`**:
  - Provides a loop status variable.

- Example:

  ```jsp []
  <c:forEach items="${items}" var="item" varStatus="loop">
      Item ${loop.index}: ${item}
  </c:forEach>
  ```

- The loop status variable `loop` contains index and count information.

---

#### More JSTL Formatting Tags

- **JSTL Formatting Tags** provide additional functionality for formatting data in JSP.

---

#### Formatting Tags: `<fmt:setLocale>`

- **`<fmt:setLocale>`**:
  - Used to set the locale for date, number, and currency formatting.

- Example:

  ```jsp []
  <fmt:setLocale value="en_US" />
  ```

- This tag sets the locale to US English for formatting.

---

#### Formatting Tags: `<fmt:parseNumber>`

- **`<fmt:parseNumber>`**:
  - Used for parsing numbers.

- Example:

  ```jsp []
  <fmt:parseNumber value="1234.56" var="parsedNumber" />
  <p>Parsed Number: ${parsedNumber}</p>
  ```

- The tag parses the number and stores it in the `parsedNumber` variable.

---

#### Formatting Tags: `<fmt:message>`

- **`<fmt:message>`**:
  - Used for displaying localized messages.

- Example:

  ```jsp []
  <fmt:setBundle basename="Messages" />
  <p><fmt:message key="welcome.message" /></p>
  ```

- This tag displays a message retrieved from the `Messages` resource bundle.

---

#### Formatting Tags: `<fmt:formatNumber>`

- **`<fmt:formatNumber>`**:
  - Used for formatting numbers.

- Example:

  ```jsp []
  <fmt:formatNumber value="1234.5678" pattern="#,##0.00" var="formattedNumber" />
  <p>Formatted Number: ${formattedNumber}</p>
  ```

- The tag formats the number according to the specified pattern.

---

#### Formatting Tags: `<fmt:formatDate>` (Advanced)

- **`<fmt:formatDate>`** (Advanced):
  - Used for formatting dates with optional styles and time zones.

- Example:

  ```jsp []
  <fmt:formatDate value="${user.birthDate}" pattern="yyyy-MM-dd" var="formattedDate" type="both" timeZone="America/New_York" />
  <p>Date of Birth: ${formattedDate}</p>
  ```

- This tag provides advanced date formatting options.

---

#### Creating a Custom Tag Library (TagLib)

- **Creating a Custom Tag Library (TagLib)** allows you to define your own custom tags for use in JSP.

---

#### Steps to Create a Custom Tag Library

1. **Create Tag Handler Classes**: Define Java classes that implement the tag behavior.

2. **Create a Tag Library Descriptor (TLD) File**: Describe the tags and their implementations in XML format.

3. **Deploy the Tag Library**: Place the TLD file in the WEB-INF directory and add it to the web.xml file.

4. **Use Custom Tags in JSP**: Include the custom tag library declaration in JSP and use the custom tags.

---

#### Example: Creating a Custom Tag for Greeting

- **Tag Handler Class** (`GreetTagHandler.java`):

  ```java []
  package customtags;

  import javax.servlet.jsp.tagext.TagSupport;
  import javax.servlet.jsp.JspException;
  import java.io.IOException;

  public class GreetTagHandler extends TagSupport {
      public int doStartTag() throws JspException {
          try {
              pageContext.getOut().print("Hello, Custom Tag!");
          } catch (IOException e) {
              throw new JspException(e);
          }
          return SKIP_BODY;
      }
  }
  ```

---

#### Example: Creating a Custom Tag for Greeting (Contd.)

- **Tag Library Descriptor (TLD) File** (`greet.tld`):

  ```xml []
  <taglib>
      <tlib-version>1.0</tlib-version>
      <short-name>greet</short-name>
      <uri>/WEB-INF/greet.tld</uri>
      <tag>
          <name>greet</name>
          <tag-class>customtags.GreetTagHandler</tag-class>
      </tag>
  </taglib>
  ```

- This TLD file describes the custom tag and associates it with the tag handler class.

---

#### Example: Using the Custom Tag in JSP

- **JSP Usage**:

  ```jsp []
  <%@ taglib uri="/WEB-INF/greet.tld" prefix="greet" %>
  <!DOCTYPE html>
  <html>
  <body>
      <greet:greet />
  </body>
  </html>
  ```

- In this JSP, we declare the custom tag library and use the `<greet:greet />` tag to display the greeting message.
