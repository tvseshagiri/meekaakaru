## Sample SpringBoot Application

#### Folder structure 

```plaintext
spring-boot-app/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   ├── com/
│   │   │   │   ├── example/
│   │   │   │   │   ├── springbootapp/
│   │   │   │   │   │   ├── Application.java
│   │   │   │   │   │   ├── controller/
│   │   │   │   │   │   │   ├── HelloController.java
│   │   │   │   │   │   ├── model/
│   │   │   │   │   │   │   ├── User.java
│   ├── test/
│   │   ├── java/
│   │   │   ├── com/
│   │   │   │   ├── example/
│   │   │   │   │   ├── springbootapp/
│   │   │   │   │   │   ├── controller/
│   │   │   │   │   │   │   ├── HelloControllerUnitTest.java
│   │   │   │   │   │   │   ├── HelloControllerIntegrationTest.java
│   │   │   │   │   │   ├── HelloControllerSeleniumTest.java
│   ├── resources/
│   │   ├── static/
│   │   ├── templates/
│   ├── application.properties
├── pom.xml
```

---

The project structure includes the following directories:

- `src/main/java`: Contains your main application code.
  - `com.example.springbootapp`: Your main package.
    - `Application.java`: The main Spring Boot application class.
    - `controller`: Controller classes.
      - `HelloController.java`: The controller with a simple REST endpoint.
    - `model`: Model classes.
      - `User.java`: A simple model class.

---

- `src/test/java`: Contains your test classes.
  - `com.example.springbootapp`: The test package.
    - `controller`: Test classes for the controller.
      - `HelloControllerUnitTest.java`: Unit test for the `HelloController`.
    - `HelloControllerIntegrationTest.java`: Integration test for the entire Spring Boot application.
    - `HelloControllerSeleniumTest.java`: Functional test using Selenium.

---

- `src/resources`: Contains application properties and static resources.
  - `application.properties`: Spring Boot application properties (you can configure your server port, datasource, etc., here).
  - `static`: Directory for static resources.
  - `templates`: Directory for templates (if using Thymeleaf or other template engines).

- `pom.xml`: Maven project configuration file.


---

**Spring Boot Application Code**

**HelloController.java** - A simple controller with a REST endpoint.

```java
package com.example.springbootapp.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/hello")
public class HelloController {

    @GetMapping
    public String sayHello() {
        return "Hello, World!";
    }
}
```

---

**Application.java** - The main Spring Boot application class.

```java
package com.example.springbootapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

---

**Unit Test**

**HelloControllerUnitTest.java** - Unit test class using JUnit for testing the `HelloController`.

```java
package com.example.springbootapp.controller;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

@SpringBootTest
@AutoConfigureMockMvc
public class HelloControllerUnitTest {

    private MockMvc mockMvc;

    @BeforeEach
    public void setUp(HelloController helloController) {
        this.mockMvc = MockMvcBuilders.standaloneSetup(helloController).build();
    }

    @Test
    public void testSayHello() throws Exception {
        mockMvc.perform(MockMvcRequestBuilders.get("/hello"))
                .andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.content().string("Hello, World!"));
    }
}
```

---

**Integration Test**

**HelloControllerIntegrationTest.java** - Integration test class for testing the entire Spring Boot application.

```java
package com.example.springbootapp;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.web.server.LocalServerPort;
import org.springframework.boot.test.web.client.TestRestTemplate;

import static org.junit.jupiter.api.Assertions.assertEquals;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class HelloControllerIntegrationTest {

    @LocalServerPort
    private int port;

    private TestRestTemplate restTemplate;

    @BeforeEach
    public void setUp() {
        restTemplate = new TestRestTemplate();
    }

    @Test
    public void testSayHello() {
        String url = "http://localhost:" + port + "/hello";
        String response = restTemplate.getForObject(url, String.class);
        assertEquals("Hello, World!", response);
    }
}
```

---

**Functional Test**

**HelloControllerSeleniumTest.java** - Functional test class for Selenium-based functional testing.

```java
package com.example.springbootapp;

import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.Test;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

import static org.junit.jupiter.api.Assertions.assertTrue;

public class HelloControllerSeleniumTest {

    private static WebDriver driver;

    @BeforeAll
    public static void setUp() {
        System.setProperty("webdriver.chrome.driver", "path/to/chromedriver.exe");
        driver = new ChromeDriver();
    }

    @Test
    public void testSayHello() {
        driver.get("http://localhost:8080/hello");
        String pageSource = driver.getPageSource();
        assertTrue(pageSource.contains("Hello, World!"));
    }
}
```

---

**pom.xml Configuration**

Here's the `pom.xml` file with configurations for the Maven plugins required for testing:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.6.1</version> <!-- Update to the latest Spring Boot version -->
    </parent>

    <dependencies>
        <!-- Spring Boot Starter -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
        <!-- Spring Boot Starter Test (for unit and integration tests) -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!-- Selenium WebDriver (for functional tests) -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>3.141.59</version>
            <scope>test</scope>
        </dependency>
    </dependencies>



    <build>
        <plugins>
            <!-- Maven Surefire Plugin for running unit tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M5</version>
            </plugin>
            <!-- Maven Failsafe Plugin for running integration and functional tests -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-failsafe-plugin</artifactId>
                <version>3.0.0-M5</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>integration-test</goal>
                            <goal>verify</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <!-- Maven Spring Boot Plugin for building Spring Boot applications -->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

---

1. **Unit Tests** (JUnit tests):

   ```bash
   mvn test
   ```
   This command will run all the unit tests in your project.
2. **Integration Tests**:
   Integration tests are typically run as part of the `verify` phase. You can use the following command to run integration tests:
   ```bash
   mvn verify
   ```
   This command will execute both integration tests and functional tests defined using the Failsafe plugin.
3. **Functional Tests** (Selenium-based functional tests):
   Selenium-based functional tests are executed using the Failsafe plugin in the `verify` phase, as mentioned above.
