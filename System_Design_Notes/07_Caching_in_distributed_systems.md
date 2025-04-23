# Caching: A Fundamental Concept

![Caching in distributed systems](./image/Caching%20in%20distributed%20systems.png)

Caching is a core concept in computer science, integral to large-scale distributed systems. It involves tradeoffs to mitigate potential drawbacks.

## 1. Caching Basics: Instagram News Feed Example

*   **Scenario:** A user requests their Instagram news feed.
*   **Traditional Process:**
    1.  Request reaches server.
    2.  Server queries database to get followed users and their posts.
    3.  Database returns response to server.
    4.  Server sends response to client.
*   **Latency:** Assumed times: User-Server (100ms), Server-Database (10ms), Database-Server (10ms), Server-Client (100ms).  Total: 220ms.
*   **Backend Optimization Target:** Server-Database communication (10ms).

## 2. Caching: Reducing Repeatable Work

*   **Observation:** Similar users often request similar feeds (e.g., young software engineers in India who like football).
*   **Caching Strategy:**
    1.  When a user from a cohort requests a news feed, the feed is generated from the database.
    2.  The feed is stored in local memory (cache).
    3.  The feed is returned to the user.
    4.  For subsequent requests from similar users, the feed is retrieved from the cache instead of the database.
*   **Caching Saves Time and Resources:** Store computation in local memory instead of recomputing or recalling database. Caches are faster to query than databases.

## 3. Performance Gains

*   Assuming cache query time is 1ms and response time is 1ms, using the cache can save 10% of the total latency.

## 4. Client-Side Caching

*   Extend caching to the client device (mobile phone).
*   If a user repeatedly scrolls their news feed, reuse the data already fetched from the network.
*   Instead of making a 200ms call, the data can be loaded from the local device in ~2ms.

## 5. Limitations of Caching

*   Caching is reducing latency by just using more storage
*   **Question:** Why not cache the entire database?
*   **Answer:** For small, static databases, caching everything is viable. However, for terabyte/petabyte-scale databases, it's impossible or prohibitively expensive to fit everything in memory. Optimize the most frequently used data section.
*   Goal : Get 90% of users from cache, 10% from database with saving 2 to 4 milliseconds.

## 6. Cache Policy: Two Key Questions

*   **When to Update:**
    *   How to manage updates to the cache when the database is modified. Should you update at the same time? Should you update later?
    *   Strategies exist (write policies).
*   **What to Evict:**
    *   What data to remove from the cache when it overflows.
    *   Algorithms define what data gets kicked out of cache.
    *   Cache memory is limited, the database is much larger.
    *   If a new video is viral and is querering from users, then the cach moves that into the cach.

## 7. Common Cache Eviction Policies

*   Least Recently Used (LRU)
*   Least Frequently Used (LFU)

## 8. Potential Drawbacks of Caching

*   **Poor Hit Rate:** If the cache doesn't contain the data being queried, all that happens is a wasteful additional computation.
*   **Trashing:** *In what case does it occur?*
A client is querying data in a sequence like 1, 2, 3, 4 while the cache memory is limited to three elements. This is where evictions and loadings cause a sequence to be messed up.
*   **Eventual Consistency:** The data in the cache may be stale compared to the source of truth (the database).  Is for seeing if YouTube likes goes up per every minute. *What is financial transactions are running through a caching system?* This may cause problems like stale entries,

## 9. Cache Placement

*   **In-Memory Cache:** A map running alongside the application.
*   **Database Cache:** The database caches commonly used queries internally.
*   **Global (Distributed) Cache:** An external cache server queried by the rest of the services. Can scale independently, may be written in a different language, deployments are independent.
*   *Which one should you choose?* Typically, all three are applied.
*   As a software engineer, the primary concern will be *distributed cache*, due to its independent scaling, deployment, and sharing of logic across services.
*   Basically they save time but the caching policy matters depending on your system.

## 10. Conclusion

*Caching policy matters* and placement matters depending on your system. In other words, they save time. You need to make the right choice!