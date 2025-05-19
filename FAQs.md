# FAQs

1. [What are the primary use cases for ClickHouse?](#what-are-the-primary-use-cases-for-clickhouse)
2. [Why is ClickHouse fast for analytical queries?](#why-is-clickhouse-fast-for-analytical-queries)
3. [What are the hardware requirements?](#what-are-the-hardware-requirements)
4. [Is ClickHouse SQL or NoSQL?](#is-clickhouse-sql-or-nosql)
5. [What are the main benefits of ClickHouse?](#what-are-the-main-benefits-of-clickhouse)
6. [Is ClickHouse an OLAP database?](#is-clickhouse-an-olap-database)
7. [How does ClickHouse compare to MySQL?](#how-does-clickhouse-compare-to-mysql)
8. [What is the MergeTree engine?](#what-is-the-mergetree-engine)
9. [Can ClickHouse update or delete data?](#can-clickhouse-update-or-delete-data)
10. [How does ClickHouse integrate with external systems?](#how-does-clickhouse-integrate-with-external-systems)
11. [Is ClickHouse ACID compliant?](#is-clickhouse-acid-compliant)
12. [How does ClickHouse handle replication?](#how-does-clickhouse-handle-replication)

---

### What are the primary use cases for ClickHouse?

- Real-time analytics dashboards
- Log analysis and SIEM
- Business Intelligence (BI) acceleration
- AdTech and time-series analysis
- Product analytics and observability platforms

ClickHouse excels at fast analysis on large, often append-only datasets.

### Why is ClickHouse fast for analytical queries?

- **Columnar Storage:** Reads only required columns, reducing I/O.
- **Vectorized Execution:** Processes data in batches using SIMD instructions.
- **Data Compression:** Uses general and specialized codecs to minimize storage.
- **Sparse Primary & Skipping Indices:** Skips irrelevant data blocks.
- **Parallel Processing:** Leverages multiple CPU cores and distributed servers.
- **Hardware Optimization:** Written in C++ for efficient hardware utilization.

### What are the hardware requirements?

- **Minimum RAM:** 8GB–16GB for basic workloads; production deployments often use 32GB, 64GB, or more per node.
- **Note:** Actual requirements depend on dataset size, query complexity, and concurrency.

### Is ClickHouse SQL or NoSQL?

- **SQL:** ClickHouse uses its own SQL dialect for queries and schema.
- **Integration:** Can connect to NoSQL systems, but is not itself NoSQL.

### What are the main benefits of ClickHouse?

- Extreme speed for OLAP queries on large datasets
- High data compression
- Horizontal scalability and open-source licensing
- Fault tolerance via replication
- Cost-effectiveness, especially for open-source deployments

### Is ClickHouse an OLAP database?

- **Yes:** ClickHouse is designed and optimized for OLAP (Online Analytical Processing).

### How does ClickHouse compare to MySQL?

- **ClickHouse:** Best for OLAP analytics (large, complex queries).
- **MySQL:** Best for OLTP (frequent small reads/writes, strict ACID).
- **Usage:** Often deployed together for complementary workloads.

### What is the MergeTree engine?

- Primary storage engine family for OLAP workloads
- Features:
  - Columnar storage
  - Data sorted by primary key
  - Immutable data parts with background merging
  - Sparse primary indexing
  - Replication support
  - Variants for deduplication (ReplacingMergeTree) and pre-aggregation (AggregatingMergeTree)

### Can ClickHouse update or delete data?

- **Yes, but differently from OLTP systems:**
  - `ALTER TABLE ... UPDATE/DELETE`: Asynchronous, rewrites data parts (heavy operation)
  - `DELETE FROM ... WHERE`: Marks rows as deleted; physical removal occurs during merges

### How does ClickHouse integrate with external systems?

- **Table Functions/Engines:** Connect to SQL/NoSQL databases, S3, Kafka, HDFS, etc.
- **Data Formats:** Supports CSV, JSON, Parquet, ORC, and more.
- **Compatibility:** MySQL/PostgreSQL wire protocols for tool integration.
- **Dictionaries:** Fast key-value enrichment from external sources.
- **Client APIs:** Native TCP/HTTP, drivers for Python, Java, Go, JDBC/ODBC.

### Is ClickHouse ACID compliant?

- **Not fully:** Provides snapshot isolation for reads and atomicity for single INSERTs.
- **Limitations:** No multi-statement transactions; durability settings favor performance over immediate fsync.

### How does ClickHouse handle replication?

- **Asynchronous multi-master replication** via ReplicatedMergeTree engines
- **Coordination:** Uses ClickHouse Keeper (Raft protocol) to log and synchronize operations across replicas
- **Consistency:** Replicas fetch missing parts or replay operations to converge state
