️✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

## ➡️ Issues in concurrency/Multithreading

### 🟦 Synchronization Problems (Thread Safety Issues)

##### 🔵 Race Condition

Happens when two or more threads try to access and modify the same data at the same time, and the final result depends on which thread wins the race.

- **Real-world analogy:** Two chefs are adding salt to the same soup without talking to each other — sometimes it’s perfect, sometimes way too salty.
- **Fix/Solution:** Synchronization (synchronized, locks, AtomicInteger).

##### 🔵 Visibility Problem

Thread A changes a variable, but Thread B doesn’t see the change immediately because the value is cached in CPU core’s local memory/Cached Memory (not flushed to main memory yet).

- Thread B sees old data because it’s looking at its own local copy in CPU cache instead of the updated one in RAM.

- **Real-world analogy:** Chef A updates the recipe on his clipboard but doesn’t tell Chef B — B keeps cooking using the old recipe.
- **Fix/Solution:** Use volatile or synchronization to ensure memory visibility.

### 🟦 Thread Coordination Problems (Locking & Resource Management Issues)

##### 🔵 Deadlock

Two or more threads are waiting on each other forever, so nothing moves forward.

- **Real-world analogy:** Chef A has the salt and waits for the pepper from Chef B.
  Chef B has the pepper and waits for the salt from Chef A.
  Both are stuck.
- **Fix/Solution:**
  - Always acquire locks in the same order.
  - Use tryLock() with timeout.
  - Minimize lock usage.

##### 🔵 Starvation

Happens when multiple threads access shared mutable data at the same time without proper synchronization.
Final outcome depends on the unpredictable thread scheduling.

- **Real-world analogy:** Two chefs are adding salt to the same soup without talking to each other — sometimes it’s perfect, sometimes way too salty.
- **Fix/Solution:** Synchronization (synchronized, locks, AtomicInteger).
