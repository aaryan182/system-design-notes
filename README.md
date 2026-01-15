# System Design Knowledge Base

## Table of Contents

1. [About System Design](#1-about-system-design)
2. [Approach to System Design](#2-approach-to-system-design)
3. [Building Good Systems](#3-building-good-systems)
4. [Relational Databases](#4-relational-databases)
5. [Database Isolation Levels](#5-database-isolation-levels)
6. [Scaling Databases](#6-scaling-databases)
7. [Sharding and Partitioning](#7-sharding-and-partitioning)
8. [Non-Relational Databases](#8-non-relational-databases)
9. [Picking the Right Database](#9-picking-the-right-database)
10. [Caching Fundamentals](#10-caching-fundamentals)
11. [Populating Cache](#11-populating-cache)
12. [Caching at Different Levels](#12-caching-at-different-levels)
13. [Message Brokers and Queues](#13-message-brokers-and-queues)
14. [Message Streams and Kafka](#14-message-streams-and-kafka)
15. [Pub/Sub Systems](#15-pubsub-systems)

---

## Overview

This repository contains comprehensive notes and concepts related to System Design, covering fundamental principles, database technologies, caching strategies, and asynchronous communication patterns. Each topic is organized into dedicated directories with detailed explanations.

```mermaid
graph TD
    A[System Design] --> B[Foundational Concepts]
    A --> C[Database Systems]
    A --> D[Caching Strategies]
    A --> E[Messaging Systems]
    
    B --> B1[What is System Design]
    B --> B2[Approach & Methodology]
    B --> B3[Good System Principles]
    
    C --> C1[Relational Databases]
    C --> C2[Non-Relational Databases]
    C --> C3[Database Selection]
    C --> C4[Isolation Levels]
    C --> C5[Scaling Techniques]
    C --> C6[Sharding & Partitioning]
    
    D --> D1[Caching Fundamentals]
    D --> D2[Cache Population]
    D --> D3[Multi-Level Caching]
    
    E --> E1[Message Brokers & Queues]
    E --> E2[Message Streams & Kafka]
    E --> E3[Pub/Sub Systems]
    
    style A fill:#f9f,stroke:#333,stroke-width:4px
    style B fill:#bbf,stroke:#333,stroke-width:2px
    style C fill:#bfb,stroke:#333,stroke-width:2px
    style D fill:#fbb,stroke:#333,stroke-width:2px
    style E fill:#ffb,stroke:#333,stroke-width:2px
```

---

## 1. About System Design

**Location:** `01-about_SD/aboutSD.txt`

### What is System Design?

System Design is the process of defining the architecture, components, and modules of a system to satisfy specified requirements. It is essentially product development at a technical level.

```mermaid
flowchart LR
    A[Set of Requirements] --> B[Architecture Design]
    B --> C[Component Definition]
    C --> D[Module Design]
    D --> E[Interaction Pattern]
    E --> F[Problem Solution]
    
    style A fill:#e1f5ff,stroke:#01579b
    style F fill:#c8e6c9,stroke:#2e7d32
```

### Core Principles

Every tech product is a system that has been designed. When designing a system, engineers must:

1. **Break Down Problems**: Decompose complex problem statements into solvable sub problems
2. **Define Components**: Decide on key components and their responsibilities
3. **Establish Boundaries**: Clearly define the boundaries of each component
4. **Address Scalability**: Touch upon key challenges in scaling the system
5. **Ensure Reliability**: Make architecture fault-tolerant and available

### System Design Process

```mermaid
graph TD
    A[Requirements] --> B{Break Down Problem}
    B --> C[Identify Components]
    C --> D[Define Responsibilities]
    D --> E[Set Component Boundaries]
    E --> F[Address Scaling Challenges]
    F --> G[Ensure Fault Tolerance]
    G --> H[Ensure Availability]
    H --> I[Complete System Design]
    
    style A fill:#fff3e0,stroke:#e65100
    style I fill:#c8e6c9,stroke:#2e7d32
```

### Key Takeaways

- System Design is the bridge between requirements and implementation
- Every component interaction must be carefully planned
- The process is iterative and practical
- Focus on solving real world problems at scale

---

## 2. Approach to System Design

**Location:** `02-approachSD/approachSD.txt`

### Structured Methodology

System Design is extremely practical and requires a structured approach. The key is to take small, deliberate steps rather than attempting to solve everything at once.

```mermaid
flowchart TD
    START[Start System Design] --> A[Understand Problem Statement]
    A --> B{Problem Clear?}
    B -->|No| A
    B -->|Yes| C[Break into Components]
    C --> D[Dissect Each Component]
    D --> E[Analyze Sub-Components]
    E --> F{More Components Needed?}
    F -->|Yes| C
    F -->|No| G[Design Complete]
    
    style START fill:#e1bee7,stroke:#4a148c
    style G fill:#c8e6c9,stroke:#2e7d32
```

### Step-by-Step Process

#### Step 1: Understand the Problem Statement

Without a thorough understanding of the problem at hand, the design process would easily digress. Invest time in clarifying requirements and constraints.

#### Step 2: Break Down into Components

- Do not create components for the sake of it
- Create only components that are essential
- Start with the must have components

#### Step 3: Dissect Each Component

For each component or sub-component, analyze the following aspects:

```mermaid
mindmap
  root((Component Analysis))
    Database
      Schema Design
      Query Patterns
      Transactions
    Caching
      Cache Strategy
      Invalidation
      TTL
    Scaling
      Vertical
      Horizontal
      Load Distribution
    Fault Tolerance
      Redundancy
      Failover
      Recovery
    Async Processing
      Message Queues
      Workers
      Delegation
    Communication
      APIs
      Protocols
      Data Format
```

#### Step 4: Iterate

- Repeat the analysis for each sub component one by one
- Add more sub components if needed during the iteration
- Refine the design based on new insights

### Design Checklist

For each component, ensure you cover:

1. **Database and Caching**: Data storage and retrieval strategies
2. **Scaling**: Horizontal and vertical scaling approaches
3. **Fault Tolerance**: Handling failures gracefully
4. **Async Processing**: Delegation and background jobs
5. **Communication**: Inter component communication patterns

---

## 3. Building Good Systems

**Location:** `03-good-system/goodSystem.txt`

### When to Stop Evolving

Every system is "infinitely" buildable, meaning there's always room for improvement. However, knowing when to stop the evolution is crucial for practical delivery.

### Key Indicators of a Good System

```mermaid
graph LR
    A[Good System] --> B[Proper Decomposition]
    A --> C[Clear Responsibilities]
    A --> D[Technical Details]
    A --> E[Component Properties]
    
    B --> B1[Broken into Components]
    C --> C1[Exclusive Responsibilities]
    D --> D1[Slight Technical Details]
    E --> E1[Scalable]
    E --> E2[Fault Tolerant]
    E --> E3[Available]
    
    style A fill:#ffeb3b,stroke:#f57f17,stroke-width:3px
    style E1 fill:#c8e6c9,stroke:#2e7d32
    style E2 fill:#c8e6c9,stroke:#2e7d32
    style E3 fill:#c8e6c9,stroke:#2e7d32
```

### Four Essential Pointers

#### 1. System Decomposition

The system should be broken down into logical, manageable components. Each component should represent a distinct functional area.

#### 2. Exclusive Responsibilities

Every component must have a clear set of responsibilities that do not overlap with other components. This ensures:
- Clear ownership
- Easier debugging
- Independent development
- Better maintainability

#### 3. Technical Details Figured Out

For each component, slight technical details should be determined, including:
- Technology stack
- Data models
- API contracts
- Communication protocols

#### 4. Component Isolation Properties

Each component, when analyzed in isolation, must be:

**Scalable (Horizontally)**
- Can handle increased load by adding more instances
- Not limited by single-machine constraints

**Fault Tolerant**
- Gracefully handles failures
- Has redundancy mechanisms
- Can recover from errors

**Available**
- High uptime guarantees
- Minimal single points of failure
- Proper failover mechanisms

```mermaid
graph TD
    A[Component in Isolation] --> B{Is it Scalable?}
    B -->|Yes| C{Is it Fault Tolerant?}
    B -->|No| X[Redesign]
    C -->|Yes| D{Is it Available?}
    C -->|No| X
    D -->|Yes| E[Good Component]
    D -->|No| X
    
    style E fill:#c8e6c9,stroke:#2e7d32
    style X fill:#ffcdd2,stroke:#c62828
```

---

## 4. Relational Databases

**Location:** `04-relationDB/relationalDatabases.txt`

### Overview

Databases are the most critical component of any system. They make or break a system. Relational databases store and represent data in rows and columns, providing strong transactional guarantees.

### ACID Properties

Relational databases provide ACID transactions, which are fundamental to data integrity:

```mermaid
graph TD
    A[ACID Properties] --> B[Atomicity]
    A --> C[Consistency]
    A --> D[Isolation]
    A --> E[Durability]
    
    B --> B1[All statements within a transaction<br/>takes effect or none]
    C --> C1[Data will never go incorrect<br/>Constraints, Cascades, Triggers]
    D --> D1[Determines how much changes<br/>of one transaction are visible to other]
    E --> E1[When transaction commits<br/>the changes outlive]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#fff9c4,stroke:#f57f17
    style E fill:#fff9c4,stroke:#f57f17
```

### ACID Explained

#### Atomicity
All statements within a transaction take effect or none. If any part of the transaction fails, the entire transaction is rolled back.

#### Consistency
Data will never go incorrect no matter what. This is enforced through:
- Constraints (Primary keys, Foreign keys, Unique constraints)
- Cascades (ON DELETE CASCADE, ON UPDATE CASCADE)
- Triggers (Automated actions on data changes)

#### Isolation
When multiple transactions are executing in parallel, the isolation level determines how much changes of one transaction are visible to others. Isolation has 4 levels (covered in detail in section 5).

#### Durability
When a transaction commits, the changes outlive system failures. Data is persisted to disk and survives crashes.

### When to Pick Relational Databases

Choose relational databases when you need:
- Strong ACID guarantees
- Complex relationships between entities
- Data integrity and correctness
- Complex queries with joins
- Transactional consistency

```mermaid
flowchart LR
    A[Data Requirements] --> B{Need Relations?}
    B -->|Yes| C{Need ACID?}
    B -->|No| D[Consider NoSQL]
    C -->|Yes| E[Relational Database]
    C -->|No| D
    
    style E fill:#c8e6c9,stroke:#2e7d32
    style D fill:#fff9c4,stroke:#f57f17
```

---

## 5. Database Isolation Levels

**Location:** `05-DB_Isolation_levels/isolation_levels.txt`

### Overview

Relational databases provide ACID guarantees and the 'I' in ACID stands for Isolation. Isolation levels help us tune how transactions interact with each other, dictating how much one transaction knows about the other.

### The Four Isolation Levels

```mermaid
graph TD
    A[Isolation Levels] --> B[Read Uncommitted]
    A --> C[Read Committed]
    A --> D[Repeatable Read]
    A --> E[Serializable]
    
    B --> B1[Lowest Isolation<br/>Highest Performance<br/>Dirty Reads Possible]
    C --> C1[Reads committed values<br/>Non-repeatable reads]
    D --> D1[Default Level<br/>Consistent reads within transaction]
    E --> E1[Highest Isolation<br/>Lowest Performance<br/>Locking reads]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#ffcdd2,stroke:#c62828
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#c8e6c9,stroke:#2e7d32
    style E fill:#bbdefb,stroke:#1976d2
```

### Detailed Explanation

#### 1. Read Uncommitted
- **Behavior**: Reads even uncommitted values from other transactions
- **Consequence**: "Dirty reads" - reading data that might be rolled back
- **Use Case**: Rarely used due to data integrity risks
- **Performance**: Fastest, no locking overhead

#### 2. Read Committed
- **Behavior**: Reads within the same transaction always read fresh committed values
- **Consequence**: Multiple reads within the same transaction can be inconsistent
- **Use Case**: When you need fresh data on every read
- **Performance**: Good performance with reasonable consistency

#### 3. Repeatable Read (Default)
- **Behavior**: Consistent reads within the same transaction
- **Consequence**: Even if other transactions commit, the first transaction will not see the changes (if value already read)
- **Use Case**: Default for most applications requiring consistency
- **Performance**: Balanced performance and consistency

#### 4. Serializable
- **Behavior**: Every read is a locking read; while one transaction reads, others must wait
- **Consequence**: Complete isolation but significantly slower
- **Use Case**: Critical operations requiring absolute consistency
- **Performance**: Slowest, maximum locking
- **Note**: Implementation depends on the database engine

### Isolation Level Comparison

```mermaid
sequenceDiagram
    participant T1 as Transaction 1
    participant DB as Database
    participant T2 as Transaction 2
    
    Note over T1,T2: Repeatable Read Example
    T1->>DB: BEGIN TRANSACTION
    T1->>DB: SELECT balance WHERE id=1<br/>(reads 100)
    T2->>DB: BEGIN TRANSACTION
    T2->>DB: UPDATE balance=200 WHERE id=1
    T2->>DB: COMMIT
    T1->>DB: SELECT balance WHERE id=1<br/>(still reads 100)
    T1->>DB: COMMIT
    
    Note over T1,T2: Read Committed Example
    T1->>DB: BEGIN TRANSACTION
    T1->>DB: SELECT balance WHERE id=1<br/>(reads 100)
    T2->>DB: BEGIN TRANSACTION
    T2->>DB: UPDATE balance=200 WHERE id=1
    T2->>DB: COMMIT
    T1->>DB: SELECT balance WHERE id=1<br/>(now reads 200)
    T1->>DB: COMMIT
```

### Choosing the Right Isolation Level

| Isolation Level | Dirty Reads | Non-Repeatable Reads | Phantom Reads | Performance |
|----------------|-------------|---------------------|---------------|-------------|
| Read Uncommitted | Yes | Yes | Yes | Highest |
| Read Committed | No | Yes | Yes | High |
| Repeatable Read | No | No | Yes | Medium |
| Serializable | No | No | No | Lowest |

---

## 6. Scaling Databases

**Location:** `06-scalingDB/scalingDB.txt`

### Overview

Databases are the most important component of any system. They make or break the system. Understanding how to scale databases is critical for building robust, high performance applications. These techniques are applicable to most databases.

### Scaling Strategies

```mermaid
graph TD
    A[Database Scaling] --> B[Vertical Scaling]
    A --> C[Horizontal Scaling]
    
    B --> B1[Add CPU]
    B --> B2[Add RAM]
    B --> B3[Add Disk]
    
    C --> C1[Read Replicas]
    C --> C2[Sharding]
    
    C1 --> C1A[Synchronous Replication]
    C1 --> C1B[Asynchronous Replication]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#c8e6c9,stroke:#2e7d32
```

### 1. Vertical Scaling

**Approach**: Add more CPU, RAM and Disk to the database server

**Advantages**:
- Simple to implement
- No code changes required
- Gives ability to handle more load

**Disadvantages**:
- Requires downtime during reboot
- Has physical hardware limitations
- Eventually becomes cost prohibitive
- Single point of failure remains

```mermaid
graph LR
    A[Database Server<br/>4 CPU, 8GB RAM] -->|Upgrade| B[Database Server<br/>8 CPU, 16GB RAM]
    B -->|Upgrade| C[Database Server<br/>16 CPU, 32GB RAM]
    C -->|Limit Reached| D[Cannot Scale Further<br/>Need Horizontal Scaling]
    
    style A fill:#fff9c4,stroke:#f57f17
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#ffcdd2,stroke:#c62828
    style D fill:#ffcdd2,stroke:#c62828
```

### 2. Horizontal Scaling - Read Replicas

**When to Use**: When read:write ratio is approximately 90:10

**Approach**: 
- Move reads to replica databases
- Keep master database free for writes
- API servers must know which database to connect to

```mermaid
graph TD
    API[API Servers] --> M[Master Database<br/>Handles Writes]
    API --> R1[Read Replica 1]
    API --> R2[Read Replica 2]
    API --> R3[Read Replica 3]
    
    M -->|Replication| R1
    M -->|Replication| R2
    M -->|Replication| R3
    
    style M fill:#ffeb3b,stroke:#f57f17,stroke-width:2px
    style R1 fill:#c8e6c9,stroke:#2e7d32
    style R2 fill:#c8e6c9,stroke:#2e7d32
    style R3 fill:#c8e6c9,stroke:#2e7d32
```

### Replication Modes

#### Synchronous Replication
- **Consistency**: Strong consistency
- **Replication Lag**: Zero replication lag
- **Write Performance**: Slower writes (must wait for replicas)
- **Use Case**: When consistency is critical

#### Asynchronous Replication
- **Consistency**: Weak (eventual) consistency
- **Replication Lag**: Some replication lag exists
- **Write Performance**: Faster writes (no waiting)
- **Use Case**: When performance is prioritized over immediate consistency

```mermaid
sequenceDiagram
    participant Client
    participant Master
    participant Replica
    
    Note over Client,Replica: Synchronous Replication
    Client->>Master: WRITE data
    Master->>Master: Write to disk
    Master->>Replica: Replicate data
    Replica->>Replica: Write to disk
    Replica->>Master: ACK
    Master->>Client: SUCCESS
    
    Note over Client,Replica: Asynchronous Replication
    Client->>Master: WRITE data
    Master->>Master: Write to disk
    Master->>Client: SUCCESS (immediate)
    Master->>Replica: Replicate data (async)
    Replica->>Replica: Write to disk
```

### 3. Horizontal Scaling - Sharding

**When to Use**: When one node cannot handle the data volume or load

**Approach**:
- Split data into multiple exclusive subsets
- Each write on a particular row/document goes to one specific shard
- Shards are independent (no replication between them)
- API server needs to know which shard to connect to

**Note**: Some databases have a proxy that handles routing automatically

```mermaid
graph TD
    API[API Servers] --> Router[Router/Proxy]
    Router --> S1[Shard 1<br/>Users 1-1000]
    Router --> S2[Shard 2<br/>Users 1001-2000]
    Router --> S3[Shard 3<br/>Users 2001-3000]
    
    S1 --> S1R1[Replica]
    S1 --> S1R2[Replica]
    S2 --> S2R1[Replica]
    S3 --> S3R1[Replica]
    
    style Router fill:#64b5f6,stroke:#1976d2
    style S1 fill:#ffeb3b,stroke:#f57f17
    style S2 fill:#ffeb3b,stroke:#f57f17
    style S3 fill:#ffeb3b,stroke:#f57f17
```

### Scaling Strategy Comparison

| Strategy | Complexity | Cost | Scalability | Downtime | Consistency |
|----------|-----------|------|-------------|----------|-------------|
| Vertical Scaling | Low | High | Limited | Yes | Strong |
| Read Replicas | Medium | Medium | High (reads) | No | Configurable |
| Sharding | High | Medium | Very High | No | Eventually Consistent |

### Best Practices

1. **Start with vertical scaling** for simplicity
2. **Add read replicas** when read-heavy workload increases
3. **Implement sharding** when single node cannot handle the load
4. **Each shard can have its own replicas** for redundancy and read scaling
5. **Monitor replication lag** in asynchronous setups
6. **Plan shard key carefully** to ensure even distribution

---

## 7. Sharding and Partitioning

**Location:** `07-shardingAndPartitioning/sAndp.txt`

### Terminology

**Sharding**: Method of distributing data across multiple machines

**Partitioning**: Splitting a subset of data within the same instance

**Key Distinction**: Overall, a database is sharded while the data is partitioned.

### How Database Scaling Works

```mermaid
graph TD
    A[Database Server<br/>EC2 Instance running mysqld/mongod] --> B[Getting More Users<br/>DB Unable to Manage]
    B --> C[Vertical Scaling<br/>More CPU, RAM, Disk]
    C --> D[Product Goes Viral<br/>DB Still Unable to Handle]
    D --> E[Vertical Scaling Again<br/>More Resources]
    E --> F{Physical Limitation Reached?}
    F -->|Yes| G[Horizontal Scaling<br/>Sharding Required]
    F -->|No| E
    
    G --> H[Add More Database Servers<br/>Split the Data]
    
    style A fill:#e1f5ff,stroke:#01579b
    style F fill:#fff9c4,stroke:#f57f17
    style G fill:#c8e6c9,stroke:#2e7d32
    style H fill:#c8e6c9,stroke:#2e7d32
```

### Practical Example

**Scenario**: 
- One DB server handling 1000 WPS (Writes Per Second)
- Cannot scale vertically beyond this
- Receiving 1500 WPS requests

**Solution**:
By adding one more database server and splitting the data, we reduce the load to 750 WPS on each node, thus handling higher throughput.

```mermaid
graph LR
    A[1500 WPS Load] --> B{Single Server?}
    B -->|Yes<br/>Overloaded| C[1500 WPS<br/>Cannot Handle]
    B -->|No<br/>Sharded| D[Shard 1<br/>750 WPS]
    B -->|No<br/>Sharded| E[Shard 2<br/>750 WPS]
    
    style C fill:#ffcdd2,stroke:#c62828
    style D fill:#c8e6c9,stroke:#2e7d32
    style E fill:#c8e6c9,stroke:#2e7d32
```

### Data Partitioning Categories

```mermaid
graph TD
    A[Data Partitioning] --> B[Horizontal Partitioning]
    A --> C[Vertical Partitioning]
    
    B --> B1[Split rows across shards<br/>Same schema per shard]
    B --> B2[Example: Users 1-1000 in Shard1<br/>Users 1001-2000 in Shard2]
    
    C --> C1[Split columns across servers<br/>Different schema per shard]
    C --> C2[Example: User profile in Shard1<br/>User activity in Shard2]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#c8e6c9,stroke:#2e7d32
    style C fill:#fff9c4,stroke:#f57f17
```

### Horizontal Partitioning Example

```mermaid
graph TD
    subgraph Original["Single Database"]
        O1[User ID: 1-3000<br/>All Data]
    end
    
    subgraph Sharded["Sharded Database"]
        S1[Shard 1<br/>User ID: 1-1000]
        S2[Shard 2<br/>User ID: 1001-2000]
        S3[Shard 3<br/>User ID: 2001-3000]
    end
    
    Original --> Sharded
    
    style O1 fill:#ffcdd2,stroke:#c62828
    style S1 fill:#c8e6c9,stroke:#2e7d32
    style S2 fill:#c8e6c9,stroke:#2e7d32
    style S3 fill:#c8e6c9,stroke:#2e7d32
```

### Advantages of Sharding

1. **Handle Large Reads and Writes**
   - Distribute load across multiple servers
   - Each shard handles a fraction of total traffic

2. **Increase Overall Storage Capacity**
   - Not limited by single machine storage
   - Linear scaling with number of shards

3. **Higher Availability**
   - Failure of one shard doesn't affect others
   - Independent shard operations

```mermaid
graph LR
    A[Sharding Benefits] --> B[Performance]
    A --> C[Capacity]
    A --> D[Availability]
    
    B --> B1[Distributed Load]
    B --> B2[Parallel Processing]
    
    C --> C1[Storage Expansion]
    C --> C2[Linear Scaling]
    
    D --> D1[Isolated Failures]
    D --> D2[Independent Operations]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

### Disadvantages of Sharding

1. **Operationally Complex**
   - Requires sophisticated routing logic
   - More infrastructure to manage
   - Backup and restore complexity

2. **Cross-Shard Queries Expensive**
   - Joins across shards are difficult
   - Aggregations require data from multiple shards
   - May need application-level joins

```mermaid
sequenceDiagram
    participant App as Application
    participant S1 as Shard 1
    participant S2 as Shard 2
    participant S3 as Shard 3
    
    Note over App,S3: Cross-Shard Query Problem
    App->>S1: Query data
    App->>S2: Query data
    App->>S3: Query data
    S1->>App: Result 1
    S2->>App: Result 2
    S3->>App: Result 3
    App->>App: Merge and aggregate<br/>(Application layer)
    
    Note over App: Expensive and Complex
```

### Sharding Strategies

```mermaid
graph TD
    A[Sharding Strategies] --> B[Range-Based]
    A --> C[Hash-Based]
    A --> D[Geographic]
    A --> E[Directory-Based]
    
    B --> B1[User ID ranges<br/>1-1000, 1001-2000]
    C --> C1[Hash of key<br/>hash user_id mod N]
    D --> D1[Region-specific<br/>US, EU, ASIA shards]
    E --> E1[Lookup table<br/>Maps key to shard]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

### Best Practices

1. **Choose the right shard key**
   - Ensure even distribution
   - Avoid hotspots
   - Consider query patterns

2. **Plan for resharding**
   - Data growth over time
   - Rebalancing requirements
   - Migration strategies

3. **Monitor shard health**
   - Load distribution
   - Storage utilization
   - Query performance

4. **Each shard can have replicas**
   - For read scaling
   - For high availability
   - For disaster recovery

---

## 8. Non-Relational Databases

**Location:** `08-nonRelationDB/nonRelationalDB.txt`

### Overview

Non-relational databases (NoSQL) are a broad category of databases that differ from traditional relational databases (MySQL, PostgreSQL). However, this does not mean all non-relational databases are similar - each type has unique characteristics and use cases.

### Key Advantage

**Most non-relational databases shard out of the box**, providing horizontal scalability without complex manual configuration.

```mermaid
graph LR
    A[Non-Relational DBs] --> B[Built-in Sharding]
    B --> C[Horizontal Scalability]
    C --> D[Easy to Scale]
    C --> E[No Manual Configuration]
    C --> F[Distributed by Default]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style C fill:#c8e6c9,stroke:#2e7d32
```

### Three Important Types of NoSQL Databases

```mermaid
graph TD
    A[NoSQL Databases] --> B[Document Databases]
    A --> C[Key-Value Stores]
    A --> D[Graph Databases]
    
    B --> B1[MongoDB]
    B --> B2[Elasticsearch]
    
    C --> C1[Redis]
    C --> C2[DynamoDB]
    C --> C3[Aerospike]
    
    D --> D1[Neo4j]
    D --> D2[Neptune]
    D --> D3[Dgraph]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#c8e6c9,stroke:#2e7d32
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#ce93d8,stroke:#7b1fa2
```

---

### 1. Document Databases

**Examples**: MongoDB, Elasticsearch

```mermaid
graph TD
    A[Document Databases] --> B[JSON-Based Storage]
    A --> C[Complex Queries]
    A --> D[Partial Updates]
    A --> E[Closest to Relational DB]
    
    B --> B1[Flexible Schema]
    B --> B2[Nested Documents]
    
    C --> C1[Aggregations]
    C --> C2[Filtering]
    C --> C3[Sorting]
    
    D --> D1[Update specific fields]
    D --> D2[No need to fetch entire doc]
    
    style A fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

#### Characteristics

- **Mostly JSON based**: Store documents in JSON like format
- **Support complex queries**: Almost like relational SQL databases
- **Partial updates possible**: Can update specific fields without fetching entire document
- **Closest to relational DB**: Most similar query capabilities to traditional RDBMS

#### Example Document Structure

```json
{
  "user_id": 12345,
  "name": "John Doe",
  "email": "john@example.com",
  "address": {
    "street": "123 Main St",
    "city": "New York",
    "country": "USA"
  },
  "orders": [
    {"order_id": 1, "total": 99.99},
    {"order_id": 2, "total": 149.99}
  ]
}
```

---

### 2. Key Value Stores

**Examples**: Redis, DynamoDB, Aerospike

```mermaid
graph TD
    A[Key-Value Stores] --> B[Extremely Simple]
    A --> C[Limited Functionalities]
    A --> D[Key-Based Access]
    A --> E[Highly Shardable]
    
    B --> B1[Simple Data Model]
    B --> B2[Fast Operations]
    
    C --> C1[GET key]
    C --> C2[PUT key, value]
    C --> C3[DEL key]
    
    D --> D1[Direct key lookup]
    D --> D2[No complex queries]
    
    E --> E1[Easy partitioning]
    E --> E2[Linear scalability]
    
    style A fill:#fff9c4,stroke:#f57f17,stroke-width:2px
```

#### Characteristics

- **Extremely simple databases**: Minimal complexity
- **Limited functionalities**: Typically only GET, PUT, DEL operations
- **Key-based access pattern**: Direct lookup by key
- **Does not support complex queries**: No aggregations or joins
- **Can be heavily sharded and partitioned**: Excellent horizontal scalability

#### Use Cases

- Profile data storage
- Order data
- Authentication data
- Message storage
- Session management
- Real-time data access

#### Example Operations

```
GET user:12345
PUT user:12345 {"name": "John", "email": "john@example.com"}
DEL user:12345
```

#### Important Note

**You can use relational databases and document DBs as KV stores**, but dedicated KV stores offer better performance and scalability for key-based access patterns.

```mermaid
sequenceDiagram
    participant App as Application
    participant KV as Key-Value Store
    
    App->>KV: GET profile:user123
    KV->>App: {name: "John", email: "..."}
    
    App->>KV: PUT profile:user123 {data}
    KV->>App: OK
    
    App->>KV: DEL profile:user123
    KV->>App: OK
    
    Note over App,KV: Simple, Fast, Efficient
```

---

### 3. Graph Databases

**Examples**: Neo4j, Neptune, Dgraph

```mermaid
graph TD
    A[Graph Databases] --> B[Nodes]
    A --> C[Edges]
    A --> D[Relations]
    
    B --> B1[Entities]
    C --> C1[Connections]
    D --> D1[Properties]
    
    A --> E[Complex Algorithms]
    A --> F[Use Cases]
    
    E --> E1[Shortest Path]
    E --> E2[Community Detection]
    E --> E3[PageRank]
    
    F --> F1[Social Networks]
    F --> F2[Recommendations]
    F --> F3[Fraud Detection]
    
    style A fill:#ce93d8,stroke:#7b1fa2,stroke-width:2px
```

#### Characteristics

- **Graph data structure as database**: Natural representation of connected data
- **Stores data as nodes, edges, and relations**: Explicit relationship modeling
- **Great for complex graph algorithms**: Built in graph traversal and analysis
- **Powerful for specific domains**: Excels where relationships are first  class citizens

#### Use Cases

1. **Social Networks**
   - Friend connections
   - Follow relationships
   - Social graph traversal

2. **Recommendations**
   - Collaborative filtering
   - Product recommendations
   - Content suggestions

3. **Fraud Detection**
   - Transaction patterns
   - Network analysis
   - Anomaly detection

#### Example Graph Structure

```mermaid
graph LR
    A[User: Alice] -->|FOLLOWS| B[User: Bob]
    A -->|LIKES| C[Post: Tech Article]
    B -->|LIKES| C
    B -->|FOLLOWS| D[User: Charlie]
    D -->|WROTE| C
    A -->|FRIEND_OF| D
    
    style A fill:#c8e6c9,stroke:#2e7d32
    style B fill:#c8e6c9,stroke:#2e7d32
    style D fill:#c8e6c9,stroke:#2e7d32
    style C fill:#fff9c4,stroke:#f57f17
```

### NoSQL Database Comparison

| Feature | Document DB | Key-Value Store | Graph DB |
|---------|------------|----------------|----------|
| **Data Model** | JSON documents | Key-value pairs | Nodes & edges |
| **Query Complexity** | High | Low | Medium-High |
| **Scalability** | High | Very High | Medium |
| **Use Case** | General purpose | Simple lookups | Relationship-heavy |
| **Examples** | MongoDB, Elasticsearch | Redis, DynamoDB | Neo4j, Neptune |
| **Schema** | Flexible | None | Semi-structured |
| **Performance** | Good | Excellent | Good for graphs |

### When to Use What

```mermaid
flowchart TD
    A[Data Requirements] --> B{Access Pattern?}
    
    B -->|Complex Queries| C[Document DB]
    B -->|Key-Based Lookup| D[Key-Value Store]
    B -->|Relationship-Heavy| E[Graph DB]
    
    C --> C1[MongoDB<br/>Elasticsearch]
    D --> D1[Redis<br/>DynamoDB]
    E --> E1[Neo4j<br/>Neptune]
    
    style A fill:#64b5f6,stroke:#1976d2
    style C1 fill:#c8e6c9,stroke:#2e7d32
    style D1 fill:#fff9c4,stroke:#f57f17
    style E1 fill:#ce93d8,stroke:#7b1fa2
```

---

## 9. Picking the Right Database

**Location:** `09-pickDB/pickrightDB.txt`

### Overview

Each kind of database targets a specific segment with some overlap. Choosing the right database is crucial for system performance, scalability, and maintainability.

### Common Misconception

**Myth**: "Pick non-relational DB because relational databases do not scale"

**Reality**: Both can scale if designed properly.

```mermaid
graph TD
    A[Why NoSQL Scales Easily?] --> B[No Relations/Constraints]
    A --> C[Data Modeled for Sharding]
    
    D[Can Relational DBs Scale?] --> E[Yes, with adjustments]
    E --> F[Do not use foreign keys]
    E --> G[Do not use cross-shard transactions]
    E --> H[Do manual sharding]
    
    style A fill:#c8e6c9,stroke:#2e7d32
    style D fill:#64b5f6,stroke:#1976d2
    style E fill:#fff9c4,stroke:#f57f17
```

### Database Selection Factors

Every database has peculiar properties and guarantees. If you need specific features, you pick that database.

```mermaid
mindmap
  root((Database Selection))
    Data Characteristics
      Type of data
      Data volume
      Growth rate
    Access Patterns
      Read/Write ratio
      Query complexity
      Latency requirements
    Special Features
      TTL/Expiration
      Full-text search
      Geospatial queries
      ACID guarantees
    Operational
      Team expertise
      Cost
      Maintenance
```

### Selection Process

Before jumping to a particular database, understand:

1. **What data are you storing?**
   - Structure: structured, semi-structured, unstructured
   - Relationships between entities
   - Data types and formats

2. **How much data will you be storing?**
   - Current volume
   - Growth projections
   - Storage requirements

3. **How will you access the data?**
   - Read-heavy or write-heavy
   - Access patterns (key-based, range queries, full scans)
   - Latency requirements

4. **What kind of queries will you fire?**
   - Simple lookups
   - Complex joins
   - Aggregations
   - Full-text search

5. **Any special features you expect?**
   - TTL (Time To Live) / Expiration
   - Transactions
   - Consistency guarantees
   - Built-in caching

---

### Decision Tree: Data Fits on Single Node

```mermaid
flowchart TD
    A[Data Fits on Single Node] --> B{Strong Consistency<br/>& Correctness Important?}
    
    B -->|Yes| C[Relational Database]
    B -->|No| D{Need Complex Queries<br/>& Aggregations?}
    
    C --> C1[MySQL, PostgreSQL<br/>Use Case: Payment transactions]
    
    D -->|Yes| E[Document Database]
    D -->|No| F{KV Access<br/>Need Speed?}
    
    E --> E1[MongoDB, Elasticsearch]
    
    F -->|Yes| G[Redis]
    F -->|No| H{Need Advanced<br/>Data Structures?}
    
    G --> G1[Redis<br/>Fast KV operations]
    H -->|Yes| I[Redis<br/>Sets, Lists, Sorted Sets]
    
    style C fill:#c8e6c9,stroke:#2e7d32
    style E fill:#c8e6c9,stroke:#2e7d32
    style G fill:#fff9c4,stroke:#f57f17
    style I fill:#fff9c4,stroke:#f57f17
```

#### Scenario 1: Strong Consistency & Data Correctness Important

**Choose**: Relational Databases (MySQL, PostgreSQL)

**Example**: Payment transactions, financial data, order management

**Rationale**: ACID guarantees ensure data integrity

---

#### Scenario 2: Need Complex Queries & Aggregations

**Choose**: Non-Relational Databases (MongoDB, Elasticsearch)

**Example**: Analytics, search functionality, flexible schema

**Rationale**: Powerful query capabilities without rigid schema

---

#### Scenario 3: Key-Value Access, Need Speed

**Choose**: Redis

**Example**: Session management, rate limiting, real-time data

**Rationale**: In-memory performance, microsecond latency

---

#### Scenario 4: Need Advanced Data Structures & Algorithms

**Choose**: Redis

**Example**: Leaderboards, pub-sub systems, real-time analytics

**Rationale**: Built-in support for sets, sorted sets, lists, etc.

---

### Decision Tree: Data Cannot Fit on One Node

```mermaid
flowchart TD
    A[Data Cannot Fit on One Node] --> B{Expertise in SQL<br/>& Manual Sharding?}
    
    B -->|Yes| C[Relational Database<br/>Manual Sharding]
    B -->|No| D{Access Pattern?}
    
    C --> C1[MySQL, PostgreSQL<br/>Drop constraints<br/>Manual sharding]
    
    D -->|Simple KV| E[Key-Value Store]
    D -->|Complex Queries| F[Document Database]
    D -->|Graph Operations| G[Graph Database]
    D -->|Nothing Specific| F
    
    E --> E1[DynamoDB, MongoDB<br/>KV mode]
    F --> F1[MongoDB<br/>Default choice]
    G --> G1[Neo4j, Neptune]
    
    style C1 fill:#64b5f6,stroke:#1976d2
    style E1 fill:#fff9c4,stroke:#f57f17
    style F1 fill:#c8e6c9,stroke:#2e7d32
    style G1 fill:#ce93d8,stroke:#7b1fa2
```

#### Scenario 1: SQL Expertise & Can Do Manual Sharding

**Choose**: Relational Database with Manual Sharding

**Approach**:
- Drop foreign key constraints
- Avoid cross-shard transactions
- Implement application-level sharding logic

**Example**: Large-scale applications with SQL expertise

---

#### Scenario 2: Simple Key-Value Based Access

**Choose**: Key-Value Store (DynamoDB, MongoDB in KV mode)

**Example**: User profiles, session data, configuration

**Rationale**: Auto-sharding, simple operations, high scalability

---

#### Scenario 3: Require Sophisticated Graph Algorithms

**Choose**: Graph Database (Neo4j, Neptune)

**Example**: Social networks, fraud detection, recommendation engines

**Rationale**: Optimized for relationship queries and graph traversal

---

#### Scenario 4: Nothing Specific

**Choose**: Document Database (MongoDB)

**Example**: General-purpose applications, MVP development

**Rationale**: Flexible, scalable, good balance of features

---

### Complete Database Selection Matrix

| Requirement | Data Fits Single Node | Data Needs Sharding |
|-------------|----------------------|---------------------|
| **Strong Consistency** | Relational DB (MySQL, PostgreSQL) | Relational DB + Manual Sharding |
| **Complex Queries** | Document DB (MongoDB, Elasticsearch) | Document DB (MongoDB) |
| **Simple KV Access** | Redis | DynamoDB, Aerospike |
| **Speed Critical** | Redis (in-memory) | Redis Cluster |
| **Graph Operations** | Neo4j | Neo4j Cluster |
| **Advanced Data Structures** | Redis | Redis Cluster |
| **General Purpose** | PostgreSQL | MongoDB |

### Practical Examples

```mermaid
graph TD
    A[Real-World Examples] --> B[E-commerce Platform]
    A --> C[Social Media]
    A --> D[Banking System]
    A --> E[Analytics Platform]
    
    B --> B1[Orders: Relational DB]
    B --> B2[Product Catalog: Document DB]
    B --> B3[Session: Redis]
    
    C --> C1[User Profiles: Document DB]
    C --> C2[Connections: Graph DB]
    C --> C3[Feed Cache: Redis]
    
    D --> D1[Transactions: Relational DB]
    D --> D2[Fraud Detection: Graph DB]
    D --> D3[Auth Tokens: Redis]
    
    E --> E1[Raw Events: Document DB]
    E --> E2[Aggregations: Elasticsearch]
    E --> E3[Real-time: Redis]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

### Key Takeaways

1. **No single database fits all use cases** - most systems use multiple databases
2. **Understand your requirements first** before selecting a database
3. **Consider scalability from the start** but don't over-engineer
4. **Team expertise matters** - choose what your team can maintain
5. **Start simple, scale later** - vertical scaling is often enough initially
6. **Test at scale** - benchmark with realistic data volumes
7. **Document DB is safe default** - when in doubt, MongoDB is a reasonable choice

```mermaid
flowchart LR
    A[Start Here] --> B{Understand Requirements}
    B --> C{Evaluate Options}
    C --> D{Consider Trade-offs}
    D --> E{Make Decision}
    E --> F{Test & Validate}
    F --> G[Deploy]
    
    style A fill:#e1f5ff,stroke:#01579b
    style G fill:#c8e6c9,stroke:#2e7d32
```

---

## 10. Caching Fundamentals

**Location:** `10-caching/caching.txt`

### What is Caching?

Caches are anything that helps you avoid an expensive network I/O, disk I/O, or computation. They store frequently accessed data in a temporary storage location that's faster to access than the primary data source.

```mermaid
graph LR
    A[Expensive Operations] --> B[Network I/O]
    A --> C[Disk I/O]
    A --> D[Heavy Computation]
    
    B --> E[API calls]
    C --> F[Database queries]
    D --> G[Complex joins]
    
    E --> H[Cache]
    F --> H
    G --> H
    
    H --> I[Fast Access]
    
    style A fill:#ffcdd2,stroke:#c62828
    style H fill:#c8e6c9,stroke:#2e7d32
    style I fill:#c8e6c9,stroke:#2e7d32
```

### Examples of Expensive Operations

1. **API call to get profile information** - Network latency
2. **Reading a specific line from a file** - Disk I/O
3. **Doing multiple table joins** - CPU-intensive computation

### How Caching Works

```mermaid
sequenceDiagram
    participant User
    participant API
    participant Cache
    participant Database
    
    User->>API: Request data
    API->>Cache: Check cache
    
    alt Data in Cache
        Cache->>API: Return cached data
        API->>User: Fast response
    else Cache Miss
        Cache->>API: Not found
        API->>Database: Query database
        Database->>API: Return data
        API->>Cache: Store in cache
        API->>User: Response (slower)
    end
    
    Note over Cache: Faster & Expensive
    Note over Database: Slower & Cheaper
```

### Key Principles

1. **Cache is checked first** - Always try cache before expensive operation
2. **Caches are faster and expensive** - Typically in-memory (RAM)
3. **Partial data caching** - Only cache subset of data most likely to be accessed
4. **Not restricted to RAM** - Any nearer storage that avoids expensive operations

```mermaid
graph TD
    A[Caching Principles] --> B[Subset of Data]
    A --> C[Frequently Accessed]
    A --> D[Temporary Storage]
    A --> E[Fast Access]
    
    B --> B1[Not all data cached]
    B --> B2[Hot data only]
    
    C --> C1[Access patterns matter]
    C --> C2[Recency important]
    
    D --> D1[With expiration]
    D --> D2[Can be invalidated]
    
    E --> E1[Lower latency]
    E --> E2[Reduced load]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

### Common Cache Technologies

- **Redis**: In-memory data store, supports rich data structures
- **Memcached**: Simple in-memory key-value cache
- **CDN**: Content delivery network for static assets
- **Browser Cache**: Client-side caching

### Simplest Form

In the simplest form, caches are just glorified hash tables.

```
cache = {
  "user:123": {name: "John", email: "john@example.com"},
  "post:456": {title: "System Design", content: "..."},
  "session:abc": {user_id: 123, expires: 1234567890}
}
```

---

### Real-World Examples

#### Example 1: Google News

```mermaid
graph TD
    A[Google News] --> B[Recent Articles]
    B --> C[More Likely to be Accessed]
    C --> D[Served from Cache]
    
    A --> E[Older Articles]
    E --> F[Less Likely to be Accessed]
    F --> G[Served from Database]
    
    style D fill:#c8e6c9,stroke:#2e7d32
    style G fill:#fff9c4,stroke:#f57f17
```

**Scenario**: Most recent news articles are more likely to be accessed

**Solution**: Cache recent articles (last 24-48 hours)

**Benefit**: Reduced database load, faster response times

---

#### Example 2: Authentication Tokens

```mermaid
sequenceDiagram
    participant User
    participant API
    participant Cache
    participant AuthDB
    
    Note over User,AuthDB: Every Request Checks Token
    
    User->>API: Request with token
    API->>Cache: Verify token
    
    alt Token Valid in Cache
        Cache->>API: Valid (0.5ms)
        API->>User: Process request
    else Token Not in Cache
        API->>AuthDB: Verify token
        AuthDB->>API: Valid (50ms)
        API->>Cache: Store token
        API->>User: Process request
    end
    
    Note over Cache: 100x faster than DB
```

**Scenario**: Authentication tokens are checked on every request

**Solution**: Cache valid tokens in Redis

**Benefit**: Avoid database hit on every request, microsecond latency

---

#### Example 3: Live Stream

```mermaid
graph LR
    A[Live Stream] --> B[Last 10 Minutes]
    B --> C[Most Accessed]
    C --> D[Cached on CDN]
    
    A --> E[Older Content]
    E --> F[Less Accessed]
    F --> G[Served from Origin]
    
    style D fill:#c8e6c9,stroke:#2e7d32
    style G fill:#fff9c4,stroke:#f57f17
```

**Scenario**: Last 10 minutes of live stream accessed most frequently

**Solution**: Cache recent content on CDN edge servers

**Benefit**: Lower latency, reduced origin server load

---

### Cache Performance Impact

```mermaid
graph TD
    A[Without Cache] --> B[Every Request to DB]
    B --> C[High Latency: 50-100ms]
    B --> D[High DB Load]
    B --> E[Limited Throughput]
    
    F[With Cache] --> G[Most Requests to Cache]
    G --> H[Low Latency: 0.5-5ms]
    G --> I[Low DB Load]
    G --> J[High Throughput]
    
    style A fill:#ffcdd2,stroke:#c62828
    style F fill:#c8e6c9,stroke:#2e7d32
```

### When to Use Caching

```mermaid
flowchart TD
    A[Consider Caching When] --> B{Read-Heavy Workload?}
    A --> C{Expensive Operations?}
    A --> D{Repeated Requests?}
    A --> E{Acceptable Staleness?}
    
    B -->|Yes| F[Good Candidate]
    C -->|Yes| F
    D -->|Yes| F
    E -->|Yes| F
    
    B -->|No| G[Maybe Not]
    C -->|No| G
    D -->|No| G
    E -->|No| G
    
    style F fill:#c8e6c9,stroke:#2e7d32
    style G fill:#ffcdd2,stroke:#c62828
```

### Key Takeaways

1. **Cache to avoid expensive operations** - Network, disk, computation
2. **Cache frequently accessed data** - Use access patterns to determine what to cache
3. **Caches are temporary** - Data has expiration (TTL)
4. **Not just RAM** - Any nearer storage can act as cache
5. **Subset of data** - Don't cache everything, only hot data
6. **Significant performance boost** - 10-100x improvement possible

---

## 11. Populating Cache

**Location:** `11-populateCache/populateCache.txt`

### Overview

Cache sits between the API server and the database. Whenever we set something in cache, we set an expiration (TTL - Time To Live) to ensure data doesn't become stale indefinitely.

```mermaid
graph LR
    A[API Server] <--> B[Cache Layer]
    B <--> C[Database]
    
    style B fill:#fff9c4,stroke:#f57f17,stroke-width:2px
```

### Two Ways to Populate Cache

```mermaid
graph TD
    A[Cache Population Strategies] --> B[Lazy Population]
    A --> C[Eager Population]
    
    B --> B1[Cache on Read]
    B --> B2[Most Popular]
    B --> B3[On-Demand]
    
    C --> C1[Cache on Write]
    C --> C2[Proactive]
    C --> C3[Anticipate Need]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#c8e6c9,stroke:#2e7d32
    style C fill:#fff9c4,stroke:#f57f17
```

---

### 1. Lazy Population (Cache-Aside Pattern)

**Most popular approach** - Populate cache on-demand when data is first requested.

#### Algorithm

```
function getData(key):
    data = cache.get(key)
    
    if data exists:
        return data  // Cache Hit
    else:
        // Cache Miss
        data = database.query(key)
        cache.set(key, data, TTL)
        return data
```

#### Flow Diagram

```mermaid
sequenceDiagram
    participant Client
    participant API
    participant Cache
    participant DB
    
    Note over Client,DB: First Request (Cache Miss)
    Client->>API: GET /blog/123
    API->>Cache: GET blog:123
    Cache->>API: NULL (miss)
    API->>DB: SELECT * FROM blogs WHERE id=123
    DB->>API: Blog data
    API->>Cache: SET blog:123, data, TTL=3600
    Cache->>API: OK
    API->>Client: Blog data (slow: ~50ms)
    
    Note over Client,DB: Subsequent Requests (Cache Hit)
    Client->>API: GET /blog/123
    API->>Cache: GET blog:123
    Cache->>API: Blog data (hit)
    API->>Client: Blog data (fast: ~1ms)
```

#### Example: Caching Blog Posts

**Scenario**: Fetching a blog from database is expensive (multiple joins for author, tags, comments)

**Solution**:
1. When someone accesses a blog, fetch from database
2. Cache the result in Redis with TTL
3. Subsequent requests are served from cache

```mermaid
graph TD
    A[User Requests Blog] --> B{In Cache?}
    B -->|Yes| C[Return from Cache<br/>1ms response]
    B -->|No| D[Fetch from DB<br/>Complex joins]
    D --> E[Store in Cache<br/>TTL: 1 hour]
    E --> F[Return to User<br/>50ms response]
    
    style C fill:#c8e6c9,stroke:#2e7d32
    style D fill:#ffcdd2,stroke:#c62828
```

#### Advantages
- Simple to implement
- Only caches data that's actually accessed
- No wasted cache space

#### Disadvantages
- First request is always slow (cache miss)
- Cache stampede possible for popular items

---

### 2. Eager Population

Populate cache proactively before data is requested. Two approaches:

#### Approach 1: Write-Through Cache

**Write to both database and cache simultaneously**

```mermaid
sequenceDiagram
    participant Client
    participant API
    participant Cache
    participant DB
    
    Client->>API: UPDATE data
    
    par Write to both
        API->>DB: UPDATE database
        API->>Cache: SET cache
    end
    
    DB->>API: OK
    Cache->>API: OK
    API->>Client: Success
    
    Note over API: Both updated atomically
```

#### Example: Live Cricket Score

**Scenario**: Thousands of people are watching cricket scores in real-time

**Solution**:
- When score updates, write to both database and cache
- Saves cache miss since data will definitely be accessed
- Users always get instant response

```mermaid
graph LR
    A[Score Update] --> B[Write to DB]
    A --> C[Write to Cache]
    
    D[1000s of Users] --> C
    C --> E[Instant Response<br/>No Cache Miss]
    
    style C fill:#c8e6c9,stroke:#2e7d32
    style E fill:#c8e6c9,stroke:#2e7d32
```

**Benefits**:
- No cache miss for hot data
- Consistent performance
- Always fresh data in cache

---

#### Approach 2: Proactive Push to Cache

**Anticipate need and push data to cache in advance**

```mermaid
sequenceDiagram
    participant Event
    participant Service
    participant Cache
    participant Users
    
    Note over Event,Users: Celebrity Posts Content
    
    Event->>Service: New post by celebrity
    Service->>Service: Detect high-profile user<br/>(100k+ followers)
    Service->>Cache: Proactively cache post
    Cache->>Service: OK
    
    Note over Users: Followers access post
    Users->>Cache: GET post (cache hit)
    Cache->>Users: Instant response
    
    Note over Event,Users: Regular User Posts
    
    Event->>Service: New post by regular user
    Service->>Service: Normal flow<br/>(lazy population)
```

#### Example: Celebrity Tweet/Post

**Scenario**: When an account with 100k+ followers posts something, it will be accessed frequently

**Solution**:
1. Detect high-profile account posting
2. Proactively push content to cache
3. Followers get instant access without cache miss

```mermaid
graph TD
    A[Celebrity Posts] --> B{Follower Count > 100k?}
    B -->|Yes| C[Proactively Cache]
    B -->|No| D[Normal Lazy Caching]
    
    C --> E[Push to Cache Immediately]
    E --> F[All Followers Get<br/>Cache Hit]
    
    D --> G[First Access Misses]
    G --> H[Then Cached]
    
    style C fill:#c8e6c9,stroke:#2e7d32
    style F fill:#c8e6c9,stroke:#2e7d32
```

**Benefits**:
- Eliminate cache miss for viral content
- Better user experience
- Reduced database load during traffic spikes

---

### Comparison: Lazy vs Eager Population

| Aspect | Lazy Population | Eager Population |
|--------|----------------|------------------|
| **When Cached** | On first read | On write or anticipation |
| **Cache Miss** | First request always misses | No miss for anticipated data |
| **Complexity** | Simple | More complex |
| **Cache Efficiency** | High (only accessed data) | Can cache unused data |
| **Use Case** | General purpose | Hot data, real-time updates |
| **Performance** | Good after first request | Consistently excellent |
| **Resource Usage** | Efficient | Can be wasteful |

### Combined Strategy

```mermaid
flowchart TD
    A[Data Update] --> B{Is Data Hot?}
    
    B -->|Yes<br/>Viral/Popular| C[Eager Population]
    B -->|No<br/>Regular| D[Lazy Population]
    
    C --> C1[Write-Through Cache]
    C --> C2[Proactive Push]
    
    D --> D1[Cache on Read]
    
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#c8e6c9,stroke:#2e7d32
```

**Best Practice**: Use a combination of both strategies
- Lazy population for most data (default)
- Eager population for known hot data
- Monitor access patterns to identify hot data

---

### Scaling Cache

Cache is just like a database, hence scaling techniques for cache (like Redis) are similar to scaling a database.

```mermaid
graph TD
    A[Cache Scaling] --> B[Vertical Scaling]
    A --> C[Horizontal Scaling - Replicas]
    A --> D[Horizontal Scaling - Sharding]
    
    B --> B1[Make cache bigger<br/>Handle more data/load]
    
    C --> C1[Same data replicated<br/>across multiple nodes]
    C --> C2[Scale reads]
    
    D --> D1[Data partitioned<br/>across shards]
    D --> D2[Scale writes]
    D --> D3[Each shard can have replicas]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#c8e6c9,stroke:#2e7d32
    style D fill:#c8e6c9,stroke:#2e7d32
```

#### Vertical Scaling
Make your cache bigger to handle more data and load
- Increase RAM
- More CPU cores
- Limited by hardware

#### Horizontal Scaling - Replica
Same data replicated across multiple nodes so that reads can scale
- Read distribution
- High availability
- Eventual consistency

#### Horizontal Scaling - Sharding
Data partitioned across multiple shards so that writes can scale
- Each shard handles subset of keys
- Linear scalability
- Each shard can have its own replicas
- Shards are mutually exclusive (no data overlap)

```mermaid
graph TD
    A[Cache Cluster] --> B[Shard 1<br/>Keys: A-H]
    A --> C[Shard 2<br/>Keys: I-P]
    A --> D[Shard 3<br/>Keys: Q-Z]
    
    B --> B1[Replica 1]
    B --> B2[Replica 2]
    
    C --> C1[Replica 1]
    
    D --> D1[Replica 1]
    D --> D2[Replica 2]
    
    style A fill:#64b5f6,stroke:#1976d2
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#fff9c4,stroke:#f57f17
```

---

## 12. Caching at Different Levels

**Location:** `12-cachingDifferentLevels/cachingLevels.txt`

### Overview

Redis is the most common cache, but it's not the only type of cache or the only place where caching can be implemented. Literally every component in the infrastructure can be used as a cache.

### Should We Cache Everywhere?

**It depends on the guarantees** - Too much caching can lead to:
- Stale data problems
- Complex invalidation logic
- Debugging difficulties
- Consistency issues

```mermaid
graph TD
    A[Caching Considerations] --> B[Guarantees Needed]
    A --> C[Staleness Tolerance]
    A --> D[Invalidation Complexity]
    
    B --> B1[Consistency]
    B --> B2[Freshness]
    
    C --> C1[How stale is acceptable?]
    C --> C2[Impact of stale data]
    
    D --> D1[How to invalidate?]
    D --> D2[Cascade invalidation]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

---

### Multi-Level Caching Architecture

```mermaid
graph TD
    A[User] --> B[Client-Side Cache<br/>Browser/Mobile]
    B --> C[CDN Cache<br/>Edge Servers]
    C --> D[Load Balancer Cache<br/>Session Data]
    D --> E[Remote Cache<br/>Redis/Memcached]
    E --> F[Database Cache<br/>Query Cache]
    F --> G[Database<br/>Source of Truth]
    
    style B fill:#e1f5ff,stroke:#01579b
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#f3e5f5,stroke:#7b1fa2
    style E fill:#c8e6c9,stroke:#2e7d32
    style F fill:#ffe0b2,stroke:#e65100
    style G fill:#ffcdd2,stroke:#c62828
```

---

### 1. Client-Side Caching

Store frequently accessed data on the client side (browser, mobile devices).

```mermaid
graph TD
    A[Client-Side Caching] --> B[Browser Cache]
    A --> C[Mobile App Cache]
    A --> D[LocalStorage/SessionStorage]
    
    B --> B1[Static Assets]
    B --> B2[API Responses]
    
    C --> C1[User Data]
    C --> C2[Offline Support]
    
    D --> D1[Preferences]
    D --> D2[Temporary Data]
    
    style A fill:#e1f5ff,stroke:#01579b,stroke-width:2px
```

#### What to Cache

- **Near-constant data**: Images, CSS, JavaScript files
- **User information**: Profile data, preferences
- **Static content**: Configuration, translations

#### Characteristics

- **Massive performance boost** - No network request needed
- **It should be okay serving stale data** - Accept some staleness
- **Invalidation by time (expiry)** - Use TTL or version numbers
- **Reduces backend load** - Fewer requests to server

#### Example: HTTP Cache Headers

```http
Cache-Control: public, max-age=86400
ETag: "abc123"
Last-Modified: Mon, 01 Jan 2024 00:00:00 GMT
```

```mermaid
sequenceDiagram
    participant Browser
    participant CDN
    participant Server
    
    Note over Browser,Server: First Request
    Browser->>CDN: GET /logo.png
    CDN->>Server: GET /logo.png
    Server->>CDN: logo.png + Cache-Control: max-age=86400
    CDN->>Browser: logo.png + headers
    Browser->>Browser: Cache for 24 hours
    
    Note over Browser,Server: Subsequent Requests (within 24 hours)
    Browser->>Browser: Serve from cache
    
    Note over Browser: No network request!
```

---

### 2. CDN (Content Delivery Network)

CDNs are a set of servers distributed across the world. Requests from users go to the nearest CDN server, providing very quick responses.

```mermaid
graph TD
    A[Global CDN Network] --> B[US East]
    A --> C[US West]
    A --> D[Europe]
    A --> E[Asia]
    A --> F[Australia]
    
    B --> B1[New York]
    B --> B2[Miami]
    
    C --> C1[San Francisco]
    C --> C2[Seattle]
    
    D --> D1[London]
    D --> D2[Frankfurt]
    
    E --> E1[Singapore]
    E --> E2[Tokyo]
    
    F --> F1[Sydney]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

#### Use Cases

- **Live streaming** - Video content
- **Static assets** - Images, videos, audio
- **JavaScript bundles** - Application code
- **API responses** - Cacheable endpoints

#### How CDN Caching Works

**CDN uses lazy cache population (Cache-Aside Pattern)**

```mermaid
sequenceDiagram
    participant User
    participant CDN
    participant Origin
    
    Note over User,Origin: First Request to CDN (Cache Miss)
    User->>CDN: GET /image.jpg
    CDN->>CDN: Check cache
    CDN->>Origin: Forward request to origin
    Origin->>CDN: image.jpg + TTL
    CDN->>CDN: Cache response
    CDN->>User: image.jpg (slow: ~200ms)
    
    Note over User,Origin: Subsequent Requests (Cache Hit)
    User->>CDN: GET /image.jpg
    CDN->>CDN: Found in cache
    CDN->>User: image.jpg (fast: ~20ms)
    
    Note over CDN: 10x faster!
```

#### CDN Workflow

```
1. User request comes to CDN ? closest server
2. CDN server checks if it has the data
3. If YES: return the data (Cache Hit)
4. If NO:
   a. CDN makes same request to origin server
   b. Gets the response
   c. Caches the response with TTL
   d. Returns the data
```

#### Geographic Performance

```mermaid
graph LR
    A[US User] --> B[US CDN Server]
    B --> C[20ms response]
    
    D[India User] --> E[India CDN Server]
    E --> F[25ms response]
    
    G[Without CDN<br/>India User] --> H[US Origin Server]
    H --> I[300ms response]
    
    style C fill:#c8e6c9,stroke:#2e7d32
    style F fill:#c8e6c9,stroke:#2e7d32
    style I fill:#ffcdd2,stroke:#c62828
```

**Key Point**: US users getting images from US servers is faster than fetching from India

#### CDN Expiration

Like any other cache, when we put data on CDN, we set an expiry to it. Post expiry, CDN deletes the data.

```mermaid
graph TD
    A[Data Added to CDN] --> B[Set TTL: 24 hours]
    B --> C{Time Elapsed?}
    C -->|< 24 hours| D[Serve from Cache]
    C -->|= 24 hours| E[Delete from Cache]
    E --> F[Next Request = Cache Miss]
    F --> G[Fetch from Origin]
    G --> B
    
    style D fill:#c8e6c9,stroke:#2e7d32
    style E fill:#fff9c4,stroke:#f57f17
```

---

### 3. Remote Cache (Redis)

Remote cache is a centralized cache that multiple API servers use to store frequently accessed data.

```mermaid
graph TD
    A[API Server 1] --> D[Redis Cluster]
    B[API Server 2] --> D
    C[API Server 3] --> D
    
    D --> E[Shard 1]
    D --> F[Shard 2]
    D --> G[Shard 3]
    
    E --> E1[Replica]
    F --> F1[Replica]
    G --> G1[Replica]
    
    style D fill:#c8e6c9,stroke:#2e7d32,stroke-width:2px
```

#### Characteristics

- **Centralized and shared** - Multiple services access same cache
- **In-memory storage** - Extremely fast (microsecond latency)
- **Expensive** - RAM is costly compared to disk
- **Requires expiration** - Every key must have TTL to manage memory
- **Relatively small size** - Limited by available RAM

#### What to Cache in Redis

```mermaid
mindmap
  root((Redis Cache))
    Session Data
      User sessions
      Auth tokens
      Shopping cart
    Hot Data
      Recent posts
      Trending items
      Popular products
    Computed Data
      Aggregations
      Leaderboards
      Counters
    Temporary Data
      OTP codes
      Rate limits
      Locks
```

#### Best Practices

1. **Always set TTL** - Prevent memory exhaustion
2. **Cache hot data** - Frequently accessed items
3. **Monitor memory** - Set eviction policies
4. **Use appropriate data structures** - Strings, Lists, Sets, Sorted Sets

```
SET user:123:session "data" EX 3600     # Expires in 1 hour
SET otp:phone:9999 "123456" EX 300      # Expires in 5 minutes
ZADD leaderboard 1500 "player1"         # Sorted set for rankings
```

---

### 4. Database Caching

Caching computed or aggregated data within the database itself to avoid expensive recomputation.

```mermaid
graph TD
    A[Database Caching] --> B[Computed Columns]
    A --> C[Materialized Views]
    A --> D[Query Cache]
    
    B --> B1[Denormalization]
    B --> B2[Aggregated Data]
    
    C --> C1[Precomputed Joins]
    C --> C2[Complex Queries]
    
    D --> D1[Query Results]
    D --> D2[Execution Plans]
    
    style A fill:#ffe0b2,stroke:#e65100,stroke-width:2px
```

#### Example: Caching Total Posts

Instead of computing total posts by a user every time with an expensive query:

```sql
-- Expensive Query (Every Time)
SELECT COUNT(*) FROM posts WHERE user_id = 123;
```

Store 	otal_posts as a column in the users table and update it periodically:

```sql
-- Fast Query
SELECT total_posts FROM users WHERE user_id = 123;

-- Update once in a while (async job or trigger)
UPDATE users SET total_posts = total_posts + 1 WHERE user_id = 123;
```

#### Benefits

- **Avoid expensive computations** - Precompute and store
- **Faster queries** - Direct column access
- **Reduced CPU usage** - Less query processing

#### Trade-offs

- **Potential staleness** - Data might be slightly outdated
- **Storage overhead** - Extra columns/tables
- **Sync complexity** - Keep cached data updated

```mermaid
sequenceDiagram
    participant App
    participant DB
    
    Note over App,DB: Without Caching
    App->>DB: SELECT COUNT(*) FROM posts WHERE user_id=123
    DB->>DB: Scan posts table (slow)
    DB->>App: 1,234 (50ms)
    
    Note over App,DB: With Caching
    App->>DB: SELECT total_posts FROM users WHERE id=123
    DB->>DB: Index lookup (fast)
    DB->>App: 1,234 (2ms)
```

---

### 5. Load Balancer Caching

Load balancers can cache session information and other data.

```mermaid
graph TD
    A[Users] --> B[Load Balancer]
    B --> C[Session Cache]
    B --> D[Server 1]
    B --> E[Server 2]
    B --> F[Server 3]
    
    C --> C1[Sticky Sessions]
    C --> C2[Session Affinity]
    
    style B fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
```

#### Use Cases

- **Session affinity** - Route user to same server
- **SSL session caching** - Reuse SSL handshakes
- **Rate limiting** - Track request counts

---

### Caching Strategy Comparison

| Cache Level | Latency | Capacity | Staleness Risk | Use Case |
|-------------|---------|----------|----------------|----------|
| **Client-Side** | ~0ms | Small | High | Static assets, UI state |
| **CDN** | ~20ms | Large | Medium | Media files, static content |
| **Load Balancer** | ~1ms | Small | Low | Sessions, SSL |
| **Remote (Redis)** | ~1ms | Medium | Low | Hot data, sessions |
| **Database** | ~5ms | Large | Medium | Computed aggregations |

---

### Cache Invalidation Strategies

```mermaid
graph TD
    A[Cache Invalidation] --> B[Time-Based - TTL]
    A --> C[Event-Based]
    A --> D[Manual]
    
    B --> B1[Set expiration time]
    B --> B2[Auto cleanup]
    
    C --> C1[On data update]
    C --> C2[Publish/Subscribe]
    
    D --> D1[Admin action]
    D --> D2[Deployment]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

#### Time-Based (TTL)
```
cache.set("key", "value", ttl=3600)  # Expires after 1 hour
```

#### Event-Based
```
on_user_update(user_id):
    cache.delete(f"user:{user_id}")
    cache.delete(f"user:{user_id}:profile")
```

#### Manual Invalidation
```
cache.flush_all()  # Clear entire cache
cache.delete_pattern("user:*")  # Pattern-based deletion
```

---

### Best Practices for Multi-Level Caching

```mermaid
flowchart TD
    A[Caching Best Practices] --> B[Set Appropriate TTLs]
    A --> C[Monitor Cache Hit Rates]
    A --> D[Plan Invalidation Strategy]
    A --> E[Avoid Over-Caching]
    A --> F[Consider Consistency]
    
    B --> B1[Short TTL for dynamic data]
    B --> B2[Long TTL for static data]
    
    C --> C1[Track hit/miss ratios]
    C --> C2[Optimize cache size]
    
    D --> D1[Event-driven invalidation]
    D --> D2[Graceful degradation]
    
    E --> E1[Cache only hot data]
    E --> E2[Avoid cache bloat]
    
    F --> F1[Accept eventual consistency]
    F --> F2[Strong consistency where needed]
    
    style A fill:#64b5f6,stroke:#1976d2,stroke-width:3px
```

### Key Principles

1. **Cache at the right level** - Choose based on access patterns
2. **Set appropriate TTLs** - Balance freshness and performance
3. **Monitor cache effectiveness** - Track hit rates and memory usage
4. **Plan invalidation** - Don't let stale data accumulate
5. **Accept trade-offs** - Performance vs. consistency
6. **Avoid over-caching** - Too much caching is bad
7. **Use case specific** - Subject to tolerance level of staleness

---

### When NOT to Cache

```mermaid
graph TD
    A[Avoid Caching When] --> B[Strong Consistency Required]
    A --> C[Frequently Changing Data]
    A --> D[Personalized Data]
    A --> E[Security-Sensitive Data]
    
    B --> B1[Financial transactions]
    B --> B2[Inventory counts]
    
    C --> C1[Real-time updates]
    C --> C2[Live data feeds]
    
    D --> D1[User-specific content]
    D --> D2[Low cache hit rate]
    
    E --> E1[Passwords]
    E --> E2[PII]
    
    style A fill:#ffcdd2,stroke:#c62828,stroke-width:2px
```

---

### Summary

Caching can be implemented at multiple levels of the infrastructure stack. Each level has its own characteristics, advantages, and trade-offs. The key is to:

- Understand what data to cache at each level
- Set appropriate TTLs based on data characteristics
- Implement proper invalidation strategies
- Monitor cache effectiveness
- Accept that some staleness is often acceptable for massive performance gains

**Remember**: Not every component should cache everything. It is very use case specific and subject to the tolerance level of staleness of the served data.

---

## Conclusion

This repository provides a comprehensive guide to System Design fundamentals, covering:

- **Foundational Concepts**: Understanding what system design is and how to approach it
- **Database Technologies**: Relational and non-relational databases, scaling strategies
- **Caching Strategies**: Multi-level caching for performance optimization

Each topic builds upon previous concepts to provide a complete understanding of building scalable, reliable, and efficient systems.

---

## Repository Structure

```
.
+-- 01-about_SD/                  # What is System Design
+-- 02-approachSD/                # How to approach System Design
+-- 03-good-system/               # Characteristics of good systems
+-- 04-relationDB/                # Relational databases and ACID
+-- 05-DB_Isolation_levels/       # Database isolation levels
+-- 06-scalingDB/                 # Database scaling techniques
+-- 07-shardingAndPartitioning/   # Sharding and partitioning strategies
+-- 08-nonRelationDB/             # Non-relational database types
+-- 09-pickDB/                    # How to pick the right database
+-- 10-caching/                   # Caching fundamentals
+-- 11-populateCache/             # Cache population strategies
+-- 12-cachingDifferentLevels/    # Multi-level caching
```

---

## Quick Reference

### Database Selection

```mermaid
flowchart TD
    A[Start] --> B{Data Fits<br/>Single Node?}
    
    B -->|Yes| C{Need Strong<br/>Consistency?}
    B -->|No| D{Need Graph<br/>Operations?}
    
    C -->|Yes| E[Relational DB]
    C -->|No| F{Complex<br/>Queries?}
    
    F -->|Yes| G[Document DB]
    F -->|No| H[Key-Value Store]
    
    D -->|Yes| I[Graph DB]
    D -->|No| J{Simple<br/>KV Access?}
    
    J -->|Yes| H
    J -->|No| G
    
    style E fill:#64b5f6,stroke:#1976d2
    style G fill:#c8e6c9,stroke:#2e7d32
    style H fill:#fff9c4,stroke:#f57f17
    style I fill:#ce93d8,stroke:#7b1fa2
```

### Scaling Strategies

```mermaid
graph LR
    A[Scaling] --> B[Vertical]
    A --> C[Horizontal]
    
    B --> B1[Add Resources]
    
    C --> C1[Read Replicas]
    C --> C2[Sharding]
    
    C1 --> C1A[Sync/Async]
    C2 --> C2A[Each Shard<br/>Can Have Replicas]
    
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#c8e6c9,stroke:#2e7d32
```

### Caching Levels

```mermaid
graph TD
    A[Client] --> B[CDN]
    B --> C[Load Balancer]
    C --> D[Remote Cache]
    D --> E[Database Cache]
    E --> F[Database]
    
    style A fill:#e1f5ff,stroke:#01579b
    style B fill:#fff9c4,stroke:#f57f17
    style D fill:#c8e6c9,stroke:#2e7d32
    style F fill:#ffcdd2,stroke:#c62828
```

---

## 13. Message Brokers and Queues

Message brokers enable asynchronous communication between services, allowing systems to handle long running tasks without blocking users. They act as intermediaries that facilitate communication through message passing.

### Synchronous vs Asynchronous Processing

**Synchronous Operations** - Immediate handling with user waiting for response:
- Loading Instagram feed
- Website login
- Payment processing
- Most web interactions

**Asynchronous Operations** - Tasks that take time, user checks status later:
- Spinning up virtual machines (takes minutes)
- Video processing
- Batch operations
- Background tasks

### Architecture Pattern

```mermaid
graph LR
    A[Client] --> B[API Server]
    B --> C[Database]
    B --> D[Message Broker]
    D --> E[Worker 1]
    D --> F[Worker 2]
    D --> G[Worker 3]
    E --> C
    F --> C
    G --> C
    C --> B
    B --> A
    
    style D fill:#fff9c4,stroke:#f57f17
    style E fill:#c8e6c9,stroke:#2e7d32
    style F fill:#c8e6c9,stroke:#2e7d32
    style G fill:#c8e6c9,stroke:#2e7d32
```

### When to Use Message Queues

1. **Long Running Tasks** - Operations that take significant time to complete
2. **Trigger Dependent Tasks** - Coordinate work across multiple machines
3. **Decoupling Services** - Allow systems to work independently

### Key Features of Message Brokers

#### 1. Service Connectivity
Brokers help connect different sub-systems, enabling loose coupling between components.

#### 2. Buffer Mechanism
Messages are buffered, allowing consumers to process at their own pace without synchronous load on connected systems.

**Example**: Notification system where messages queue up and are sent as the notification service can handle them.

#### 3. Message Retention
Brokers can retain messages for configurable periods (depends on broker implementation), providing durability and recovery options.

#### 4. Message Re-queuing
If a message is not acknowledged or deleted, it can be re-queued automatically.

**Example**: Consumer reads a message but crashes before deleting it - the message returns to the queue.

### Use Case Example: Auto Subtitle Generation

```mermaid
sequenceDiagram
    participant User
    participant VideoService
    participant S3
    participant Broker
    participant Captioner
    participant Database
    
    User->>VideoService: Upload video
    VideoService->>S3: Store video
    S3-->>VideoService: Upload complete
    VideoService->>Broker: Put message
    VideoService-->>User: Upload complete
    Note over User: User sees upload complete
    
    Broker->>Captioner: Async message read
    Captioner->>S3: Download video
    Captioner->>Captioner: Generate captions
    Captioner->>Database: Update with captions
    Note over User: User sees caption button enabled
```

**Flow**:
1. User uploads video to S3 through video service
2. Video service puts a message to broker after upload completes
3. Returns response to user immediately
4. User sees "upload complete"
5. Message is asynchronously read by captioner service
6. Captioner downloads the video
7. Captioner generates captions and updates the database
8. User now sees caption button enabled

### Message Queue Benefits

```mermaid
graph TD
    A[Message Broker Benefits] --> B[Decoupling]
    A --> C[Scalability]
    A --> D[Reliability]
    A --> E[Flexibility]
    
    B --> B1[Services work independently]
    B --> B2[No tight coupling]
    
    C --> C1[Scale consumers independently]
    C --> C2[Handle variable load]
    
    D --> D1[Message persistence]
    D --> D2[Retry mechanism]
    
    E --> E1[Multiple consumers]
    E --> E2[Easy to add new consumers]
    
    style A fill:#64b5f6,stroke:#1976d2
```

---

## 14. Message Streams and Kafka

Message streams extend message queues with "write once, read by many" semantics, solving the problem of multiple consumers needing to process the same message independently.

### The Problem: Multiple Consumers

**Example**: Building a blogging platform (like Medium) where upon blog publication:
- Need to index it in search engine (Elasticsearch)
- Need to increment user's total blog count

### Approach 1: Single Broker with Combined Logic

```mermaid
graph LR
    A[Client] --> B[API]
    B --> C[RabbitMQ]
    C --> D[Consumer]
    D --> E[Index to Elasticsearch]
    E --> F[Increment count in DB]
    F --> G[Main DB]
    G --> B
    B --> A
    
    style C fill:#fff9c4,stroke:#f57f17
```

**Issue**: What if one operation succeeds but the other fails?
- Count incremented but not in search index
- In search index but count doesn't match in database

### Approach 2: Two Brokers and Two Consumer Sets

```mermaid
graph LR
    A[Client] --> B[API]
    B --> C[RabbitMQ 1]
    B --> D[RabbitMQ 2]
    C --> E[Search Consumer]
    D --> F[Counter Consumer]
    E --> G[Elasticsearch]
    F --> H[Main DB]
    H --> B
    B --> A
    
    style C fill:#fff9c4,stroke:#f57f17
    style D fill:#fff9c4,stroke:#f57f17
```

**Issue**: Still doesn't solve the problem - API server writes to two brokers, if one fails, we end up in the same situation.

### Approach 3: Message Streams (Kafka)

**Solution**: "Write to one" and "read by many" semantic

```mermaid
graph LR
    A[Client] --> B[API]
    B --> C[Kafka Topic]
    C --> D[Search Consumer]
    C --> E[Counter Consumer]
    D --> F[Elasticsearch]
    E --> G[Main DB]
    G --> B
    B --> A
    
    style C fill:#c8e6c9,stroke:#2e7d32
```

API server pushes one message to Kafka. Both search service and counter service read from the same topic independently.

### Message Streams vs Message Queues

```mermaid
graph TD
    A[Comparison] --> B[Message Queues]
    A --> C[Message Streams]
    
    B --> B1[One message, one consumer]
    B --> B2[Message deleted after read]
    B --> B3[RabbitMQ, AWS SQS]
    
    C --> C1[One message, many consumers]
    C --> C2[Message retained]
    C --> C3[Kafka, AWS Kinesis]
    
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#c8e6c9,stroke:#2e7d32
```

### Kafka Essentials

**Core Concepts**:
- Kafka is a message stream that holds messages
- Internally organized into **topics**
- Each topic has **n partitions**
- Messages sent to a topic are distributed to partitions based on hash key
- **Within partition**: messages are ordered
- **Across partitions**: no ordering guarantee

```mermaid
graph TD
    A[Kafka Topic] --> B[Partition 0]
    A --> C[Partition 1]
    A --> D[Partition 2]
    A --> E[Partition N]
    
    B --> B1[Message 1]
    B --> B2[Message 2]
    B --> B3[Message 3]
    
    C --> C1[Message 4]
    C --> C2[Message 5]
    
    D --> D1[Message 6]
    D --> D2[Message 7]
    D --> D3[Message 8]
    
    style A fill:#c8e6c9,stroke:#2e7d32
    style B fill:#e1f5ff,stroke:#01579b
    style C fill:#e1f5ff,stroke:#01579b
    style D fill:#e1f5ff,stroke:#01579b
    style E fill:#e1f5ff,stroke:#01579b
```

### Kafka Architecture

```mermaid
sequenceDiagram
    participant Producer
    participant Topic
    participant Partition1
    participant Partition2
    participant Consumer1
    participant Consumer2
    
    Producer->>Topic: Send message with key
    Topic->>Partition1: Route based on hash(key)
    Topic->>Partition2: Route based on hash(key)
    
    Consumer1->>Partition1: Read messages
    Consumer2->>Partition2: Read messages
    
    Note over Partition1: Ordered within partition
    Note over Consumer1,Consumer2: Parallel consumption
```

### Limitations of Kafka

**Key Constraint**: Number of consumers = Number of partitions

```
# consumers = # partitions
```

**Implication**: Parallelism of Kafka is limited by the number of partitions configured for that particular topic.

**Example**:
- Topic with 4 partitions can have maximum 4 consumers in a consumer group
- 5th consumer would remain idle
- To increase parallelism, need to increase partitions (cannot be done dynamically without downtime in most cases)

### Kafka vs Traditional Message Queues

| Feature | Message Queues (RabbitMQ) | Message Streams (Kafka) |
|---------|---------------------------|-------------------------|
| **Consumption Model** | One message to one consumer | One message to many consumers |
| **Message Lifecycle** | Deleted after consumption | Retained for configured period |
| **Ordering** | Queue order maintained | Order within partition only |
| **Scalability** | Scale consumers freely | Limited by partition count |
| **Use Case** | Task distribution | Event streaming, multiple processors |

### When to Use Kafka

- Multiple independent systems need the same data
- Event sourcing architecture
- Log aggregation
- Stream processing
- Real-time analytics
- Change Data Capture (CDC)

---

## 15. Pub/Sub Systems

Pub/Sub (Publish/Subscribe) systems provide real-time, push-based message delivery, contrasting with the pull-based approach of message queues and streams.

### Pull vs Push Models

#### Pull Model (Queues & Streams)

```mermaid
sequenceDiagram
    participant Consumer
    participant Broker
    
    loop Continuous Polling
        Consumer->>Broker: Request messages
        Broker-->>Consumer: Return messages (if any)
        Consumer->>Consumer: Process messages
        Note over Consumer: Wait/Poll interval
    end
```

**Advantages**:
- Consumers pull at their own pace
- Consumers don't get overwhelmed
- Back-pressure handling

**Disadvantages**:
- Consumption lag during high ingestion
- Polling overhead
- Not truly real-time

#### Push Model (Pub/Sub)

```mermaid
sequenceDiagram
    participant Publisher
    participant PubSub
    participant Subscriber1
    participant Subscriber2
    participant Subscriber3
    
    Publisher->>PubSub: Publish message
    PubSub->>Subscriber1: Push message
    PubSub->>Subscriber2: Push message
    PubSub->>Subscriber3: Push message
    
    Note over Subscriber1,Subscriber3: Instant delivery
```

**Advantages**:
- Very low latency
- Zero lag
- Truly reactive
- No polling overhead

**Disadvantages**:
- Can overwhelm consumers
- No natural back-pressure
- Consumers must handle messages faster than they arrive

### The Trade-off

```mermaid
graph TD
    A[Messaging Trade-offs] --> B[Pull Model]
    A --> C[Push Model]
    
    B --> B1[Controlled pace]
    B --> B2[Back-pressure]
    B --> B3[Higher latency]
    B --> B4[Polling overhead]
    
    C --> C1[Low latency]
    C --> C2[Zero lag]
    C --> C3[Can overwhelm]
    C --> C4[No back-pressure]
    
    style B fill:#fff9c4,stroke:#f57f17
    style C fill:#c8e6c9,stroke:#2e7d32
```

### Real-time Pub/Sub: When to Use

**Question**: What if we want low latency and zero lag?

**Answer**: Real-time Pub/Sub systems

Instead of consumers pulling messages, messages are pushed to them immediately.

### Example: Redis Pub/Sub

```mermaid
graph TD
    A[Publisher] --> B[Redis Pub/Sub]
    B --> C[Subscriber 1]
    B --> D[Subscriber 2]
    B --> E[Subscriber 3]
    B --> F[Subscriber N]
    
    style B fill:#c8e6c9,stroke:#2e7d32
    style C fill:#e1f5ff,stroke:#01579b
    style D fill:#e1f5ff,stroke:#01579b
    style E fill:#e1f5ff,stroke:#01579b
    style F fill:#e1f5ff,stroke:#01579b
```

### Use Cases for Pub/Sub

#### 1. Message Broadcasting
Send the same message to multiple subscribers instantly.

#### 2. Configuration Push
```mermaid
sequenceDiagram
    participant ConfigService
    participant PubSub
    participant Server1
    participant Server2
    participant Server3
    
    ConfigService->>PubSub: Publish config update
    PubSub->>Server1: Push update
    PubSub->>Server2: Push update
    PubSub->>Server3: Push update
    
    Note over Server1,Server3: All servers receive updates<br/>without polling
```

All servers receive configuration updates instantly without polling for data.

#### 3. Real-time Notifications
- Chat applications
- Live dashboards
- Real-time alerts
- Live score updates

### The Challenge: Consumer Overload

**Problem**: What if consumers receive messages faster than they can process?

```mermaid
graph LR
    A[High Rate Publisher] -->|1000 msgs/sec| B[Pub/Sub]
    B -->|1000 msgs/sec| C[Slow Consumer]
    
    C -->|Can process 100 msgs/sec| D[Bottleneck]
    
    style D fill:#ffcdd2,stroke:#c62828
```

**Solutions**:
1. **Rate limiting** at publisher side
2. **Consumer scaling** - multiple consumers
3. **Buffering layer** - add queue between pub/sub and consumers
4. **Hybrid approach** - pub/sub for notification, queue for processing

### Comparison of Messaging Systems

| Feature | Message Queues | Message Streams | Pub/Sub |
|---------|---------------|-----------------|---------|
| **Model** | Pull | Pull | Push |
| **Latency** | Medium | Medium | Very Low |
| **Consumption** | One-to-one | One-to-many | One-to-many |
| **Persistence** | Temporary | Long-term | None (typically) |
| **Ordering** | Yes | Per partition | No guarantee |
| **Back-pressure** | Yes | Yes | No |
| **Use Case** | Task queues | Event streaming | Real-time broadcast |
| **Examples** | RabbitMQ, SQS | Kafka, Kinesis | Redis Pub/Sub, Cloud Pub/Sub |

### Hybrid Architecture

```mermaid
graph TD
    A[Publisher] --> B[Pub/Sub]
    B --> C[Subscriber 1: Fast]
    B --> D[Subscriber 2: Slow]
    
    D --> E[Message Queue]
    E --> F[Worker Pool]
    F --> G[Process at own pace]
    
    style B fill:#c8e6c9,stroke:#2e7d32
    style C fill:#e1f5ff,stroke:#01579b
    style E fill:#fff9c4,stroke:#f57f17
    style F fill:#e1f5ff,stroke:#01579b
```

**Best of Both Worlds**:
- Use Pub/Sub for immediate notification
- Use Message Queue for actual heavy processing
- Fast subscribers process directly
- Slow subscribers enqueue for later processing

### Summary: Choosing the Right System

```mermaid
flowchart TD
    A[Need Async Communication?] -->|Yes| B{Real-time Required?}
    
    B -->|Yes| C{Can consumers<br/>handle rate?}
    B -->|No| D{Multiple processors<br/>for same data?}
    
    C -->|Yes| E[Pub/Sub]
    C -->|No| F[Hybrid: Pub/Sub + Queue]
    
    D -->|Yes| G[Message Streams<br/>Kafka]
    D -->|No| H[Message Queues<br/>RabbitMQ]
    
    style E fill:#c8e6c9,stroke:#2e7d32
    style F fill:#fff9c4,stroke:#f57f17
    style G fill:#64b5f6,stroke:#1976d2
    style H fill:#ffcc80,stroke:#e65100
```

---
