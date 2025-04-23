# Publisher Subscriber Model - Event-Driven Services

![Publisher Subscriber Model](./image/Publisher%20Subscriber%20Model.png)

This explanation focuses on event-driven services, a microservice architecture built on the publisher-subscriber model.

## 1. Initial Scenario: Microservices with Request/Response

*   Microservice architecture with services SS0, SS1, SS2, SS3, SS4.
*   Client connected to SS1.
*   SS1 needs to send messages to SS0 and SS2.  The order of messages doesn't matter.
*   SS2 needs to send messages to SS3 and SS4.  The order doesn't matter.
*Using a request/response architecture will do this thing asynchronously

## 2. Drawbacks of Request/Response

*   SS2 might wait for both services to complete and sends a time out to SS1.
*   it took a long time for this request to fail.

## 3. Publisher-Subscriber Model

*Instead of sending two messages*
*   SS1 sends a message to a *message broker* (e.g., Kafka, RabbitMQ).
*   The message broker sends the message to SS2.
*   SS1 then sends success to the client.
*    Kafka is going to persist the message and abstract things out
*   Same process is followed by SS2 sending to S3 and S4.
*   The request response is taken out of S1.

## 4. Advantages of Event Driven Services

*   **Decoupling:** SS1 is no longer dependent on S2 and S0.
*   So it just publishes to the message broker and it has now been relieved.
*   Client says that this is successful to broker.
*   If it is successful, the message broker then needs to persist those messages
*   **Easier to Understand:** A single point of failure (the message broker) is easier to deal with than multiple dependencies.
*   **Single Interface:** A generic message format is used, simplifies development.
    *   It sends a generic message with a lot of data so it can consume it and take data
*   **Transaction Guarantees (At-Least-Once):** If SS1 successfully persists the message to the message broker, the message will eventually reach SS3 and SS4, it has some persistence
*   The message broker isn't going to lose messages because the persistence of it.
*   "Guaranteed to be done at some point of time".
*   **Scalability:** New services (e.g., S6) can subscribe to S1's messages without SS1 needing to know. A new services can register messages without knowing the publishers.

## 5. Disadvantages of Event Driven Services

*In financial systems*
*   Let's say you have an invoice and a fund transfer. S1 is the gateway that just processes.
*You get a request from client saying to transfer funds to A. Initial Amount 1000. Commission for the bank 50. Final expectation A = 0, B=950.*
*   **Consistency Challenges:** Difficult to use in systems requiring strong consistency (e.g., financial transactions). Cannot be used for a system which requires success and failure, no atomicity.
    *   If a transfer does not run this can be confusing.
*  **Financial system scenario**
    *   A, a gateway, forwards the message to S2.
    *   S0 takes a comission
* **Item Potency Concerns:** The general architecture won't help developers, they need to focus on the messages sent. Does not guarantee anything with item potency because of multiple depletions of funds in account (S2)
*   What happened if SS4 fails?

## 6. Use Cases

*   Not good for financial systems.
*   Good for gaming services (analytics) or sending events that have occurred.
*   **Example:** Twitter (posting a tweet and having many people consume it). A business posting and a way for users to subscribe is a perfect business model