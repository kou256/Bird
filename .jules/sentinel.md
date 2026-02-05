## 2026-02-05 - Weak RNG in Game Logic
**Vulnerability:** The game's random number generator was unseeded (`math.randomseed` was never called), causing predictable pipe placement on every game launch.
**Learning:** In client-side game engines like Defold/Lua, `math.random` is deterministic by default unless explicitly seeded. This is often overlooked in single-player games but affects gameplay integrity.
**Prevention:** Always initialize RNG with a time-based seed (`math.randomseed(os.time())`) in the main controller's `init` function.
