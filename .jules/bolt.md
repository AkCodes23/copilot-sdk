## 2025-05-15 - [Sequential session destruction in SDKs]
**Learning:** All Copilot SDKs (Node.js, Python, Go, .NET) were initially implementing session destruction sequentially during client shutdown. This leads to a linear increase in shutdown time as the number of active sessions grows, especially when individual destructions involve retries and backoff.
**Action:** Parallelize session cleanup using language-specific concurrency primitives (e.g., `Promise.all` in Node.js, `asyncio.gather` in Python, `Task.WhenAll` in .NET, or WaitGroups/Channels in Go) to ensure shutdown time remains constant and minimal.
## 2026-02-07 - [Python SDK] Parallelize Session Destruction
**Learning:** Sequential cleanup of network-bound resources (like JSON-RPC sessions) leads to (N)$ shutdown time. Parallelizing with `asyncio.gather` reduces it to (1)$ relative to session count.
**Action:** Always check cleanup/stop methods for sequential IO and parallelize where safe. Implement retry logic for cleanup to match robust SDK patterns.
