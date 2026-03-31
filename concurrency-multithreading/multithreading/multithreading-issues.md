️✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

## ➡️ Issues in concurrency/Multithreading

### 🟦 Thread Safety Issues

##### 🔵 Race Condition

- Data corruption(wrong result)
- Happens when two or more threads access and modify the same data concurrently, and the final result becomes unpredictable due to timing/interleaving.
- Both threads execute the operation
  - But due to timing:
    - One result may overwrite the other
    - Some updates may be lost

- **Real-world analogy:** Two chefs add salt to the same soup at the same time without coordination — sometimes too much, sometimes correct, but never predictable.
- **Fix/Solution:** Synchronization (synchronized, ReentrantLock, AtomicInteger).

##### 🔵 Visibility Problem

- Stale data
- Thread A changes a variable, but Thread B doesn’t see the change immediately because the value is cached in CPU core’s local memory/Cached Memory (not flushed to main memory yet).
- Thread B sees old data because it’s looking at its own local copy in CPU cache instead of the updated one in RAM.

- **Real-world analogy:** Chef A updates the recipe on his clipboard but doesn’t tell Chef B — B keeps cooking using the old recipe.
- **Fix/Solution:** Use volatile or synchronization to ensure memory visibility.

### 🟦 Thread Coordination Problems (Locking & Resource Management Issues)

##### 🔵 Deadlock

- stuck forever
- Two or more threads are waiting on each other forever, so nothing moves forward.

- **Real-world analogy:** Chef A has the salt and waits for the pepper from Chef B.
  Chef B has the pepper and waits for the salt from Chef A.
  Both are stuck.
- **Fix/Solution:**
  - Always acquire locks in the same order.
  - Use tryLock() with timeout.
  - Minimize lock usage.

##### 🔵 Starvation

- no chance to run
- A thread never gets CPU time or access to a resource because other threads keep taking it.
  - One thread keeps waiting indefinitely(longer time)
  - System is running, but that thread is ignored
- Thread A releases lock
  - Immediately Thread B grabs it
  - Then Thread C
  - Then B again
    .....
  - Thread D is always waiting and never gets a chance
- **Real-world analogy:** One chef is always ready to cook, but other chefs keep taking the kitchen again and again, so he never gets a chance to cook.
- **Fix/Solution:**
  - Use fair locks (ReentrantLock(true))
  - Avoid thread priority misuse
  - Use proper scheduling / thread pools
