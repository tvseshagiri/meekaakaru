#### Plugins and Build Lifecycle

**Key Points:**
- Understanding Maven plugins and their role.
- Common Maven plugins for various tasks.
- Configuring plugins in the POM.
- Understanding the build lifecycle and its phases.

---

#### Introduction to Plugins

- **Maven Plugins** are extensions that provide specific build-related functionality.
- Plugins enable Maven to perform various tasks, such as compiling, testing, packaging, and more.
- Each plugin consists of **goals**, which represent specific tasks.

---

#### Commonly Used Plugins

1. **Compiler Plugin:**
   - Compiles project source code.
   - Supports various Java versions.

2. **Surefire Plugin (for Testing):**
   - Executes unit tests.
   - Generates test reports.

3. **JAR Plugin:**
   - Creates JAR (Java Archive) files.

4. **WAR Plugin:**
   - Creates WAR (Web Archive) files for web applications.

---

#### Configuring Plugins in the POM

- You can configure plugins in your project's POM by specifying their settings.

**Example: Configuration of Compiler Plugin**

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.0</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

---

#### Introduction to Build Lifecycle

- The **build lifecycle** is a sequence of phases that define the build process.
- Maven defines several standard phases in its build lifecycle, including:
  - `validate`, `compile`, `test`, `package`, `install`, and `deploy`.

- Each phase corresponds to a specific step in the build process.

---

#### Build Phases

- The **build phases** are the individual steps within the build lifecycle.
- Example phases:
  - `validate`: Validate the project.
  - `compile`: Compile the source code.
  - `test`: Run unit tests.
  - `package`: Package the project (e.g., create JAR or WAR).
  - `install`: Install the project in the local repository.
  - `deploy`: Deploy the project to a remote repository.

---

#### Default Lifecycle and Goals

- The **default lifecycle** represents the standard sequence of build phases.
- Maven binds specific goals to each phase by default.

**Example:** When you run `mvn compile`, Maven executes the `compile` phase and associated goals.

---

#### Binding Custom Goals

- You can bind custom goals to specific phases in the build lifecycle.

**Example:** Binding a custom goal to the `package` phase:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-antrun-plugin</artifactId>
            <version>3.0.0</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>run</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

---

#### Let's create a sample Maven project for this purpose:

--- 

#### Step 1: Create a New Maven Project

First, create a new directory for your project and navigate to it in your terminal:

```shell
mkdir MyUberJarProject
cd MyUberJarProject
```

#### Step 2: Initialize a Maven Project

Initialize a new Maven project using the `maven-archetype-quickstart` archetype:

```shell
mvn archetype:generate -DgroupId=com.example.myuberjar -DartifactId=my-uber-jar-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This command generates a basic Maven project structure with a sample Java application.

#### Step 3: Add Dependencies

In your `pom.xml`, add dependencies to your Java application. For example, let's add a popular logging library, Log4j:

```xml
<dependencies>
    <!-- ... other dependencies ... -->
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>2.14.1</version>
    </dependency>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>2.14.1</version>
    </dependency>
</dependencies>
```

#### Step 4: Create a Simple Java Application

Create a simple Java application in the `src/main/java/com/example/myuberjar` directory. Here's a basic example:

```java
package com.example.myuberjar;

import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

public class MyApp {
    private static final Logger logger = LogManager.getLogger(MyApp.class);

    public static void main(String[] args) {
        logger.info("Hello from My Uber JAR!");
    }
}
```

#### Step 5: Configure the Maven Shade Plugin

Add the Maven Shade Plugin to your `pom.xml` to create the Uber JAR. This plugin will bundle your application code and all its dependencies into a single JAR file.

```xml
<build>
    <plugins>
        <!-- ... other plugins ... -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.2.4</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <transformers>
                            <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass>com.example.myuberjar.MyApp</mainClass>
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

#### Step 6: Build the Uber JAR

Build your Uber JAR by running the following command:

```shell
mvn clean package
```

This will create a JAR file with all dependencies bundled into it in the `target` directory. You can run it with:

```shell
java -jar target/my-uber-jar-app-1.0-SNAPSHOT.jar
```

