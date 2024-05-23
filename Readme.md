## Distributed Transaction ID Generator

### Problem Statement
Develop a distributed transaction ID generator service for a fintech application, ensuring unique UUID-like IDs across multiple Docker instances with data consistency, collision prevention, and a rollback mechanism for failed transactions, achieving sub-100ms latency per request.

### Functional Requirements
1. **ID Generation**
   - Generate unique, UUID-like transaction IDs.
   - Ensure IDs are globally unique across multiple instances using a UUID library compatible with Golang.

2. **Data Consistency**
   - Use a distributed lock service for ensuring exclusive ID generation.
   - Maintain a central registry of issued IDs to avoid duplication, preferably Distributed Redis Cache.

3. **Distributed Architecture**
   - Deploy multiple instances in Docker containers.
   - Ensure horizontal scalability.
   - Utilize service discovery for dynamic instance management.

4. **Collision Prevention**
   - Implement a centralized coordination mechanism (e.g., Zookeeper, etcd).
   - Use a unique shard ID or node ID as part of the UUID to ensure uniqueness.
   - Implement a quorum-based system for consensus on ID issuance.

5. **Rollback Mechanism**
   - Implement a Saga pattern for compensating transactions.
   - Ensure idempotency for compensating transactions.

6. **Monitoring and Logging**
   - Provide detailed logging for transaction tracing and debugging.
   - Implement monitoring for system health and performance metrics.

### Non-Functional Requirements
1. **Performance**
   - Target latency: Sub-100ms per ID generation request.
   - High throughput: Handle thousands of ID generation requests per second.
   - Optimize database queries for low latency.
   - Use in-memory caching (e.g., Redis) to speed up read operations.

2. **Scalability**
   - Horizontally scalable architecture to handle increasing load.
   - Use load balancers to distribute requests evenly across instances.
   - Implement auto-scaling policies based on CPU/memory usage and request rates.
   - Ability to add/remove instances without downtime.

3. **Availability**
   - Achieve 99.99% uptime SLO.
   - Deploy instances across multiple availability zones for redundancy.
   - Implement fault-tolerant mechanisms to handle instance failures.
   - Implement health checks and auto-restart policies for failed instances.

4. **Security**
   - Ensure secure communication between instances using TLS.
   - Implement authentication and authorization for access control (e.g., JWT or OAuth2).

5. **Reliability**
   - Ensure the system can recover from failures without data loss.
   - Use replication for the central registry to ensure high availability.
   - Implement automated backups and disaster recovery plans.
   - Implement redundancy for critical components.

6. **Compliance**
   - Adhere to PCI DSS and GDPR compliance for handling transaction data.
   - Encrypt transaction data at rest and in transit.
   - Implement data access controls and audit logging.

### Getting Started

#### Prerequisites
- Docker
- Golang
- Redis
- Zookeeper or etcd
- Kubernetes (optional for deployment)

#### Installation
1. Clone the repository:
   ```
   git clone https://github.com/yourusername/distributed-id-generator.git
   ```
2. Navigate to the project directory:
   ```
   cd distributed-id-generator
   ```
3. Build the Docker images
   ```
   docker-compose build
   ```

#### Running the Application
1. Start the services:
   ```
   docker-compose up
   ```
2. Access the application at http://localhost:8080.


#### API Endpoints
Generate ID: POST /generate
* Request: {}
* Response: { "id": "generated-uuid" }

#### Monitoring and Logging
* Access logs at http://localhost:8080/logs
* Monitor system health at http://localhost:8080/health
