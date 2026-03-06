## 2024-05-24 - [Medium] Fix weak random number generation
**Vulnerability:** Weak PRNG seeding using `math.randomseed(os.time())`.
**Learning:** In Lua, `os.time()` only provides second-level resolution, leading to predictable seeds if instances start within the same second. Defold environment has `socket` available which provides millisecond resolution with `socket.gettime()`.
**Prevention:** Use high-entropy sources like `socket.gettime()` for seeding in Defold, and apply modulo to prevent integer overflows.
