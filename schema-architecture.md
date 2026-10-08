# Smart Clinic Management System - Architecture Design

## 1. Architecture Summary

The Smart Clinic Management System is a Spring Boot-based three-tier web application that uses both Spring MVC and REST APIs. Thymeleaf is used to render the Admin and Doctor dashboards as server-side HTML pages, while REST APIs provide JSON-based communication for modules such as appointments and patient-related functionality.

The application separates responsibilities into presentation, application, and data tiers. Controllers receive requests from users or API clients and delegate business operations to the service layer. The service layer contains the main business logic and communicates with repositories to access persistent data.

The system uses two databases based on the type of data being stored. MySQL is used for structured relational data such as patients, doctors, appointments, and administrators through Spring Data JPA and JPA entities. MongoDB is used for flexible document-based data such as prescriptions through Spring Data MongoDB and document models.

This architecture provides separation of concerns, maintainability, scalability, and flexibility while allowing both server-rendered web interfaces and REST-based clients to use the same backend services.

## 2. Numbered Flow of Data and Control

1. **User Interface Layer**  
   Users access the Smart Clinic Management System through the Admin Dashboard or Doctor Dashboard, which are rendered using Thymeleaf. Other clients, such as frontend applications or mobile applications, can access appointment and patient-related functionality through REST APIs.

2. **Controller Layer**  
   Incoming requests are routed to the appropriate controller based on the requested URL and HTTP method. Thymeleaf controllers handle requests for server-rendered pages, while REST controllers handle API requests and return JSON responses.

3. **Service Layer**  
   The controllers delegate processing to the service layer. The service layer contains the application's business logic, performs validations, applies business rules, and coordinates operations such as checking doctor availability before creating an appointment.

4. **Repository Layer**  
   The service layer communicates with repositories to retrieve and persist data. MySQL repositories use Spring Data JPA for relational data, while the MongoDB repository uses Spring Data MongoDB for document-based data such as prescriptions.

5. **Database Access**  
   The repositories communicate with the appropriate database. MySQL stores structured entities such as patients, doctors, appointments, and administrators. MongoDB stores flexible document-based information such as prescriptions.

6. **Model Binding**  
   Data retrieved from the databases is mapped into Java model classes. MySQL records are represented using JPA entities annotated with `@Entity`, while MongoDB documents are represented using document models annotated with `@Document`.

7. **Response and Presentation**  
   The processed models are returned to the appropriate presentation layer. In MVC flows, model data is passed to Thymeleaf templates and rendered as HTML for the browser. In REST flows, model data or DTOs are serialized into JSON and returned to the API client.