✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

# ⏺️ Fork/Join Framework

- java 7, `java.util.concurrent`.
- The Fork/Join framework is a concurrency utility in Java.
- It is designed specifically for parallel processing of divide-and-conquer algorithms, this design leverage multiple processors/cores efficiently — unlike normal threads, it uses a special `work-stealing algorithm` to maximize CPU usage.
- It's optimized for workloads where a large task can be recursively broken down ("forked") into smaller subtasks, which are then solved in parallel and combined ("joined") to produce the final result. This makes it ideal for CPU-intensive tasks like sorting, searching, or matrix computations, where you have many small, independent subtasks.
- Unlike general-purpose thread pools (e.g., `ThreadPoolExecutor`), **Fork/Join** uses a **work-stealing scheduler** to minimize idle time: idle worker threads "steal" tasks from busy threads' queues, improving efficiency on multi-core systems.

## ➡️ Key Components

### 🟦 ForkJoinPool

- The main executor service.
- It creates a pool of worker threads (typically one per CPU core) and manages task scheduling.
- You submit tasks to it via `invoke()`, `execute()`, or `submit()`.
- **Example:** `ForkJoinPool pool = new ForkJoinPool();`

### 🟦 ForkJoinTask

- The base class for tasks. It has two main subclasses:

##### 🔵 RecursiveAction

- For tasks that don't return a value (e.g., void operations like updating an array).

##### 🔵 RecursiveTask<V>

- For tasks that return a value (e.g., summing numbers).

### 🟦 Core Methods (used inside your task's `compute()` method):

- **fork():** Asynchronously schedules the subtask on the pool (doesn't block the current thread).
- **join():** Blocks until the subtask completes and retrieves its result (if any).
- **compute():** The abstract method you override to define the task's logic—where you decide to fork subtasks or compute sequentially.

## ➡️ How It Works (High-Level Flow)

- **Divide:** In your task's `compute()` method, check if the task is small enough to solve directly (base case). If not, split it into two (or more) subtasks.
- **Conquer:** Fork the subtasks to run in parallel on different threads.
- **Combine:** Join the subtasks to get their results and merge them into the final result.
  The pool handles **thread management**, **load balancing**, and **exceptions**.

#### 🟦 Parallel Sum of an Array

```java
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.RecursiveTask;

public class ParallelSum extends RecursiveTask<Long> {
    private final long[] numbers;
    private final int start;
    private final int end;
    private static final int THRESHOLD = 1000; // Base case threshold

    public ParallelSum(long[] numbers, int start, int end) {
        this.numbers = numbers;
        this.start = start;
        this.end = end;
    }

    @Override
    protected Long compute() {
        int length = end - start;
        if (length <= THRESHOLD) {
            // Base case: Compute sequentially
            return computeSequentially();
        } else {
            // Fork into two subtasks
            int mid = start + length / 2;
            ParallelSum left = new ParallelSum(numbers, start, mid);
            ParallelSum right = new ParallelSum(numbers, mid, end);
            left.fork();  // Run left in parallel
            Long rightResult = right.compute();  // Run right on current thread (or fork if needed)
            Long leftResult = left.join();  // Wait for left
            return leftResult + rightResult;  // Combine
        }
    }

    private long computeSequentially() {
        long sum = 0;
        for (int i = start; i < end; i++) {
            sum += numbers[i];
        }
        return sum;
    }

    public static void main(String[] args) {
        long[] nums = new long[10000]; // Sample array
        // Initialize nums...
        ForkJoinPool pool = ForkJoinPool.commonPool(); // Use default pool
        long result = pool.invoke(new ParallelSum(nums, 0, nums.length));
        System.out.println("Sum: " + result);
    }
}
```

- **THRESHOLD** decides when to stop splitting.
- **fork()** submits a subtask asynchronously.
- **join()** waits for its result.
- **ForkJoinPool.invoke()** starts the root task.
