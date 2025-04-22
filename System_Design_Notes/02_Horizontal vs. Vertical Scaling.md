# Basics of System Design

This content introduces the fundamental concepts of system design, ideal for those with no prior experience.  It covers taking a simple algorithm and making it a scalable, resilient, and consistent service.

## 1. From Algorithm to API

*   **Scenario:** You have an algorithm (code) on your computer that people find valuable and are willing to pay for.
*   **Problem:** You can't simply give everyone your computer.
*   **Solution:**
    *   Expose the code using a protocol accessible over the internet (an API).
    *   The API receives *requests* and sends back *responses*.
*   **Key Concept:**  API (Application Programming Interface) is the interface through which users interact with your code.

## 2. Hosting on the Cloud

*   **Problem:**  Setting up the computer, connecting a database, configuring endpoints, and dealing with power loss are complex and risky.  You can't afford downtime.
*   **Solution:** Host the service on the cloud.
*   **Explanation:**
    *   The cloud is a collection of computers provided as a service for money.
    *   Cloud providers (e.g., AWS) handle the configuration, settings, and reliability aspects.
    *   You effectively "rent" computation power.
*   **Benefits:** Reduces operational burden, allowing focus on business requirements.

## 3. Scalability: Handling Increased Demand

*   **Problem:**  The code running on a single machine can't handle the increasing number of connections.
*   **Solution:**  Increase the system's *scalability* – its ability to handle more requests.
*   **Two Approaches:**
    *   Vertical Scaling
    *   Horizontal Scaling

## 4. Vertical Scaling

*   **Definition:** Buying a bigger, more powerful machine (CPU, RAM).
*   **Benefit:** The larger machine can process requests faster.

## 5. Horizontal Scaling

*   **Definition:** Buying more machines.
*   **Explanation:** Requests are distributed randomly amongst the machines.
*   **Benefit:** More machines = more capacity.

## 6. Comparing Vertical and Horizontal Scaling

| Feature               | Vertical Scaling                 | Horizontal Scaling                      |
|-----------------------|------------------------------------|------------------------------------------|
| Load Balancing         | Not required                     | Required                                  |
| Fault Tolerance       | Single point of failure           | Resilient (requests redirected if a machine fails) |
| Communication        | Interprocess Communication (fast) | Network calls (Remote Procedure Calls - slow)  |
| Data Consistency       | Consistent                       | Difficult to maintain (loose transactional guarantees)|
| Hardware Limits        | Exists                           | Scales well (linear with user growth)       |

## 7. Hybrid Approach (Real World)

*   **Description:** Combines the benefits of both vertical and horizontal scaling.
*   **Details:**
    *   Horizontal scaling is the primary approach.
    *   Each machine is made as powerful as is feasible (vertical scaling).
    *   Start with vertical scaling and, transition to horizontal scaling once the user base grows.

## 8. Key Considerations in System Design

*   **Scalability:** Can the system handle increasing load?
*   **Resilience:** Can the system recover from failures?
*   **Consistency:** Is the data consistent across the system?
*   **Trade-offs:** System design involves balancing these qualities; there's no perfect solution.
*   **Goal:**  Design a system that meets the requirements in the most feasible way.