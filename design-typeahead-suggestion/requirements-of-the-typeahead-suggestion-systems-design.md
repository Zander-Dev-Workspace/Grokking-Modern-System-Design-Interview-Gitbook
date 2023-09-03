# Requirements of the Typeahead Suggestion System’s Design

### Requirements <a href="#requirements-0" id="requirements-0"></a>

In this lesson, we look into the requirements and estimated resources that are necessary for the design of the typeahead suggestion system. Our proposed design should meet the following requirements.

#### Functional requirements <a href="#functional-requirements-1" id="functional-requirements-1"></a>

The system should suggest top �N (let’s say top ten) frequent and relevant terms to the user based on the text a user types in the search box.

#### Non-functional requirements <a href="#non-functional-requirements-2" id="non-functional-requirements-2"></a>

* **Low latency:** The system should show all the suggested queries in real time after a user types. The latency shouldn’t exceed 200 ms. A study suggests that the average time between two keystrokes is 160 milliseconds. So, our time-budget of suggestions should be greater than 160 ms to give a real-time response. This is because if a user is typing fast, they already know what to search and might not need suggestions. At the same time, our system response should be greater than 160 ms. However, it should not be too high because in that case, a suggestion might be stale and less useful.
* **Fault tolerance:** The system should be reliable enough to provide suggestions despite the failure of one or more of its components.
* **Scalability:** The system should support the ever-increasing number of users over time.

### Resource estimation <a href="#resource-estimation-0" id="resource-estimation-0"></a>

As was stated earlier, the typeahead feature is used to enhance the user experience while typing a query. We need to design a system that works on a scale that’s similar to Google Search. Google receives more than 3.5 billion searches every day. Designing such an enormous system is a challenging task that requires different resources. Let’s estimate the storage and bandwidth requirements for the proposed system.

#### Storage estimation <a href="#storage-estimation-1" id="storage-estimation-1"></a>

Assuming that out of the 3.5 billion queries per day, two billion queries are unique and need to be stored. Let’s also assume that each query consists of 15 characters on average, and each character takes 2 Bytes of storage. According to this formulation, we would require the following:

22 �������billion ×15×2=60��×15×2=60GB to store all the queries made in a day.

Storage required per year:

60��/���×365=21.9��/����60GB/day×365=21.9TB/year

Storage requirements for the typeahead suggestion system

#### Bandwidth estimation <a href="#bandwidth-estimation-0" id="bandwidth-estimation-0"></a>

3.5 billion queries will reach our system every day. Assume that each query a user types is 15 characters long on average.

Keeping this in mind, the total number of reading requests of characters per day would be as follows:

15×3.515×3.5 �������=52.5billion=52.5 �������billion characters per day.

Total read requests per second: 52.5�/86400≈0.607�52.5B/86400≈0.607M characters/sec. 86,400 is the number of seconds per day.

Since each character takes 2 Bytes, the bandwidth our system would need is as follows:

0.607�×2×8=9.7��/���0.607M×2×8=9.7Mb/sec

9.7��/���9.7Mb/sec is the incoming bandwidth requirement for queries that have a maximum length of 15 characters. Our system would suggest the top ten queries that are roughly of the same length as the query length after each character a user types. Therefore, the outgoing bandwidth requirement would become the following: 15×10×9.7��/���=1.46��/���15×10×9.7Mb/sec=1.46Gb/sec.

The total bandwidth required by the typeahead suggestion system

#### Number of servers estimation <a href="#number-of-servers-estimation-0" id="number-of-servers-estimation-0"></a>

Our system will receive 607,000 requests per second concurrently. Therefore, we need to have many servers installed to avoid burdening a single server. Let’s assume that a single server can handle 8,000 queries per second. So, we require around 76 servers to handle 607,000 queries.

607�/8000≈76607K/8000≈76 servers

Here, we only refer to the number of application servers. For simplicity, we ignored the number of cache and database servers. The actual number is higher than 76 because we would also need redundant servers to achieve availability.

The number of servers required for the typeahead suggestion system

In the table below, adjust the values to see how the resource estimations change.

**Resource Estimation for the Typeahead Suggestion System**

| Total Queries per Day         | 3.5    | billion            |
| ----------------------------- | ------ | ------------------ |
| Unique Queries per Day        | 2      | billion            |
| Minimum Characters in a Query | 15     | Characters         |
| Server's QPS                  | 8000   | Queries per second |
| Storage                       | f60    | GB/day             |
| Incoming Bandwidth            | f9.7   | Mb/sec             |
| Outgoing Bandwidth            | f1.455 | Gb/sec             |
| Number of Servers             | f76    | Severs             |

### Building blocks we will use <a href="#building-blocks-we-will-use-0" id="building-blocks-we-will-use-0"></a>

The design of the typeahead suggestion system consists of the following building blocks that have been discussed in the initial chapters of the course:

Building blocks required in the design of the typeahead suggestion system

* [**Databases**](../databases/introduction-to-databases.md) are required to keep the data related to the queries’ prefixes.
* [**Load balancers**](../load-balancers/introduction-to-load-balancers.md) are required to disseminate incoming queries among a number of active servers.
* [**Caches**](../distributed-cache/system-design-the-distributed-cache.md) are used to keep the top �N suggestions for fast retrieval.

In the next lesson, we’ll focus on the high-level design and APIs of the typeahead suggestion system.
