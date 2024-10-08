https://microservices.io/patterns/index.html

# Design patterns for microservices
Design patterns for microservices provide best practices and solutions for common challenges in building and maintaining microservices architectures. Here are some key design patterns:

### 1. **Decomposition Patterns**
   - **Service per Business Capability**: Aligns services with business capabilities.
   - **Service per Team**: Each team is responsible for one or more services, promoting autonomy.

### 2. **Data Management Patterns**
   - **Database per Service**: Each service manages its own database, ensuring decoupling.
   - **Shared Database**: Multiple services share a single database, which can simplify management but reduce decoupling.
   - **Saga**: Manages distributed transactions by using a sequence of local transactions.
   - **Command Query Responsibility Segregation (CQRS)**: Separates read and write operations to optimize handling and scalability.

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

