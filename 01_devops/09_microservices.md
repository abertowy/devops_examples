# Microservices

## Table of contents
1. [What is microservices](#question1)
2. [Microservice vs Monolit](#question2)
3. [Microservice vs SOA](#question3)
4. [Coupling, high cohesion, and domain-driven design](#question4)
5. [Inter-service communication patterns](#question5)
6. [Role of API Gateways and service discovery mechanisms](#question6)
7. [Handling distributed transactions and ensuring data consistency](#question7)
8. [REST API](#question8)
9. [Some](#question9)
10. [Some](#question10)

## 1. What is microservices <a name="question1"></a>

Microservices are a software architecture style that structures a large application as a collection of small, independent, and loosely coupled services, each responsible for a specific business function. These services can be developed, deployed, and scaled independently using different technologies, and they communicate with each other over a network, often through lightweight APIs or messaging systems. This approach offers benefits like increased agility, improved scalability, and greater fault isolation compared to traditional monolithic applications. 

- Small and Independent:
    Each microservice is a small, self-contained unit with its own responsibility, codebase, and even database. 
- Loosely Coupled:
    Services are not tightly integrated; they can operate and evolve independently without affecting others. 
- Business-Oriented:
    Services are typically organized around business capabilities or specific functions. 
- Autonomous Deployment:
    Each service can be developed, tested, and deployed in isolation from the rest of the application. 
- Communication via APIs:
    Services communicate over a network using well-defined interfaces, such as RESTful APIs or messaging protocols. 
- Technological Diversity:
    Teams can choose the best programming languages, frameworks, and technologies for each individual service. 

Benefits
- Agility & Faster Time-to-Market:
    Independent deployment allows for more frequent and faster delivery of new features. 
- Scalability:
    Each service can be scaled independently based on its specific demand, leading to more efficient resource utilization. 
- Resilience:
    The failure of one service typically does not bring down the entire application. 
- Technological Freedom:
    Teams can select the most appropriate tools for each service, fostering innovation. 
- Team Autonomy:
    Small, focused teams can own and manage their services, improving productivity. 

## 2. Microservice vs Monolit <a name="question2"></a>

**Contrast with Monolithic Architecture**  
In a monolithic architecture, the entire application is built as a single, tightly integrated unit. This can make development, scaling, and updates more challenging, as changes to one part of the application can have unintended consequences for others. Microservices offer a way to break down these large, complex systems into more manageable and flexible components

## 3. Microservice vs Service-Oriented Architecture <a name="question3"></a>

Service-Oriented Architecture (SOA) and Microservices are architectural styles for building applications, both aiming to decompose large systems into smaller, manageable units. However, they differ in scope, design principles, and implementation details.

1. Service-Oriented Architecture (SOA):
    - Scope:
        SOA typically has an enterprise-wide scope, focusing on integrating various business processes and applications across an organization.
    - Service Definition:
        Services are often coarse-grained and can be shared and reused across multiple applications.
    - Communication:
        SOA often relies on an Enterprise Service Bus (ESB) for communication between services, facilitating centralized control and orchestration.
    - Data Governance:
        Data management can be centralized, with services potentially sharing a common database.
    - Deployment:
        Services in SOA are often deployed as part of a larger, potentially monolithic application. 
2. Microservices Architecture:
    - Scope:
        Microservices have an application-specific scope, focusing on decomposing a single application into independently deployable services.
    - Service Definition:
        Services are fine-grained, highly specialized, and designed to perform a single business capability.
    - Communication:
        Microservices use lightweight communication protocols like HTTP/REST and messaging queues, promoting decentralized communication.
    - Data Governance:
        Each microservice typically owns its data store, promoting independent data management and reducing dependencies.
    - Deployment:
        Microservices are independently deployable, allowing for faster development cycles and continuous delivery.


Key Differences Summarized:
- Scope: SOA is enterprise-wide; Microservices are application-specific.
- Granularity: SOA services are typically coarse-grained; Microservices are fine-grained.
- Communication: SOA often uses ESBs; Microservices use lightweight protocols.
- Data Management: SOA can have centralized data; Microservices promote independent data stores.
- Deployment: SOA services can be part of larger deployments; Microservices are independently deployable.

## 4. Coupling, high cohesion, and domain-driven design (DDD) in microservices <a name="question4"></a>

## 5. Inter-service communication patterns <a name="question5"></a>

## 6. Role of API Gateways and service discovery mechanisms <a name="question6"></a>

## 7. Handling distributed transactions and ensuring data consistency <a name="question7"></a>

## 8. REST API <a name="question8"></a>

A REST API, or RESTful API, is an Application Programming Interface (API) that adheres to the architectural style known as Representational State Transfer (REST). This style defines a set of constraints for how web services should be designed and interact, primarily over the HTTP protocol. 

Key characteristics and principles of REST APIs:
1. Client-Server Architecture:
    The client (e.g., a web browser or mobile app) and the server (e.g., a web service providing data) are separate and independent, allowing for scalability and flexibility.
2. Statelessness:
    Each request from the client to the server must contain all the information necessary to understand and fulfill the request. The server does not store any client context between requests. 
3. Cacheability:
    Responses from the server can be declared cacheable or non-cacheable, allowing clients to store responses to improve performance and reduce server load.
4. Uniform Interface:
    This is a core principle, emphasizing a consistent and standardized way of interacting with resources. It includes:
    - **Resource Identification:** Resources are identified by unique Uniform Resource Identifiers (URIs).
    - **Resource Manipulation through Representations:** Clients interact with resources by manipulating their representations (e.g., JSON or XML).
    - **Self-descriptive Messages:** Messages exchanged between client and server contain enough information to be understood without prior knowledge.
    - **Hypermedia as the Engine of Application State (HATEOAS):** Resources include links to related resources, guiding the client through the application's state.
5. Layered System:
    A client can connect to an end server through intermediate servers (e.g., load balancers, proxies) without being aware of the layers.

**How REST APIs work:**
REST APIs typically use standard HTTP methods (like GET, POST, PUT, DELETE) to perform operations on resources, which are identified by URLs.
- GET: Retrieves a resource or a collection of resources.
- POST: Creates a new resource.
- PUT: Updates an existing resource (or creates it if it doesn't exist).
- DELETE: Removes a resource. 
  
Responses are often returned in data formats like JSON (JavaScript Object Notation) or XML (Extensible Markup Language).
  
Advantages of REST APIs:
- **Simplicity**: They are relatively easy to understand and implement.
- **Scalability**: The stateless nature and client-server separation facilitate scaling.
- **Flexibility**: They support various data formats and can be built with different programming languages.
- **Performance**: Cacheability and statelessness can lead to efficient data transfer.


## 9.  <a name="question9"></a>

## 10.  <a name="question10"></a>