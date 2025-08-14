# Database Cheat Sheet — Types, Protocols & Ports

| **Database Type** | **Example Database** | **Protocol** | **Default Port** |
|-------------------|----------------------|--------------|------------------|
| **Relational (RDBMS)** | MySQL / MariaDB | MySQL Protocol (TCP) | 3306 |
|                   | PostgreSQL | PostgreSQL Protocol (TCP) | 5432 |
|                   | Oracle Database | Oracle Net (TCP) | 1521 |
|                   | Microsoft SQL Server | Tabular Data Stream (TDS) | 1433 |
|                   | SQLite | File-based (No network protocol) | N/A |
| **Document (NoSQL)** | MongoDB | MongoDB Wire Protocol (TCP) | 27017 |
|                     | CouchDB | HTTP/REST (TCP) | 5984 |
|                     | Amazon DocumentDB | MongoDB Wire Protocol (TCP) | 27017 |
| **Key-Value Store (NoSQL)** | Redis | Redis Protocol (TCP) | 6379 |
|                            | Memcached | Memcached Protocol (TCP/UDP) | 11211 |
|                            | Amazon DynamoDB | HTTP/HTTPS (TCP) | 443 |
| **Wide-Column Store (NoSQL)** | Apache Cassandra | Native Protocol (TCP) | 9042 |
|                              | HBase | Thrift / REST | 9090 (Thrift), 8080 (REST) |
| **Graph Database** | Neo4j | Bolt Protocol (TCP) | 7687 |
|                    | Amazon Neptune | Bolt / SPARQL over HTTPS | 8182 / 443 |
|                    | TigerGraph | REST / GSQL Protocol | 14240 (REST API) |
| **Object-Oriented Database** | db4o | Custom Binary Protocol | N/A |
|                             | ObjectDB | Java/JPA Protocol | N/A |
| **Cloud Database** | AWS RDS (MySQL) | MySQL Protocol (TCP) | 3306 |
|                    | Azure SQL Database | TDS Protocol (TCP) | 1433 |
|                    | Google Cloud Spanner | gRPC / HTTPS | 443 |
| **Time Series Database** | InfluxDB | HTTP API (TCP) | 8086 |
|                          | TimescaleDB | PostgreSQL Protocol (TCP) | 5432 |
|                          | Prometheus | HTTP/REST (TCP) | 9090 |
| **Vector Database** | Pinecone | HTTPS API | 443 |
|                     | Milvus | gRPC / HTTP | 19530 (gRPC), 19121 (HTTP) |
|                     | Weaviate | HTTP/REST (TCP) | 8080 |
| **Hierarchical Database** | IBM IMS | Proprietary Protocol | N/A |
| **Network Database** | IDMS | Proprietary Protocol | N/A |
| **Distributed Database** | Google Spanner | gRPC / HTTPS | 443 |
|                          | CockroachDB | PostgreSQL Wire Protocol (TCP) | 26257 |
|                          | YugabyteDB | PostgreSQL / CQL Protocols | 5433 (Postgres), 9042 (CQL) |
| **Multi-Model Database** | ArangoDB | HTTP/REST (TCP) | 8529 |
|                          | OrientDB | Binary / HTTP Protocol | 2424 (Binary), 2480 (HTTP) |
| **Search Engine DB** | Elasticsearch | HTTP/REST (TCP) | 9200 (REST), 9300 (Transport) |
|                      | Apache Solr | HTTP/REST (TCP) | 8983 |
| **Columnar Database** | ClickHouse | Native Protocol / HTTP | 9000 (Native), 8123 (HTTP) |
|                       | Amazon Redshift | PostgreSQL Protocol (TCP) | 5439 |
|                       | Google BigQuery | HTTPS (TCP) | 443 |
|                       | Snowflake | HTTPS (TCP) | 443 |
