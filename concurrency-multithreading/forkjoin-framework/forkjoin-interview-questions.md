✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

# ⏺️ Interview Questions

## ➡️ Explain Fork/Join and when you'd use it" or "Compare it to ThreadPoolExecutor.

### 🟦 Fork/Join vs ThreadPoolExecutor

- **Fork/Join** Compared to **ThreadPoolExecutor** — which is better for independent, unrelated tasks like handling requests — **Fork/Join** is optimized for recursive parallelism and gives better performance for computational problems.
- **Fork/Join** for data crunching, **ThreadPool** for API orchestration.

#### 🔵 Fork/Join vs ThreadPoolExecutor

| Feature               | **Fork/Join Framework**                                | **ThreadPoolExecutor**                                 |
| --------------------- | ------------------------------------------------------ | ------------------------------------------------------ |
| **Introduced**        | Java 7                                                 | Java 5                                                 |
| **Best For**          | Divide-and-conquer, recursive, CPU-bound tasks         | Independent, unrelated tasks (e.g., handling requests) |
| **Task Type**         | RecursiveTask / RecursiveAction                        | Runnable / Callable                                    |
| **Execution Model**   | Fork (split) → parallel execution → Join (combine)     | Submit individual tasks for execution                  |
| **Thread Management** | **Work-stealing**: idle threads pick tasks from others | Fixed or cached thread pools, no stealing              |
| **Performance**       | Highly efficient for parallel computation              | Good for general concurrent workloads                  |
| **Use Case Example**  | Parallel array sum, sorting, searching                 | Web server request handling, async task execution      |
