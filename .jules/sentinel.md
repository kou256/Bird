## 2024-05-23 - Weak PRNG Seeding
**Vulnerability:** The PRNG was seeded using `os.time()`, which only provides second-level resolution, leading to predictable sequences of random numbers if the application starts at the same second.
**Learning:** In Lua/Defold, `math.randomseed(os.time())` does not offer sufficient entropy for games or applications needing less predictable randomness.
**Prevention:** Use `socket.gettime()` combined with modulo arithmetic (`math.floor((socket.gettime() * 10000) % 4294967296)`) to seed the PRNG, ensuring sub-second resolution and sufficient entropy.
