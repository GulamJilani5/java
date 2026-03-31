✔️🟦🟣🔵🟢🔴🟡🟠➡️⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

# ⏺️ ThreadLocal (`java.lang.ThreadLocal<T>`)

**ThreadLocal** is a class that provides thread-local storage. This means each thread in a multi-threaded application can have its own independent copy of a variable, and changes to that variable in one thread do not affect its value in other threads. Essentially, ThreadLocal allows you to associate a variable with a specific thread, ensuring thread isolation for that variable.

### ➡️ What Problem Does ThreadLocal Solve?

##### 🟦 Avoiding Synchronization Overhead:

In multi-threaded environments, shared resources (e.g., global or static variables) typically require synchronization (using locks, semaphores, etc.) to prevent race conditions. Synchronization can be costly in terms of performance. ThreadLocal eliminates the need for synchronization by giving each thread its own copy of the variable

##### 🟦 Thread-Specific Context:

Some applications need to maintain thread-specific data, such as user session information, transaction IDs, or database connections, that should not be shared across threads. ThreadLocal provides a clean way to store such data without passing it explicitly through method calls.

##### 🟦 Preventing Data Corruption:

When multiple threads access a shared variable, there's a risk of data corruption or inconsistent states. ThreadLocal ensures that each thread operates on its own instance, avoiding unintended interference.

### ➡️ How to Use ThreadLocal

- 1. **Create a ThreadLocal Instance:** Declare a `ThreadLocal` variable, typically as a static field.
- 2. **Set a Value:** Use `set()` to assign a value to the ThreadLocal for the current thread.
- 3. **Get a Value:** Use `get()` to retrieve the thread-specific value.
- 4. **Remove a Value:** Use `remove()` to clear the value for the current thread to prevent memory leaks.

```java

public class ThreadLocalExample {
    // Create a ThreadLocal variable to store a user ID
    private static final ThreadLocal<String> userId = new ThreadLocal<>();

    public static void main(String[] args) {
        // Simulate two threads with different user IDs
        Runnable task1 = () -> {
            userId.set("User1");
            System.out.println(Thread.currentThread().getName() + " has user ID: " + userId.get());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " after sleep, user ID: " + userId.get());
            userId.remove(); // Clean up
        };

        Runnable task2 = () -> {
            userId.set("User2");
            System.out.println(Thread.currentThread().getName() + " has user ID: " + userId.get());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + " after sleep, user ID: " + userId.get());
            userId.remove(); // Clean up
        };

        // Start two threads
        new Thread(task1, "Thread-1").start();
        new Thread(task2, "Thread-2").start();
    }


}
```

# ⏺️ InheritableThreadLocal

InheritableThreadLocal is a class in Java that extends the ThreadLocal class. It provides thread-local storage like ThreadLocal, but with an additional feature: when a new thread (child thread) is created, it can inherit the thread-local values from its parent thread. This allows child threads to access the same thread-local variable values that were set in the parent thread at the time of their creation.

### ➡️ What Problems Does InheritableThreadLocal Solve?

##### 🟦 Sharing Data with Child Threads

In a program with multiple threads, a main thread (or a thread from a thread pool) might create smaller "child" threads to do specific tasks. If the main thread has some data, like a user ID or transaction details, the child threads might need that same data. InheritableThreadLocal lets child threads automatically get a copy of this data from the parent thread without extra work.

##### 🟦 Avoiding Complicated Data Passing

Without InheritableThreadLocal, you’d have to manually pass this data to child threads, for example, by including it in their setup code. This can make your program messy and lead to mistakes. InheritableThreadLocal makes it easier by automatically sharing the data with child threads.

##### 🟦 Keeping Data Consistent Across Thread Families

In programs where threads create more threads (like a main thread creating workers, which create more workers), InheritableThreadLocal ensures all these related threads can access the same data. This keeps things consistent across the thread family.

### ➡️ How to Use ThreadLocal

- **Create an InheritableThreadLocal Instance:** Declare an InheritableThreadLocal variable, typically as a static field.
- **Set a Value:** Use the set() method to assign a value in the parent thread.
- **Access in Child Threads:** Child threads can use the get() method to retrieve the inherited value.
- **Clean Up:** Use the remove() method to clear the value in the current thread to prevent memory leaks.
- **Optional Customization:** Override the childValue() method to customize how the parent’s value is copied to the child thread.

```java
public class InheritableThreadLocalExample {
    // Create an InheritableThreadLocal variable to store a user ID
    private static final InheritableThreadLocal<String> userId = new InheritableThreadLocal<>();

    public static void main(String[] args) {
        // Set the user ID in the main thread
        userId.set("MainUser");

        System.out.println("Main Thread: " + userId.get());

        // Create a child thread
        Runnable childTask = () -> {
            // Child thread inherits the user ID
            System.out.println("Child Thread: " + userId.get());

            // Modify the user ID in the child thread
            userId.set("ChildUser");
            System.out.println("Child Thread (after modification): " + userId.get());
        };

        // Start the child thread
        Thread childThread = new Thread(childTask, "Child-Thread");
        childThread.start();

        // Wait for the child thread to complete
        try {
            childThread.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Main thread's value remains unchanged
        System.out.println("Main Thread (after child thread): " + userId.get());

        // Clean up
        userId.remove();
    }
}

```
