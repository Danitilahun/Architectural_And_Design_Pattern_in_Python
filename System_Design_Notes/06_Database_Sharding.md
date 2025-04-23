# Sharding: Scaling Your Database

![DATABASE SHARDING](./image/DATABASE%20SHARDING.png)

## 1. The Problem: Database Bottlenecks

*   Optimizing queries and indexing are insufficient for very large datasets.
*   NoSQL solutions might not always be appropriate.

## 2. Sharding Analogy: The Pizza

*   You can't eat an entire pizza alone, so you share it with friends by dividing it into slices.
*   Each friend gets a slice (partition) of the pizza.

## 3. Sharding Definition

*   Breaking up a database into smaller, more manageable pieces (shards).
*   Each shard resides on a separate database server.
*   Requests are routed to the appropriate shard based on some key (e.g., user ID).

## 4. Horizontal Partitioning

*   Sharding is a form of *horizontal partitioning*.
*   Horizontal partitioning depends on one key, which is an attribute of the data
    that you're storing to partition data.
*   Data is partitioned based on an attribute of the data being stored.
*   Contrast with *vertical partitioning*, which divides data based on columns.

## 5. Application vs. Database Servers

*   Sharding deals with *database servers* (where the actual data is stored).
*   Application servers are typically stateless.
*   Database servers prioritize *consistency*: ensuring that data is accurate and up-to-date.
*   Databases also strive for *availability* (uptime), but consistency is usually more important.

## 6. Sharding Key Selection

*   *What should you shard your data on?*
*   User ID (as used in the example).
*   Location (for location-based applications).

## 7. Benefits of Sharding

*   Improved performance: Queries operate on smaller datasets.
*   Faster performance because the database can only use a single shot.

## 8. Sharding Challenges

*   **Joins Across Shards:** Querying data that spans multiple shards can be expensive due to network communication.  Data needs to be pulled and joined from separate shards.
*   **Inflexibility:** The initial sharding scheme can be difficult to change. You can't change pizza slices.
*    You can't have dynamic number of shots.

## 9. Consistent Hashing for Dynamic Sharding

*   Consistent hashing (as discussed in previous videos) helps manage the assignment of data to shards in a dynamic way.
*   This approach allows the database to scale and shrink more easily.

## 10. Hierarchical Sharding

*   To overcome the inflexibility problem, a shard with too much data in it is dynamically broken into pieces.
*   A manager maps requests to the correct mini slice in pizza slice.

## 11. Shard-Level Indexing

*   Create indexes within each shard to further optimize query performance.
*   These indexes can be based on different attributes than the sharding key.
*   For example, if you shard by city ID, you can create an index on age within the New York shard.

## 12. Replication for Fault Tolerance (Master-Slave Architecture)

*   **Problem:** What happens if a shard fails?
*   **Solution:** Implement a master-slave architecture:
    *   Each shard has a master server and multiple slave servers.
    *   Writes are always directed to the master.
    *   Slaves replicate data from the master.
    *   Reads can be distributed across slaves.
    *   If the master fails, a slave is promoted to be the new master.

## 13. Sharding: Implementation Difficulties

*   Conceptually easy, but practically tough.
*   Maintaining data consistency is difficult.