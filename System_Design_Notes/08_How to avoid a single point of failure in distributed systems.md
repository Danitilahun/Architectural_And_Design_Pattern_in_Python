# How to Avoid Single Points of Failure

![How to avoid a single point of failure in distributed systems](./image/How%20to%20avoid%20a%20single%20point%20of%20failure%20in%20distributed%20systems.png)

This explanation focuses on single points of failure (SPOFs) in system design: points where the failure of a single component can bring down the entire system.

## 1. Definition of SPOF

*   Points where the entire system crashes in case that point crashes.

## 2. Importance of Resiliency

*   SPOFs indicate a lack of resiliency in the architecture.
*   Resiliency means having multiple components so if the point crashes, then
    your system crashes.

## 3. Mitigation Strategy: Add Redundancy

*   The obvious way to mitigate SPOFs is to add redundant nodes.
*   For a profile server, you can add another profile server.

## 4. Backup vs. Active-Active

*   Two Main Ways to Set Up Extra Nodes
*   **Backup:** A node that only activates when the primary fails.
*   **Active-Active:** Nodes that both actively serve requests. Active-Active is more useful in service level while backup is useful for data level.
*   **Example:** For a database, having a replica is a good backup strategy. Any change is mirrored in database so this creates redundancy and adds a master or slave architecture. The probability has suddenly become P square which is much smaller.

## 5. General Diagram & Redundancy

*   The basic way to mitigate single points of failure is adding more nodes.
*   **Client Failures:** Client failures are not typically a concern for the overall system's availability.
*   **Database Redundancy:** Master-slave architecture for the database, with read slaves for handling read requests.
*   **Load Balancer Redundancy:** Multiple load balancers are needed to distribute requests.
*   **DNS:** Clients connect to a DNS, which resolves to multiple IP addresses (the load balancers). Hitting facebook.com can land on any of the ip addresses.
*   **Gateway:** load balancer only would be a little misleading is actually a gateway having a load balancing mechanism.

## 6. Regional Distribution

*   To protect against disasters, distribute the system across multiple regions.
*   The entire system, if located in one place, will possibly fail during disaster.

## 7. Coordinator Redundancy

*   For distributed read/write operations in the database, any coordinator needs to be made redundant.
*   Coordinator failure should be handled in the same way as load balancer failure.

## 8. Resiliency: Ongoing Process

*   Achieving true resiliency involves addressing all SPOFs throughout the system.

## 9. Chaos Engineering

*   Netflix uses "Chaos Monkey" (and other tools) to randomly take down nodes in production to test the system's resiliency.

## 10. System Design Interview Tips

*   Talk about master-slave replication.
*   Throw more nodes at the problem.
*   Have multiple regions in case of disaster.