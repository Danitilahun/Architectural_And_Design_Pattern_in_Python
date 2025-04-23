# NoSQL Databases: When and Why

This explanation dives into NoSQL databases, discussing their use cases, advantages, disadvantages, and how they work.

## 1. SQL vs. NoSQL

*   **SQL Example (Person Schema):**
    *   id (user_id)
    *   name
    *   address (foreign key to address table)
    *   age
    *   role
    *   Separate address table with: address_id, city, country, district.
*   **NoSQL Example:**
    *   id
    *   One large J ss o n blob:
        *   name: John Doe
        *   address: { id, city, country }
        *   age
        *   role
* What is it that makes NoSQL so Efficient?

## 2. Why NoSQL Can Be More Efficient

*   **Data Storage Patterns:** Usually a user is registering with all their information so single insert. Select start are most common.
*Usually to need is all the info about data at all times*
*   **Locality:** All relevant data is contained together in one block.
*It is cheaper here.*

## 3. NoSQL Advantages

*   **Easier to Insert/Retrieve:** All relevant data in one block.
*   **Flexible Schema:** Doesn't enforce a fixed schema. New attributes can be added without modifying the database structure. No need of adding new columns to DB and no need of locks on the table.
*If address is entirely blanck that's fine because it uses JSON
*   **Horizontal Partitioning (Built-in):** Designed for scale and focused on availability. This provides nice scale and you also want to keep them together
*   **Built for Aggregations:** Optimized for finding metrics and getting intelligent data (average age, total salary).

## 4. NoSQL Disadvantages

*   **Not Read Optimized:**
    *   Finding all the ages requires reading every block.
    *   Can't extract info between all different tables
*   **Asset is not guaranteed** You cant have the same transactions if it was not.
*   **Inherent Redundancy or Aggregations:** Not to many updates to the DB is not nice. There are not implicit relations or information because R stands for relation.
*   **Relations are not implicit.**
*  **Joins are hard**. Since you need to run the blocks the intelligent is not behind it.

## 5. When to Use NoSQL

* It depends on these thinks
*If the data has to be all together then NoSQL may be the way to go.*
*There is are lot of rights are coming then NoSQL can be used for inherent requirements*
*It all depends on the above said information, look at these before going through with using it.*

## 6. Example: Cassandra Architecture

*   Cassandra cluster with five nodes.
*   Expensive to host a Cassandra cluster.

## 7. Request Routing

*   Requests have IDs.
*   The requests ids may not be alway numerical, and they have some kind of name, like a person
*   Keys are used rather than IDs in NoSQL databases.
*   Hash the key to map the request to a node: `node = H(key) mod N`
*Hashing ensures is distributed evenly
*What this make sure is all notes can get to the full capacity instead of to much preassure
*Hash( 1, 2, 3 ) is passed through a hash function and gets mapped to 256
*The note has a clock wise function.*

## 8. Load Balancing & Hash Function Quality

*   Uniform distribution is achieved if hash is nice.
*If the has function is not so nice, it can use cluster where there can be other 5 points

## 9. Redundancy

*   Replicate data to multiple nodes.
* If hashing is good then redundancy comes automatically.

## 10. Distributed Consensus (Quorum)

*   Need a mechanism to agree on a value to return to the user if the application factor is the reason if node can't process.
*Need  node, need to make sure all three nodes has the same amount of data to run.
*   Nodes copy data.
*Quorum is a way which data has to accept what you are about to give in that point*
*   Use timestamps to determine the latest version of the data.
* This process, Cassandra must return a database error to that something is wrong.
    * They have to pick the date to show the process.

## 11. Data Storage

*   Requests sent to Cassandra are put in memory as a *log file* - all the requests will be wrote in the file.
*   Cassandra takes a key value pair.
*Cassandra knows where it wants to do, this process can be fast.*
*   Periodically, this memory is dumped into an *SSTable* (Sorted String Table).
*Sorted string tables it's not going to be change so if the can be flushed to that it will be nice."
*They have have similar strings, so what cassandra do is have this data*
*This was created to do BITS data structure, a google process.*

## 12. Updates & Compaction

*   Updates result in new records (not overwrites).
* This one make sure it can be change through time stamped with each string
* The thing is it will save storage with the duplicate key so what it does is take space usage.
*So it takes less string tables.*
*   Compaction merges SSTables to remove duplicate records and tombstones.

## 13. Tombstones

*   When a record is deleted, a *tombstone* is placed in the SSTable.
*   Tombstone flags in order to the last stamp.
*   Tombstones can result in the system returning an error.

## 14. Extensible Concepts

These concepts used with Elastic Search and also Amazon Dynamo db.