

# Quiz and Question Microservices Project

This project is a microservices-based system to manage quiz and question services. It is built using Spring Boot and Spring Cloud to create a scalable and distributed architecture. The project includes essential features such as service registry, API gateway, and load balancing.


## Table of Contents
1. [Project Overview](#project-overview)
2. [Technologies Used](#technologies-used)
3. [Microservices Architecture](#microservices-architecture)
4. [Features](#features)
5. [Setup Instructions](#setup-instructions)
6. [Microservices Communication](#microservices-communication)
7. [Service Registry](#service-registry)
8. [Load Balancing](#load-balancing)
9. [API Gateway](#api-gateway)
10. [Testing](#testing)
11. [Contributing](#contributing)
12. [License](#license)

## Project Overview

The project demonstrates how to create and manage multiple microservices for handling quizzes and questions using Spring Boot and Spring Cloud. Each microservice is responsible for a specific domain (e.g., Quiz Service, Question Service), and they communicate with each other using REST APIs and service discovery mechanisms.

## Technologies Used

- **Java** (JDK 11)
- **Spring Boot** (2.x.x)
- **Spring Cloud** (Hoxton/SR12)
- **Eureka** (Service Registry)
- **Spring Cloud Gateway** (API Gateway)
- **MySQL/PostgreSQL** (Database for persistence)
- **Docker** (for containerization)

## Microservices Architecture

The system is designed with a microservices architecture, where each service handles a different part of the business logic.

- **Quiz Service**: Manages quiz creation and details.
- **Question Service**: Manages question creation and linking questions to quizzes.

### Key Components:

1. **Service Registry**: Using Eureka for microservice discovery.
2. **API Gateway**: Spring Cloud Gateway for routing requests to appropriate services.
3. **Database**: MySQL/PostgreSQL for persistence of quiz and question data.
4. **Load Balancer**: Ensures requests are balanced across multiple service instances.

## Features

- **Creating Quiz and Questions**: The services allow creating quizzes and adding questions to them.
- **Service Registry**: Manages microservices and enables communication between them.
- **API Gateway**: Centralized entry point for all client requests.
- **Load Balancing**: Distributes traffic across multiple instances of services.
- **Microservices Communication**: RESTful communication between the services.
- **Containerization**: Services are Dockerized for ease of deployment.

## Setup Instructions

### Prerequisites

- Java JDK 11 or higher
- Docker
- Maven
- MySQL/PostgreSQL

### Steps

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/quiz-question-microservices.git
   ```
2. **Navigate to the project directory**:
   ```bash
   cd quiz-question-microservices
   ```
3. **Build the services**:
   ```bash
   mvn clean install
   ```
4. **Run the services using Docker**:
   ```bash
   docker-compose up
   ```

## Microservices Communication

Microservices communicate via REST APIs. In this project, we use **Feign Client** for easy inter-service communication. For example, the Quiz Service fetches questions from the Question Service using the Feign Client.

## Service Registry

We use **Eureka** as the service registry. This enables each service to register itself at startup and discover other services for communication.

### Steps to Start Eureka Server:

1. Start the Eureka server:
   ```bash
   cd eureka-server
   mvn spring-boot:run
   ```

2. All microservices will register themselves with the Eureka server once started.

## Load Balancing

We implement load balancing using **Spring Cloud LoadBalancer**. Multiple instances of the microservices can be deployed, and the API Gateway will route requests evenly among them.

### Example:
To see load balancing in action, start multiple instances of the Question Service and observe how requests are distributed.

## API Gateway

We use **Spring Cloud Gateway** to route external requests to internal services. The gateway is configured to direct traffic based on service names.

### Configuring API Gateway Routes:

In the `application.yml` of the API Gateway, routes are defined as follows:
```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: quiz_service
          uri: lb://QUIZ-SERVICE
          predicates:
            - Path=/quiz/**
        - id: question_service
          uri: lb://QUESTION-SERVICE
          predicates:
            - Path=/question/**
```

## Testing

Each service includes unit and integration tests to verify the functionality.

To run the tests:
```bash
mvn test
```

## Managing Multiple Microservice Instances

You can start multiple instances of any service to handle more requests. For example, using Docker Compose, you can scale up the number of instances:
```bash
docker-compose up --scale question-service=3
```

## Contributing

Feel free to open issues or submit pull requests to improve the project.

## License

This project is licensed under the MIT License.

---

Let me know if you'd like to adjust any sections or add more details!
