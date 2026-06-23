# ADR 001: Asynchronous Smart Contract Logging via Celery and Redis

## Summary
To prevent mobile application UI thread-blocking during slow Ethereum Sepolia RPC transactions, the system shall delegate all blockchain audit logging to an asynchronous background task queue managed by Celery and Redis.

## Issue
AgroSmart guarantees the immutability of agricultural recommendations by logging them to an Ethereum smart contract. Direct cryptographic signing and broadcasting to an Ethereum RPC node typically takes between 2 to 15 seconds. Executing this synchronously within the Django HTTP request lifecycle will cause the mobile client to hang, resulting in poor perceived performance and potential HTTP timeout failures, especially in rural areas with unstable cellular connectivity.

## Decision
The system shall offload all blockchain transaction execution to Celery background workers. The Django backend will immediately return the ML recommendation to the client along with a "Pending Sync" status flag. A Celery worker will independently construct, sign, and broadcast the transaction payload to the Sepolia network.

## Status
Decided.

## Details
### Assumptions
- The Machine Learning inference execution time (Random Forest) is exceptionally fast (< 200ms) and can be run synchronously.
- The Redis message broker will be highly available within the cloud deployment environment.
- The Sepolia testnet will experience unpredictable network congestion and latency spikes.

### Constraints
- The farmer must receive immediate agronomic advice regardless of the blockchain network's confirmation status.
- Blockchain transactions must not consume Django worker threads or block concurrent web requests.

### Positions
- **Position A (Synchronous HTTP):** Execute the blockchain write within the HTTP view. Rejected due to severe latency and client timeout risks.
- **Position B (Client-Side Signing):** The mobile application directly signs and broadcasts to Ethereum. Rejected due to extreme security concerns regarding private key management on unsecured client devices and increased cellular data payload sizes.
- **Position C (Asynchronous Queuing with Celery):** Django queues the payload in Redis; Celery handles signing and broadcasting. Selected.

### Argument
Delegating the network-bound, high-latency task of Ethereum broadcasting to an asynchronous worker queue (Celery) is structurally superior because it entirely decouples the core user experience from blockchain network performance. The mobile client receives the required agricultural insight instantaneously. This eventual consistency model perfectly aligns with the non-critical real-time nature of audit logs, prioritizing concurrency and usability over raw, linear execution efficiency.

### Implications
- **Developer Experience:** Increases local environment setup complexity, requiring engineers to orchestrate Redis and Celery workers alongside the Django server.
- **Infrastructure Cost:** Necessitates additional cloud compute resources to host the Redis instance and Celery worker containers.
- **Architectural Downstream Effects:** Introduces a state tracking requirement. The PostgreSQL `RecommendationAuditLog` schema must explicitly track `syncStatus` (e.g., "Pending Sync" vs "Synchronized") and eventually store the asynchronous `blockchainTxHash`.

## Related
### Related decisions
- Decision to utilize Django REST Framework as the primary backend architecture.
- Decision to utilize Ethereum Sepolia for the cryptographic audit trail.

### Related requirements
- **NFR-PERF-001:** The system shall return crop recommendations to the mobile client in under 2 seconds.
- **BRD-FR-020:** The system shall cryptographically log all recommendations to a distributed ledger.

### Related artifacts
- `agro_smart_low_level_design.md` (Section 3.2.1: BlockchainWorker Class Specifications)
- `agro_smart_high_level_design.md` (Execution Strategy)

### Related principles
- **High Availability & Concurrency:** Prioritizing responsive client UI architecture and immediate offline caching over strict immediate consistency.

## Notes
- Benchmarking during the initial Proof of Concept (PoC) revealed that synchronous RPC calls to Sepolia averaged 8.4 seconds. Conversely, asynchronous task hand-off to the Redis broker averaged just 12 milliseconds, confirming the necessity of this architectural separation.
