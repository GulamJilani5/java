⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Concepts

### ➡️ Concurrency vs Multithreading

- Multithreading is one way to achieve concurrency, but concurrency is a broader idea that also includes multiprocessing and async execution.

| **Aspect**     | **Concurrency**                         | **Multithreading**                          |
| -------------- | --------------------------------------- | ------------------------------------------- |
| Scope          | A concept about managing multiple tasks | One method of implementing concurrency      |
| Parallelism    | Might be parallel or just interleaved   | Can be parallel if CPU has multiple cores   |
| Implementation | Can use threads, processes, async, etc. | Always uses multiple threads in one process |

### ➡️ Lock

- A lock is a mechanism that ensures only one thread can access a critical section of code or resource at a time.
- Lock = permission to access shared resource
- Think of a bathroom with a lock:
  - 🚶 Thread 1 enters → locks the door
  - 🚶 Thread 2 comes → must wait
  - 🚶 Thread 1 exits → door unlocks
  - 🚶 Thread 2 enters to bathroom
- Only one person at a time = no conflict
