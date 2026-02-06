# Sentinel Journal

## 2026-02-06 - Default Lua RNG State
**Vulnerability:** Weak Random Number Generation
**Learning:** Lua's `math.random` is deterministic by default unless seeded with `math.randomseed`. In game development, this leads to predictable gameplay if not addressed.
**Prevention:** Always seed the RNG in the main initialization script using a time-based seed or similar entropy source.
