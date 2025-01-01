# Multi-threading

## multithreading Issues

- Race conditions
  - Two or more threads updating the same value but in their previous state
- Invisible writes
  - One thread writes a value but before it's updated back into the ram,
    another thread reads it. So the write is invisible
- Congestion
- Deadlock
- Nested Monitor Lockout
- Starvation
- Slipped Conditions
- Missed Signals
