⏺️ ➡️ 🟦 🔵 🟢🔴➡️⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Threads, Runnable, Callable, Future, Thread Pool, Thread Lifecycle

## ➡️ Threads

- Threads are lightweight processes within a program that allow multiple tasks to run concurrently, utilizing CPU resources efficiently.
- Threads share the same memory space, enabling communication but requiring careful synchronization.
- - Primary two ways to create the thread

#### 🟦 Creating Thread

- Extending the Thread Class

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}
public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start(); // Starts the thread
    }

}
```

- Override the `run()` method to define the thread's task.
- Call `start()` to initiate the thread (not `run()` which executes in the current thread).

## ➡️ Runnable

- A task that does something but doesn’t return a result. It has a run() method

#### 🟦 Implementing the Runnable Interface (Preferred):

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running: " + Thread.currentThread().getName());
    }
}
public class Main {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start();
    }
}
```

- More flexible, as it allows the class to extend another class.
- Pass the Runnable object to a Thread constructor.

## ➡️ Callable

- A task that does something and returns a result. It has a `call()` method.

## ➡️ Future

- An object that holds the result of a `Callable task`, which you can check later.

## ➡️ Thread Pool

- A group of reusable threads managed by the `ExecutorService` to run tasks.

## ➡️ Thread Lifecycle

- A thread in Java goes through several states:

#### 🟦 New:

Thread is created but not started (`new Thread()`).

#### 🟦 Runnable:

Thread is ready to run after `start()` is called; it’s waiting for CPU time.

#### 🟦 Running:

Thread is executing its `run()` method.

#### 🟦 Blocked/Waiting:

###### 🔵 Blocked:

Thread is waiting for a monitor `lock` (e.g., in a synchronized block).

###### 🔵 Waiting:

Thread is waiting indefinitely (e.g., `wait()`, `join()`, or `LockSupport.park()`).

###### 🔵 Timed Waiting:

Waiting with a timeout (e.g., `sleep()`, `wait(timeout)`, or `join(timeout)`).

#### 🟦 Terminated:

Thread has completed execution or was stopped.

### Transitions:

- **start():** New → Runnable.
- **Scheduler assigns CPU:** Runnable → Running.
- **sleep(), wait(), or I/O:** Running → Blocked/Waiting/Timed Waiting.
- **notify() or lock release:** Blocked/Waiting → Runnable.
- **run() completes or exception:** Running → Terminated.
