# Design Patterns
https://refactoring.guru/design-patterns/java

## Creational
Creational patterns are ones that create objects, rather than having to instantiate objects directly. This gives the program more flexibility in deciding which objects need to be created for a given case.
 - Abstract factory groups object factories that have a common theme.

 - Builder constructs complex objects by separating construction and representation.

 - Factory method creates objects without specifying the exact class to create.

 - Prototype creates objects by cloning an existing object.

 - Singleton restricts object creation for a class to only one instance.

# Structural
These concern class and object composition. They use inheritance to compose interfaces and define ways to compose objects to obtain new functionality.
 - Adapter allows classes with incompatible interfaces to work together by wrapping its own interface around that of an already existing class.

 - Bridge decouples an abstraction from its implementation so that the two can vary independently.
 ```java
 // Logger has two implementations: info and warning
 @FunctionalInterface
 interface Logger {
     void log(String message);

     static Logger info() {
         return message -> System.out.println("info: " + message);
     }
     static Logger warning() {
         return message -> System.out.println("warning: " + message);
     }
 }

 abstract class AbstractAccount {
     private Logger logger = Logger.info();

     public void setLogger(Logger logger) {
         this.logger = logger;
     }

     // the logging part is delegated to the Logger implementation
     protected void operate(String message, boolean result) {
         logger.log(message + " result " + result);
     }
 }
 ```

 - Composite composes zero-or-more similar objects so that they can be manipulated as one object.

 - Decorator dynamically adds/overrides behaviour in an existing method of an object.
 ```java
 // abstract decorator class - note that it implements Window
 abstract class WindowDecorator implements Window {
     private final Window windowToBeDecorated; // the Window being decorated

     public WindowDecorator (Window windowToBeDecorated) {
         this.windowToBeDecorated = windowToBeDecorated;
     }
     @Override
     public void draw() {
         windowToBeDecorated.draw(); //Delegation
     }
     @Override
     public String getDescription() {
         return windowToBeDecorated.getDescription(); //Delegation
     }
 }

 // The first concrete decorator which adds vertical scrollbar functionality
 class VerticalScrollBarDecorator extends WindowDecorator {
     public VerticalScrollBarDecorator (Window windowToBeDecorated) {
         super(windowToBeDecorated);
     }

     @Override
     public void draw() {
         super.draw();
         drawVerticalScrollBar();
     }

     private void drawVerticalScrollBar() {
         // Draw the vertical scrollbar
     }

     @Override
     public String getDescription() {
         return super.getDescription() + ", including vertical scrollbars";
     }
 }

 // The second concrete decorator which adds horizontal scrollbar functionality
 class HorizontalScrollBarDecorator extends WindowDecorator {
     public HorizontalScrollBarDecorator (Window windowToBeDecorated) {
         super(windowToBeDecorated);
     }

     @Override
     public void draw() {
         super.draw();
         drawHorizontalScrollBar();
     }

     private void drawHorizontalScrollBar() {
         // Draw the horizontal scrollbar
     }

     @Override
     public String getDescription() {
         return super.getDescription() + ", including horizontal scrollbars";
     }
 }
 ```

 - Facade provides a simplified interface to a large body of code.

 - Flyweight reduces the cost of creating and manipulating a large number of similar objects.
```c#
 // Defines Flyweight object that repeats itself.
public class Flyweight
{
    public string CompanyName { get; set; }
    public string CompanyLocation { get; set; }
    public string CompanyWebsite { get; set; }
    // Bulky data
    public byte[] CompanyLogo { get; set; }
}

public static class FlyweightPointer
{
    public static readonly Flyweight Company = new Flyweight
    {
        CompanyName = "Abc",
        CompanyLocation = "XYZ",
        CompanyWebsite = "www.example.com"
        // Load CompanyLogo here
    };
}

public class MyObject
{
    public string Name { get; set; }
    public string Company => FlyweightPointer.Company.CompanyName;
}
```

 - Proxy provides a placeholder for another object to control access, reduce cost, and reduce complexity.

Example: cache, lazy loading

## Behavioral
Most of these design patterns are specifically concerned with communication between objects.
 - Chain of responsibility delegates commands to a chain of processing objects.

 - Command creates objects that encapsulate actions and parameters.

 - Interpreter implements a specialized language.

 - Iterator accesses the elements of an object sequentially without exposing its underlying representation.

 - Mediator allows loose coupling between classes by being the only class that has detailed knowledge of their methods.

 - Memento provides the ability to restore an object to its previous state (undo).

 - Observer is a publish/subscribe pattern, which allows a number of observer objects to see an event.

 - State allows an object to alter its behavior when its internal state changes.

 - Strategy allows one of a family of algorithms to be selected on-the-fly at runtime.

 - Template method defines the skeleton of an algorithm as an abstract class, allowing its subclasses to provide concrete behavior.

 - Visitor separates an algorithm from an object structure by moving the hierarchy of methods into one object.


# SOLID Principles:
1. **Single Responsibility Principle (SRP)**
   - **Definition:** A class should have only one reason to change, meaning it should have only one job or responsibility.
   - **Explanation:** By adhering to SRP, you ensure that each class in your codebase addresses a single concern, making it easier to understand, test, and maintain. Changes in one part of the application will not affect unrelated parts.

   **Example:** A class handling user authentication should not also be responsible for logging user activities. These should be separate classes.

2. **Open/Closed Principle (OCP)**
   - **Definition:** Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
   - **Explanation:** This principle encourages developers to write code that can be extended without modifying existing code, thereby reducing the risk of introducing bugs when new features are added.

   **Example:** If you have a base class `Shape` with a method `draw()`, you can extend it by creating subclasses like `Circle` and `Rectangle` that override the `draw()` method, without altering the `Shape` class itself.

3. **Liskov Substitution Principle (LSP)**
   - **Definition:** Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
   - **Explanation:** This principle ensures that a subclass can stand in for its superclass and behave in the same way without causing errors or unexpected behavior.

   **Example:** If you have a class `Bird` with a method `fly()`, and a subclass `Penguin` which cannot fly, then `Penguin` should not inherit from `Bird`. Instead, you might need a different design to respect LSP.

4. **Interface Segregation Principle (ISP)**
   - **Definition:** Clients should not be forced to depend on interfaces they do not use.
   - **Explanation:** This principle advocates for creating specific interfaces rather than a large, general-purpose one. This way, classes that implement these interfaces are only concerned with the methods that are relevant to them.

   **Example:** Instead of a single `Animal` interface with methods `eat()`, `sleep()`, `fly()`, and `swim()`, you could have separate interfaces like `IFlyable` and `ISwimmable` for animals that can fly or swim, respectively.

5. **Dependency Inversion Principle (DIP)**
   - **Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces). Additionally, abstractions should not depend on details. Details should depend on abstractions.
   - **Explanation:** This principle encourages decoupling software modules to enhance flexibility and reusability. By depending on abstractions rather than concrete implementations, changes in low-level modules do not directly impact high-level modules.

   **Example:** Instead of a class `Database` directly depending on a specific `MySQLDatabase` class, it should depend on an interface `IDatabase` that `MySQLDatabase` implements. This way, you can switch to a different database implementation with minimal changes.

### Summary:
- **SRP**: One class, one responsibility.
- **OCP**: Extendable without modification.
- **LSP**: Subtypes should be substitutable for their base types.
- **ISP**: Prefer small, specific interfaces.
- **DIP**: Depend on abstractions, not concretions.


# Design patterns for microservices
Design patterns for microservices provide best practices and solutions for common challenges in building and maintaining microservices architectures. Here are some key design patterns:

### 1. **Decomposition Patterns**
   - **Service per Business Capability**: Aligns services with business capabilities.
   - **Service per Team**: Each team is responsible for one or more services, promoting autonomy.

### 2. **Data Management Patterns**
   - **Database per Service**: Each service manages its own database, ensuring decoupling.
   - **Shared Database**: Multiple services share a single database, which can simplify management but reduce decoupling.
   - **Saga**: Manages distributed transactions by using a sequence of local transactions.

### 3. **Communication Patterns**
   - **API Gateway**: Acts as a single entry point for all client requests, handling routing, authentication, and other concerns.
   - **Service Discovery**: Automatically detects service instances to enable dynamic scaling and load balancing.
   - **Circuit Breaker**: Prevents cascading failures by stopping attempts to access a failing service.
   - **Event-Driven Communication**: Services communicate via events, promoting loose coupling and asynchronous interactions.

### 4. **Deployment Patterns**
   - **Single Service per Host**: Deploys each service on a separate host, simplifying resource allocation and isolation.
   - **Multiple Services per Host**: Deploys multiple services on the same host to optimize resource usage.
   - **Service Instance per Container**: Each service instance runs in its own container, promoting isolation and easy scaling.

### 5. **Observability Patterns**
   - **Log Aggregation**: Collects and centralizes logs from all services for monitoring and debugging.
   - **Distributed Tracing**: Tracks requests across multiple services to diagnose latency and failures.
   - **Health Check**: Monitors the health of services to detect and handle failures.

### 6. **Security Patterns**
   - **Access Token**: Uses tokens (e.g., JWT) for secure, stateless authentication and authorization.
   - **Role-Based Access Control (RBAC)**: Manages permissions based on user roles.
   - **API Gateway Security**: Implements security measures such as SSL termination and rate limiting at the gateway level.

### 7. **Scalability Patterns**
   - **Auto-Scaling**: Automatically adjusts the number of service instances based on demand.
   - **Replication**: Creates multiple instances of a service to handle increased load.

### 8. **Resilience Patterns**
   - **Bulkhead**: Isolates critical resources to prevent failures from spreading.
   - **Retry**: Automatically retries failed requests with exponential backoff.
   - **Fallback**: Provides alternative functionality or degraded performance when a service fails.

### 9. **Configuration Management Patterns**
   - **Externalized Configuration**: Stores configuration outside the application to enable dynamic updates without redeployment.
   - **Service Mesh**: Manages service-to-service communication, security, and observability centrally.

### 10. **Testing Patterns**
   - **Consumer-Driven Contracts**: Ensures compatibility between services by defining and testing contracts from the consumer's perspective.
   - **Service Virtualization**: Simulates service dependencies to test a service in isolation.

Implementing these patterns can help address the complexity and challenges of building robust, scalable, and maintainable microservices architectures.


# Message Broker
A message broker is a software intermediary that enables different systems or applications to communicate with each other by translating messages from the formal messaging protocol of the sender to the formal messaging protocol of the receiver. This allows for decoupled, scalable, and reliable communication between distributed systems.

### Key Functions of a Message Broker:

1. **Message Routing:**
   - Directs messages from senders to the correct receivers based on predefined rules or patterns.

2. **Message Transformation:**
   - Converts messages from one format or protocol to another to ensure compatibility between different systems.

3. **Message Buffering:**
   - Temporarily stores messages to handle differences in processing speeds between producers and consumers.

4. **Message Filtering:**
   - Filters messages so that only relevant messages are delivered to each receiver.

5. **Message Security:**
   - Ensures that messages are securely transmitted between systems, often through encryption and authentication mechanisms.

6. **Load Balancing:**
   - Distributes messages across multiple consumers to balance the load and ensure efficient processing.

### Benefits of Using a Message Broker:

- **Decoupling:**
  - Enables systems to communicate without being directly connected, enhancing flexibility and scalability.
  
- **Reliability:**
  - Provides mechanisms for ensuring messages are delivered and processed reliably, even in the event of failures.

- **Scalability:**
  - Supports scaling by allowing multiple producers and consumers to connect and communicate efficiently.

- **Asynchronous Communication:**
  - Facilitates asynchronous messaging, enabling systems to continue processing without waiting for responses.

### Examples of Message Brokers:

- **RabbitMQ:**
  - An open-source message broker that supports multiple messaging protocols.

- **Apache Kafka:**
  - A distributed streaming platform used for building real-time data pipelines and streaming applications.

- **ActiveMQ:**
  - An open-source message broker that supports JMS (Java Message Service) and many other messaging protocols.

- **Amazon SQS (Simple Queue Service):**
  - A fully managed message queuing service provided by AWS.

### Common Use Cases:

- **Event-driven Architectures:**
  - Triggering actions or processing workflows based on specific events occurring in a system.

- **Microservices Communication:**
  - Enabling communication and data exchange between different microservices in a distributed application.

- **Data Streaming:**
  - Collecting, processing, and analyzing real-time data streams from various sources.

- **Task Queuing:**
  - Distributing and managing tasks among multiple workers or processing units.

Message brokers play a critical role in modern software architectures by facilitating robust, efficient, and scalable communication between different systems and components.


# Publish/Subscribe
"Pub/Sub" (short for "Publish/Subscribe") is a messaging pattern where publishers send messages without knowing who the recipients (subscribers) are, and subscribers receive only the messages that interest them without knowing who the publishers are. This decoupling of publishers and subscribers allows for scalable, flexible, and efficient communication in distributed systems.

### Key Components of Pub/Sub:

1. **Publishers:**
   - Entities or components that produce messages and publish them to specific topics.

2. **Subscribers:**
   - Entities or components that consume messages. They subscribe to specific topics to receive messages relevant to them.

3. **Topics:**
   - Named channels or subjects to which publishers send messages and from which subscribers receive messages.

4. **Message Broker:**
   - An intermediary that manages the topics, receives messages from publishers, and delivers them to the appropriate subscribers.

### How Pub/Sub Works:

1. **Publishing Messages:**
   - A publisher sends a message to a specific topic on the message broker.

2. **Topic Management:**
   - The message broker receives the message and categorizes it under the given topic.

3. **Subscription:**
   - Subscribers express interest in one or more topics by subscribing to them.

4. **Message Delivery:**
   - The message broker delivers the message to all subscribers who have subscribed to the topic.

### Benefits of Pub/Sub:

- **Decoupling:**
  - Publishers and subscribers do not need to know about each other, leading to a more flexible system architecture.

- **Scalability:**
  - The system can easily handle an increasing number of publishers and subscribers without significant changes to the underlying infrastructure.

- **Flexibility:**
  - New subscribers can be added without affecting existing publishers or other subscribers.

- **Efficiency:**
  - Messages are only sent to subscribers who have expressed interest in them, reducing unnecessary data transmission.

### Use Cases of Pub/Sub:

- **Real-Time Notifications:**
  - Sending real-time alerts or notifications to users, such as updates on social media platforms.

- **Event-Driven Architectures:**
  - Triggering actions or workflows in response to specific events, such as updating inventory after a purchase.

- **Data Streaming:**
  - Streaming data from sensors or IoT devices to various data consumers for real-time processing and analysis.

- **Log Aggregation:**
  - Collecting and distributing logs from different services to centralized log processing systems.

### Examples of Pub/Sub Systems:

- **Google Cloud Pub/Sub:**
  - A fully managed messaging service that allows for asynchronous messaging between independent applications.

- **Apache Kafka:**
  - A distributed streaming platform that supports pub/sub messaging along with other capabilities.

- **Redis Pub/Sub:**
  - An in-memory data structure store that supports simple pub/sub messaging.

- **Amazon SNS (Simple Notification Service):**
  - A fully managed pub/sub messaging service provided by AWS.

### Summary:

Pub/Sub is a powerful messaging paradigm that supports the development of scalable, flexible, and efficient distributed systems by decoupling message producers and consumers. It is widely used in various applications, from real-time notifications to complex event-driven architectures.

