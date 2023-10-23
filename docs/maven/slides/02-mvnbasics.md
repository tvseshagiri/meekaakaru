#### Maven Basics

**Key Points:**
- Understanding the Project Object Model (POM).
- Standard directory structure.
- Creating a Maven project.
- Building and packaging with Maven.
- Common Maven commands and goals.

---

#### Project Object Model (POM)

- The **Project Object Model (POM)** is an XML file that contains project configuration information.
- Key elements in the POM include **groupId**, **artifactId**, and **version**.
- The POM defines project dependencies, plugins, and goals.

**Example POM:**

```xml []
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>my-app</artifactId>
  <version>1.0-SNAPSHOT</version>
</project>
```

---

#### Directory Structure

- Maven enforces a **standard directory structure** for projects.
- This structure helps organize project source code, resources, and other files.

**Standard Directory Structure:**

- `src/main/java`: Java source code.
- `src/main/resources`: Non-code resources (e.g., configuration files).
- `src/test/java`: Unit test source code.
- `src/test/resources`: Test resources.

---

#### Creating a Maven Project

- Use the `mvn archetype:generate` command to create a new Maven project from an archetype (template).
- Select an archetype based on your project type (e.g., Java application, web application).

```bash []
mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

---

#### Building and Packaging

- Maven automates the **build process**, which includes:
  - Compiling source code.
  - Running tests.
  - Packaging the project into a deployable unit (e.g., JAR or WAR file).

- Use the `mvn clean install` command to build and package the project.

```bash []
mvn clean install
```

- The packaged artifact is usually stored in the `target` directory.

---

#### Common Maven Commands

- `mvn clean`: Cleans the project by removing generated files.
- `mvn compile`: Compiles source code.
- `mvn test`: Runs tests.
- `mvn package`: Packages the project.
- `mvn install`: Installs the project artifact in the local repository.
- `mvn deploy`: Deploys the artifact to a remote repository.

---

#### Additional Important Topics

**Maven Goals:**
- Maven goals are specific tasks you can run using the `mvn` command.
- Common goals include `clean`, `compile`, `test`, `package`, and more.

**Profiles:**
- Maven profiles allow you to customize builds for different environments or conditions.
- Profiles can be activated based on specific criteria, such as properties or file existence.

