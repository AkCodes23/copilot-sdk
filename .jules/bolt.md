## 2025-05-15 - [Sequential session destruction in SDKs]
**Learning:** All Copilot SDKs (Node.js, Python, Go, .NET) were initially implementing session destruction sequentially during client shutdown. This leads to a linear increase in shutdown time as the number of active sessions grows, especially when individual destructions involve retries and backoff.
**Action:** Parallelize session cleanup using language-specific concurrency primitives (e.g., `Promise.all` in Node.js, `asyncio.gather` in Python, `Task.WhenAll` in .NET, or WaitGroups/Channels in Go) to ensure shutdown time remains constant and minimal.

## 2025-05-16 - [Sequential session destruction in Go and .NET SDKs]
**Learning:** While Node.js and Python SDKs have been optimized for parallel session destruction, Go and .NET SDKs still implement this sequentially. This leads to a linear increase in shutdown time as the number of active sessions grows in those languages.
**Action:** Parallelize session cleanup in Go using goroutines/WaitGroups and in .NET using Task.WhenAll to ensure consistent O(T) shutdown time across all SDKs.
