# EXPERIMENT : INSTALL AND EXPLORE KARATE AND SPRING BOOT TESTING FOR AUTOMATED TESTING

## 1. AIM

To install and explore Karate and Spring Boot testing for automated testing by creating a REST API using Spring Boot and testing the API using the Karate framework.

## 2. SOFTWARE REQUIREMENTS

1. Ubuntu Operating System.
2. Visual Studio Code.
3. Java Development Kit (JDK 17).
4. Apache Maven.
5. Spring Boot.
6. Karate Framework.
7. Web Browser.
8. Internet Connection.

## 3. PROCEDURE

### Step 1: Install Java and Maven

Update the package list:

```
sudo apt update
```

Install Java JDK 17 and Maven:

```
sudo apt install openjdk-17-jdk maven -y
```

Check Java installation:

```
java -version
```

Check Maven installation:

```
mvn -version
```

Expected Output:

Java and Maven version information will be displayed.

### Step 2: Create a Spring Boot Project

1. Open Spring Initializr: [https://start.spring.io/](https://start.spring.io/?utm_source=chatgpt.com)
2. Select the following options:

| Option       | Selection                |
| ------------ | ------------------------ |
| Project      | Maven                    |
| Language     | Java                     |
| Java Version | 17                       |
| Dependencies | Spring Web               |
| Testing      | Spring Boot Starter Test |

3. Click Generate.
4. Download the ZIP file.
5. Extract the ZIP file.
6. Open the extracted project folder in VS Code.

### Step 3: Create a REST API

1. Open the main Java package.
2. Create a new file named `HelloController.java`.
3. Enter the following Java code.

Program: HelloController.java

```
package com.example.demo;

import org.springframework.web.bind.annotation.*;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello from Spring Boot!";
    }
}
```

Explanation:

- `@RestController` – Defines a REST controller.
- `@GetMapping("/hello")` – Handles HTTP GET requests at the `/hello` URL.
- `hello()` – Returns the message "Hello from Spring Boot!".

### Step 4: Run the Spring Boot Application

Open the VS Code terminal and execute:

```
mvn spring-boot:run
```

Wait until the Spring Boot application starts successfully.

Open another terminal and execute:

```
curl http://localhost:8080/hello
```

Expected Output:

```
Hello from Spring Boot!
```

This confirms that the REST API is working successfully.

### Step 5: Add Karate Dependency

Open the `pom.xml` file.

Add the following dependency inside the `dependencies` section:

Karate Dependency:

```
<dependency>
    <groupId>com.intuit.karate</groupId>
    <artifactId>karate-junit5</artifactId>
    <version>1.4.1</version>
    <scope>test</scope>
</dependency>
```

Save the `pom.xml` file.

Explanation:

- `groupId` – Identifies the Karate framework.
- `artifactId` – Specifies the Karate JUnit 5 dependency.
- `version` – Specifies the Karate version.
- `scope` – Specifies that the dependency is used only for testing.

### Step 6: Create a Karate Test

Create the following directory:

```
mkdir -p src/test/java/com/example/demo
```

Inside this directory, create a file named:

`hello.feature`

Enter the following code.

Program: hello.feature

```
Feature: Test Spring Boot API

Scenario: Test Hello API

    Given url 'http://localhost:8080/hello'
    When method GET
    Then status 200
    And match response == 'Hello from Spring Boot!'
```

Explanation:

- `Feature` – Defines the test feature.
- `Scenario` – Defines the test case.
- `Given` – Specifies the API URL.
- `When` – Sends an HTTP GET request.
- `Then` – Checks whether the response status is 200.
- `And` – Verifies the response message.

### Step 7: Create KarateTest.java

Create another file named `KarateTest.java` in the same directory.

Enter the following Java code.

Program: KarateTest.java

```
package com.example.demo;

import com.intuit.karate.junit5.Karate;

class KarateTest {

    @Karate.Test
    Karate testHello() {
        return Karate.run("hello").relativeTo(getClass());
    }
}
```

Explanation:

- `@Karate.Test` – Identifies the Karate test method.
- `Karate.run("hello")` – Executes the `hello.feature` file.
- `relativeTo(getClass())` – Locates the feature file relative to the test class.

### Step 8: Execute Automated Testing

1. Keep the Spring Boot application running in the first terminal.
2. Open another terminal in VS Code.
3. Execute the following command:

```
mvn test
```

4. Maven downloads the required dependencies if necessary.
5. Karate executes the test cases.
6. The API response and test results are displayed.

Expected Output:

```
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

BUILD SUCCESS
```

This indicates that the automated test was executed successfully.

## 4. PROJECT FOLDER STRUCTURE

Your VS Code project should look like this:

```
demo/
│
├── pom.xml
│
└── src/
    │
    ├── main/
    │   └── java/
    │       └── com/
    │           └── example/
    │               └── demo/
    │                   ├── DemoApplication.java
    │                   └── HelloController.java
    │
    └── test/
        └── java/
            └── com/
                └── example/
                    └── demo/
                        ├── KarateTest.java
                        └── hello.feature
```

## 5. EXPECTED OUTPUT

REST API Output:

Browser / Terminal

## Hello from Spring Boot!

[http://localhost:8080/hello](http://localhost:8080/hello?utm_source=chatgpt.com)

Karate Automated Testing Output:

```
Feature: Test Spring Boot API

Scenario: Test Hello API

status: 200
response: Hello from Spring Boot!

Tests run: 1
Failures: 0
Errors: 0

BUILD SUCCESS
```

## 6. RESULT

Thus, Karate and Spring Boot testing were successfully installed and explored. A REST API was created using Spring Boot, and automated API testing was performed using the Karate framework. The test was executed successfully with the expected response.

## 7. IMPORTANT COMMANDS FOR LAB EXAM

| Command                                    | Purpose                     |
| ------------------------------------------ | --------------------------- |
| `sudo apt update`                          | Update package list         |
| `sudo apt install openjdk-17-jdk maven -y` | Install Java and Maven      |
| `java -version`                            | Check Java version          |
| `mvn -version`                             | Check Maven version         |
| `mvn spring-boot:run`                      | Run Spring Boot application |
| `curl http://localhost:8080/hello`         | Test REST API               |
| `mkdir -p src/test/java/com/example/demo`  | Create test directory       |
| `mvn test`                                 | Execute automated tests     |

## 8. VIVA QUESTIONS AND ANSWERS

1\. What is Spring Boot?

Spring Boot is a Java framework used to create standalone, production-ready applications quickly.

2\. What is Karate Framework?

Karate is an open-source testing framework used for automated API testing.

3\. What is Maven?

Maven is a build automation and dependency management tool used in Java projects.

4\. What is REST API?

REST API is an interface that allows applications to communicate using HTTP methods.

5\. What is JDK?

JDK stands for Java Development Kit. It provides tools to develop and run Java applications.

6\. What is the purpose of `@RestController`?

It defines a REST controller that handles HTTP requests and returns data as responses.

7\. What is `@GetMapping`?

It maps HTTP GET requests to a particular method in a Spring Boot application.

8\. What is a Feature file in Karate?

A feature file contains test scenarios written in Gherkin syntax.

9\. What is HTTP status code 200?

It indicates that the HTTP request was successful.

10\. What is the purpose of `mvn test`?

It executes the automated test cases in a Maven project.

11\. What is JUnit 5?

JUnit 5 is a Java testing framework used to write and execute unit tests.

12\. What is automated testing?

Automated testing uses software tools to execute test cases and verify application results automatically.

Complete lab exam write-up

Important practical note: Keep the Spring Boot application running in the first terminal while executing `mvn test` in the second terminal. Otherwise, the Karate test cannot connect to `localhost:8080`. Also, the `pom.xml` must contain both the Spring Boot testing dependency and the Karate dependency.
