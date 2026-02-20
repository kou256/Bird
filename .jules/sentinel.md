## 2026-02-20 - Predictable RNG Sequence due to Weak Seeding and Initialization Order

**Vulnerability:** The game used `math.randomseed(os.time())` for seeding, which allows players to predict the obstacle sequence by manipulating the system time (second-level precision). Furthermore, `claypipe.script` initialized its random positions in `init()` potentially before `game_master.script` seeded the RNG, leading to a deterministic first set of obstacles (default seed 1).
**Learning:** In Defold, script initialization order is determined by the collection hierarchy and can be subtle. Relying on a central controller to set global state (like `math.randomseed`) for other components' `init()` functions introduces race conditions.
**Prevention:** Use high-entropy sources like `socket.gettime()` for seeding. Ensure that any component relying on random numbers during initialization either seeds the RNG itself or waits for a signal from a properly initialized controller.
