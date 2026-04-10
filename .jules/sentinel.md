## 2024-05-24 - Weak PRNG Seeding in Lua
**Vulnerability:** The random number generator was seeded with `os.time()`, which only provides 1-second resolution. This makes random events in the game highly predictable, especially if the application is started at a known time.
**Learning:** `os.time()` is insufficient for seeding RNG where unpredictability is required, as it updates too slowly. Using a high-resolution timer from the `socket` library provides much better entropy.
**Prevention:** Always use `socket.gettime()` (or a similarly high-resolution clock) combined with modulo arithmetic (`% 4294967296`) to ensure a valid integer seed when initializing `math.randomseed()` in Defold/Lua environments.
