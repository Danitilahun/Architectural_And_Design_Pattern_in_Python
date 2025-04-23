# Event-Driven Architecture

![Event-Driven Architecture](./image/Event-Driven%20Architecture.jpg)

This explanation covers event-driven architecture, a design pattern where services communicate through asynchronous events.

## 1. Key Differences from Request/Response

*   **Request/Response:** Clients send requests to gateway services, and those services interact directly.
*   **Event-Driven:** Services never interact directly. They use events to indicate state changes.
    *  services use events to state that yes something has changed.

## 2. The Event Bus

*   A service sends an event to the *event bus* (similar to a message broker).
*   The event bus is the way services communicate with each other.
*   Services state something is happened and if it concerns others they can consume the event.
*   Interested services (*subscribers* or *consumers*) consume the event to see if it's relevant.
*   Consumers may then generate their own events, creating a chain of reactions.

## 3. Storing Event Data

*   Each service typically stores the events it receives in its *own local database*.
*   It's not compulsory to store all of these events.
*   It's important to pass this persistence requirement and each of the services must store all the relevant events.
*   Services can add additional relevant fields or remove irrelevant fields.
*This makes each services independent

## 4. Advantages of Event-Driven Architecture

*   **Availability:** Even if a service goes down, consumers can still access relevant events from their local databases.
    * You don't need to ask it for relevant events so you are available although with high availability comes one straight off problem which is consistency.
*   **Historical Replay:** The *event log* (database) allows you to move to any point in history by replaying events.
    * Going from start to particular point is easy
    * If you have any bug come, you can actually debug even production systems.
*   **Easy Service Replacement:** New services can easily replace old ones by replaying historical events.
    * Asks even bus to send you events.
*   **Transactional Guarantees:** Messages are guaranteed to be delivered *at least once* or *at most once*.
*   **Intent Capture:** Storing event data captures the *intent* behind the data change.  A newer services, the service will determine the actions.

## 5. Disadvantages of Event-Driven Architecture

*   **Challenges with External Dependencies:** If a service interacts with external systems (e.g., sending emails), it becomes difficult to replay events accurately because external responses may be time-dependent.
*   *There is a major issues with event driven architecture*
*   **Limited Control:** Less fine-grained control over the handling of events compared to request/response. It depends on the event bus if you don't mention to the event bus what happened, it still may not come.

*   **Data Exposure Concerns:** You may not want all services consuming all events.
*    You should fine-tune when you want to make something available.

## 6. State Management & Historical Replay

*There are two ways of replay*
*   **Replay from Start:** Replaying all events, completely impractical.
*   **Diff-Based:** Store the first event then the diffs in state.
*Use an Undo command all the way to that version

## 7. Developer Challenges

*   **Difficult to Reason About Flow:** Hard to trace the path of a program, making it difficult to understand what is going on. *looking at one, it's hard to understand*. If developers use service one, they are publishing but can't figure out the code stop.
*   **Difficult to Move Out Of:** Hard to transition from an event-driven architecture to a request/response architecture. Almost all is based on Events.

## 8. Conclusion

*In summary, event-driven architectures have the following*
*  **Event Logged:** all service will be created with logging their event
*   **Publisher Subscriber Model:** passing and consuming these event

*The difference between the service is what they look for*
*   They publish when they think some people needs to know
*   Responses are only asked when services is asked for.

*   In this case. most of the advantages/disadvantages stem to these subtle differences
*   Get and Smalltalk have this with the best.