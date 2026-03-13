## 2024-05-18 - Weak Random Number Generator Seeding and Global State

**Vulnerability:** The random number generator (RNG) was seeded with `os.time()`, leading to highly predictable outputs, especially when the game is restarted frequently.

**Learning:** `os.time()` only changes once per second, making it an insufficiently granular seed for a game where the initial setup should vary dynamically. In Lua, `math.randomseed()` alters the global RNG state underneath (standard C `srand` function). Multiple rapid sequential calls to `math.randomseed` in different script initializations are actually an anti-pattern: if these initialize within the exact same timer tick, they'll write identical values to the global seed, effectively resetting the sequence mid-startup and degrading the true randomness of output values.

**Prevention:** Use high-entropy seeding via the `socket` library's `gettime()` function. Calculate the seed via `math.randomseed((socket.gettime() * 10000) % 4294967296)` to incorporate sub-second precision and avoid potential integer overflow issues. Crucially, the RNG should be seeded **exactly once** at the very beginning of the application's lifecycle (e.g., inside the `init()` function of the main game loop / master script like `game_master.script`).
