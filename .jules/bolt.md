# Bolt's Performance Journal

## 2025-05-15 - Parallel Session Destruction
**Learning:** Sequential session destruction during client shutdown is a significant bottleneck when multiple sessions are active, as each destruction involves a JSON-RPC request over IPC/Network. Parallelizing this across all SDKs (Go, .NET, Python) brings them to parity with the Node.js implementation and significantly reduces shutdown latency.
**Action:** Always prefer parallel execution for independent I/O-bound cleanup tasks during client shutdown.
