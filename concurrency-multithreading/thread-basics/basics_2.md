⏺️ ➡️ 🟦 🔵 🟢🔴➡️⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ➡️ What happens if you call run() instead of start()

- Calling run() executes the code in the same thread — no new thread is created.
- Calling start() creates a new thread, and that thread internally calls run().
- start() → creates a new thread
  - JVM allocates a new call stack
  - A new OS-level thread is created
  - Then JVM internally triggers run() on that new thread
  - Actual multithreading happens
- run() → behaves like a normal method

  - No new thread
  - Code executes on the same call stack
  - It becomes a simple method call
  - No multithreading happens

  ```java
  class MyThread extends Thread {
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
  }
  ```

public static void main(String[] args) {
MyThread t = new MyThread();

    t.run();   // prints: main
    t.start(); // prints: Thread-0 (or similar)

}

```
  class MyThread extends Thread {
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}

public static void main(String[] args) {
    MyThread t = new MyThread();

    t.run();   // prints: main
    t.start(); // prints: Thread-0 (or similar)
}

```

## ➡️ Thread vs Runnable

- Thread is a class, Runnable is an interface.
- Runnable represents a task, while Thread represents the worker that executes the task. like Thread = Driver, Runnable = Car
- Thread (extends Thread), Cannot extend any other class (Java supports single inheritance).
- Runnable (implements Runnable), Class can still extend other classes.
- Use Thread only when:override additional Thread methods, create a custom Thread class (rare).
- Use Runnable when: reuse tasks, use ExecutorService, need loose coupling, class already extends another class.

## ➡️ Runnable vs Callable

- Runnable → fire-and-forget task, does not return a value or throw checked exceptions.
- Callable → task that returns a result, returns a value and can throw checked exceptions.
- Callable works with ExecutorService and returns a Future from which we can fetch the result asynchronously, Runnable couldn't do this.
