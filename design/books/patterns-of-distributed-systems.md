# Patterns of Distributed Systems

# Data Replication
- Write-Ahead Log

- Replication with Leader and Followers

- Heartbeat

- Elections when heartbeat timeout

- Generation clock: to associate generation id (changes when leader changes) to log entries, and be able to recognize issues with leader changing more than one

- Commit only by majority quorum

- Elections only by majority quorum

- High-Water Mark: index of the latest update to be committed. The leader provides this on it's HeartBeat, for followers to commit the indexes.

- Raft: Replicated log algorithm, uses most up-to-date replica

- Single Update Queue: to avoid blocking with processing of log entries and also concurrency issues. This allows to remain responsive to clients.

- Request Waiting List: list of clients, waiting to complete processing to send ackowledge of completion

- Idempotent Receiver: to avoid executing a retried request.
Use clientId + unique request number to achieve idempotence.
Clusters need to register a client to generate it's ID.

- Leader can use a Single-Socket Channel with follower to avoid out-of-order messages

## Followers can handle read requests to reduce load on leader
This frees the leader for more writes for example, but comes at the price of the leader possibly not being up-to-date.
A wait to tackle this is to use a Versioned Value, storing a version number with the record.
Thus replica can wait for version to be updated and not returning stale data while not receiving data from leader.

## A Large amount of data can be partitioned over multiple nodes
The data can be separated into partitions (also called shards) on different nodes.

Here are the key requirements for any partitioning scheme:
- Data should be evenly distributed across all the cluster nodes.
- It should be possible to know which cluster node stores a particular data record, without making a request to all the nodes.
- It should be quick and easy to move part of the data to the new nodes.

Hash values for keys make sure that data is evenly distributed. If the number of partitions is known, can use:
`partition = hash_of_key % no. of partitions`

Changing the number of partitions causes the partition for every record to change, which requires moving all the data records across the cluster.
This is definitely a no-no when we are dealing with large amount of data.
A common pattern is to define logical partitions (more than nodes).
To find a node for a record, first get the logical partition, then look up the nodes for the partition. 
The logical partition doesn't need to change; when adding a node to the cluster, we reassign some of the logical partitions to it,
which only moves the records for that partition.

The most straightforward form of using this is Fixed Partitions.
For example, Akka suggests having `n-partitions = 10 * n-nodes`, Apache Ignite has 1024.
If there are queries for range of values (example cities starting with p to r), Key-Range Partitions could be used, but it has it's own challenges.

## Partitions can/should be replicated for resilience
Same replica concept from before.
3 or 5 replicas strike a balance between good performance (also considering Majority Quorum) and fault tolerance.

## A Minimum of Two Phases Are Needed to Maintain Consistency across Partitions
Introducing partitions adds complexity for operations with multiple partitions, and we can use `Two-Phase Commit` to achieve consistency across partitions.
We can use a Write-Ahead Log for Transactions.
Typically the node hosting the partition for the first key of the operation is made the coordinator.

## In Distributed Systems, Ordering Cannot Depend on System Timestamps
To track the order of requests across cluster nodes without relying on system timestamps, we can use a Lamport Clock, which employs a simple integer counter per node. This counter is passed along in requests and responses. However, basic Lamport Clocks track versions with integers unrelated to actual timestamps, which is problematic for databases needing timestamp-based versions for user queries.

To address this, a `Hybrid Clock` combines clock time with a Lamport Clock. When nodes send messages, they include the Hybrid Clock, which merges the current server time with a Lamport Clock counter. If a node receives a message with a timestamp ahead of its clock, it increments its Hybrid Clock's integer counter to ensure its operations occur later than the received message.

To address the problem of partial order in a distributed system, where different nodes might have lagging clocks and thus return outdated values, we can use the `Clock-Bound Wait` technique, which involves waiting before storing a value to ensure that all cluster nodes' clocks have advanced beyond the timestamp assigned to the records. This helps maintain a consistent view of the data across all nodes.
With the Clock-Bound Wait approach, every node waits for the maximum clock skew, ensuring that any request on any cluster node sees the latest values regardless of their own clock values.


# A Consistent Core Can Manage the Membership of a Data Cluster
A cluster can have hundreds or thousands of nodes, which can be also dynamic (adding/removing). 
To manage such a cluster, we need to keep track of which nodes are part of the cluster. 
Replicated Log is an excellent way to achieve this, but it depends on Majority Quorum, which cannot scale to thousands of replicas. 

Managing a large cluster should be given to a `Consistent Core`, a small set of nodes to manage it.
The Consistent Core tracks the data cluster membership with Lease and State Watch.
Example: `Apache ZooKeeper` and `etcd`.


# Gossip Dissemination for Decentralized Cluster Management
Some systems, such as Cassandra, lean more towards eventual consistency, and do not want to rely on a centralized Consistent Core.
At regular intervals, each node picks another node at random and sends it the information it has on the state of the cluster.