#### Managing Dependencies and Repositories

**Key Points:**
- Project dependencies in Maven.
- Transitive dependencies and their significance.
- Maven repositories for managing dependencies.
- Custom repositories and their use.
- Understanding dependency scopes and their role.

---

#### Project Dependencies

- **Dependencies** in Maven are external libraries or modules that your project relies on.
- You declare dependencies in your project's POM file.
- Maven will download and manage these dependencies for you.

**Example Dependency Declaration:**

```xml []
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.8</version>
    </dependency>
</dependencies>
```

---

#### Group ID, Artifact ID, and Version

- **Group ID:** 
  - Organizes artifacts into logical groups.
  - Helps prevent naming conflicts.
  - Often follows reverse domain name notation (e.g., `com.example`).
- **Artifact ID:**
  - Represents the name of the artifact.
  - Used to identify the project/module.
  - Should be unique within the group.
- **Version:**
  - Specifies the version of the artifact.
  - Enables consistent management of dependencies.
  - Allows for updates and compatibility control.
- Together, these coordinates uniquely identify an artifact.


---

#### Transitive Dependencies

- Maven automatically resolves and includes **transitive dependencies**.
- Transitive dependencies are dependencies of your project's dependencies.
- This simplifies dependency management but can lead to version conflicts.

**Example:** Suppose your project depends on `A`, which in turn depends on `B`. Maven will manage `B` as a transitive dependency.

---

#### Maven Repositories

- **Maven Repositories** are locations where Maven stores and retrieves project artifacts (e.g., JAR files).
- The **Central Repository** is the default remote repository for Maven.
- You can also define custom repositories for your project.

**Central Repository:** Maven's default repository for common libraries.

---

#### Custom Repositories

- You can define **custom repositories** in your POM or settings.xml.
- Custom repositories are useful for hosting internal libraries or third-party repositories.

**Example: Custom Repository Definition**

```xml []
<repositories>
    <repository>
        <id>my-repo</id>
        <url>https://example.com/maven-repo/</url>
    </repository>
</repositories>
```

---

#### Dependency Scopes

- **Dependency Scopes** determine when dependencies are available during the build lifecycle.
- Common scopes include `compile`, `test`, `runtime`, and `provided`.

**Example: Dependency Scope**

```xml []
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>my-library</artifactId>
        <version>1.0.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
```

---

#### Dependency Scope Examples

- **Compile Scope:** The default scope. Dependencies are available for the whole build lifecycle.
- **Test Scope:** Dependencies are only available during testing.
- **Runtime Scope:** Dependencies are available during runtime, but not for compiling.
- **Provided Scope:** Dependencies are provided by the runtime environment (e.g., servlet container).

---

#### Dependency Management

- **Dependency Management** allows you to declare a version for a dependency in a parent POM.
- Child projects can then inherit this version without specifying it.

**Example: Dependency Management in Parent POM**

```xml []
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.example</groupId>
            <artifactId>common-library</artifactId>
            <version>2.0.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

---

#### Dependency Scopes

- **Dependency Scopes Overview:**
  - Dependency scopes define the visibility and lifecycle of a dependency in your project.
  - Maven provides several predefined scopes to control when and how dependencies are used.

---

#### Compile Scope

- **Compile Scope:**
  - The default scope for dependencies.
  - Dependencies with this scope are available during compile and runtime.
  - They are included in the final artifact.

**Example:**
```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>library</artifactId>
    <version>1.0</version>
    <scope>compile</scope>
</dependency>
```

---

#### Provided Scope

- **Provided Scope:**
  - Dependencies with this scope are available during compile time.
  - They are expected to be provided by the runtime environment (e.g., servlet containers).
  - They are not included in the final artifact.

**Example:**
```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>servlet-api</artifactId>
    <version>3.1</version>
    <scope>provided</scope>
</dependency>
```

---

#### Runtime Scope

- **Runtime Scope:**
  - Dependencies with this scope are not needed for compilation.
  - They are required at runtime.
  - They are included in the final artifact.

**Example:**
```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>5.5.2.Final</version>
    <scope>runtime</scope>
</dependency>
```

---

#### Test Scope

- **Test Scope:**
  - Dependencies with this scope are used only for testing purposes.
  - They are not included in the final artifact.
  - Useful for testing frameworks and tools.

**Example:**
```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13</version>
    <scope>test</scope>
</dependency>
```

---

#### Dependency Exclusions

- **Managing Dependency Exclusions:**
  - Exclusions allow you to exclude specific transitive dependencies of a dependency.
  - Useful when you want to prevent conflicts or unnecessary dependencies.

**Example:**
```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0</version>
    <exclusions>
        <exclusion>
            <groupId>com.somegroup</groupId>
            <artifactId>undesired-artifact</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

---

#### Transitive Dependencies

- **Transitive Dependencies:**
  - Transitive dependencies are dependencies required by other dependencies.
  - Maven automatically resolves and manages transitive dependencies.
  - It simplifies dependency management but can lead to version conflicts.

**Example:**
  - If you include `A` as a direct dependency, which relies on `B` and `C`, Maven will transitively manage `B` and `C`.

---

#### Dependency Management

- **Dependency Management Section:**
  - The `<dependencyManagement>` section allows you to centralize the management of dependency versions.
  - This is particularly useful for multi-module projects.

**Example:**
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.example</groupId>
            <artifactId>common-lib</artifactId>
            <version>2.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

---

#### Importing Dependencies

- **Importing Dependency Management:**
  - Child POMs can import the `<dependencyManagement>` section to inherit dependency versions.
  - This simplifies version consistency across modules.

**Example:**
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.example</groupId>
            <artifactId>common-lib</artifactId>
            <version>2.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```