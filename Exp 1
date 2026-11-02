# EXPERIMENT 1: USER REGISTRATION FORM USING MICROSERVICES

## AIM
To write a program for a simple user registration form for an event using Spring Boot Microservices.

## SOFTWARE REQUIREMENTS
- Java JDK 17
- Spring Boot
- Maven
- Eclipse / VS Code
- Postman

## 1. CREATE EVENT SERVICE

Create a Spring Boot project using Spring Initializr.

- Project: Maven
- Language: Java
- Group: com.example
- Artifact: event-service
- Dependency: Spring Web
- Java: 17

Create the following files.

### Event.java

```java
package com.example.event_service;

public class Event {
    private String eventName;

    public Event() {
    }

    public Event(String eventName) {
        this.eventName = eventName;
    }

    public String getEventName() {
        return eventName;
    }

    public void setEventName(String eventName) {
        this.eventName = eventName;
    }
}
```

### EventController.java

```java
package com.example.event_service;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class EventController {

    @GetMapping("/event")
    public Event getEvent() {
        return new Event("Python Workshop");
    }
}
```

### EventServiceApplication.java

```java
package com.example.event_service;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class EventServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(EventServiceApplication.class, args);
    }
}
```

### application.properties

```properties
spring.application.name=event-service
server.port=8082
```

## 2. CREATE REGISTRATION SERVICE

Create another Spring Boot project using Spring Initializr.

- Project: Maven
- Language: Java
- Group: com.example
- Artifact: registration-service
- Dependency: Spring Web
- Java: 17

Create the following files.

### Event.java

```java
package com.example.registration_service;

public class Event {

    private String eventName;

    public Event() {
    }

    public String getEventName() {
        return eventName;
    }

    public void setEventName(String eventName) {
        this.eventName = eventName;
    }
}
```

### Registration.java

```java
package com.example.registration_service;

public class Registration {

    private int id;
    private String name;
    private String email;
    private String event;

    public Registration() {
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getEvent() {
        return event;
    }

    public void setEvent(String event) {
        this.event = event;
    }
}
```

### RegistrationController.java

```java
package com.example.registration_service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.client.RestTemplate;

@RestController
@RequestMapping("/registration")
public class RegistrationController {

    @Autowired
    private RestTemplate restTemplate;

    @GetMapping
    public String testRegistrationService() {
        return "Registration Service is running";
    }

    @PostMapping
    public Registration register(
            @RequestBody Registration registration) {

        Event event = restTemplate.getForObject(
                "http://localhost:8082/event",
                Event.class
        );

        if (event != null) {
            registration.setEvent(event.getEventName());
        }

        return registration;
    }
}
```

### RegistrationServiceApplication.java

```java
package com.example.registration_service;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.web.client.RestTemplate;

@SpringBootApplication
public class RegistrationServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(
                RegistrationServiceApplication.class, args);
    }

    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

### application.properties

```properties
spring.application.name=registration-service
server.port=8083
```

## 3. RUN THE APPLICATION

First, run the Event Service.

Linux:

```bash
./mvnw spring-boot:run
```

Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Next, open another terminal and run the Registration Service.

Linux:

```bash
./mvnw spring-boot:run
```

Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Keep both services running.

## 4. TEST USING POSTMAN

### Request 1: Get Event Details

- Method: GET
- URL: http://localhost:8082/event

Expected response:

```json
{
    "eventName": "Python Workshop"
}
```

### Request 2: Check Registration Service

- Method: GET
- URL: http://localhost:8083/registration

Expected response:

```text
Registration Service is running
```

### Request 3: Register a User

- Method: POST
- URL: http://localhost:8083/registration
- Select Body → raw → JSON.

Enter:

```json
{
    "id": 2,
    "name": "Gabber",
    "email": "gabber@gmail.com"
}
```

Expected response:

```json
{
    "id": 2,
    "name": "Gabber",
    "email": "gabber@gmail.com",
    "event": "Python Workshop"
}
```

## 5. RESULT

Thus, a simple user registration application for an event was developed successfully using Spring Boot Microservices. The Registration Service communicates with the Event Service using RestTemplate and retrieves the event details.

