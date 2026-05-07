✔️🟦🟣🔵🟢🔴🟡🟠⭕🟠⬛🟩🟪🟫 ➡️ ⏺️ ••‣⁎⁕⁜※⁂

# ⏺️ Future vs CompletableFuture and Structured Concurrency(StructuredTaskScope)

## ➡️ Future

- Java 5, `java.util.concurrent`
- A Future represents the result of an asynchronous computation — think of it like a promise that a value will be available in the future.

### 🟦 Key Features

- You submit a task to an ExecutorService.
- You receive a Future object immediately.
- You can later call `future.get()` to retrieve the result
  - This blocks until the computation is complete.

```java
  ExecutorService executor = Executors.newSingleThreadExecutor();

    Future<Integer> future = executor.submit(() -> {
        // Simulate time-consuming task
        Thread.sleep(2000);
        return 42;
    });

    Integer result = future.get(); // Blocks until result is ready
    System.out.println(result);    // 42

    executor.shutdown();

```

### 🟦 Limitations of Future

- **No callbacks** → You can’t attach code to run automatically when the computation finishes.
- **No chaining** → You can’t easily compose multiple async operations.
- `Blocking .get()` → Defeats the purpose of async in many scenarios.

## ➡️ CompletableFuture

- `CompletableFuture` in Java is very similar to Promises in JavaScript.
- java 8, `java.util.concurrent`
- asynchronous, non-blocking, and declarative programming.
- Java doesn’t have `await` syntax but `CompletableFuture` offers a **Promise-like API** with callback chaining and composition

```java
import java.util.concurrent.CompletableFuture;

public class ApiExample {
    public static void main(String[] args) {
        CompletableFuture.supplyAsync(() -> fetchUserFromApi()) // Async task
            .thenApply(user -> transformUser(user))             // Similar to .then()
            .thenAccept(finalUser -> System.out.println("User data: " + finalUser))
            .exceptionally(ex -> {
                System.out.println("Error fetching user: " + ex.getMessage());
                return null;
            });
    }

    static String fetchUserFromApi() {
        // Simulate API fetch (blocking here, but imagine a real HTTP call)
        try { Thread.sleep(1000); } catch (Exception e) {}
        return "{ \"name\": \"John\" }";
    }

    static String transformUser(String userJson) {
        return "Transformed: " + userJson;
    }
}
```

- CompletableFuture vs JavaScript Promises
  - `supplyAsync` starts an async task (similar to returning a Promise).
  - `.thenApply()` works like `.then()` in JS for transformation.
  - `.thenAccept()` works like a `.then()` that does not return anything.

### 🟦 CompletableFuture vs JavaScript Promises

| Concept                       | JavaScript                  | Java                              |
| ----------------------------- | --------------------------- | --------------------------------- |
| Promise                       | `Promise`                   | `CompletableFuture`               |
| Create async task             | `new Promise()` / `fetch()` | `CompletableFuture.supplyAsync()` |
| Chain transformations         | `.then()`                   | `.thenApply()`, `.thenAccept()`   |
| Error handling                | `.catch()`                  | `.exceptionally()`, `.handle()`   |
| Wait for multiple async tasks | `Promise.all()`             | `CompletableFuture.allOf()`       |
| Await result                  | `await` keyword             | `future.join()` / `future.get()`  |

- CompletableFuture is conceptually the same as Promises in JavaScript.
  - Promise = Future,
  - CompletableFuture = Promise with .then(),
  - `.join()` in Java ≈ `await` in JS (but not syntactically sugar-coated).
  - `allOf()` ≈ `Promise.all()`.

## ➡️ Structured Concurrency

### 🟦 Problem Before Structured Concurrency

- You’d use `CompletableFuture` with `allOf()`, `thenApply()`, `join()`…
- It worked, but:

  - Code became callback-heavy (like old JS Promises without async/await).
  - Managing cancellation, errors, and lifecycles was tricky.
  - You needed to manually join or chain futures.

- Similar to **callback hell** in **JavaScript** before `async/await`.

### 🟦 StructuredTaskScope

- java 25, `java.util.concurrent`
- Structured Concurrency treats multiple concurrent tasks as a single unit of work, making them easier to manage, cancel, and handle errors.
- A new API in the `java.util.concurrent` package: `StructuredTaskScope`
  - This allows you to `fork` multiple tasks inside a structured scope and then `join` them — similar to running multiple **async functions** inside an **async function** in **JavaScript**.

```java
   import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.concurrent.StructuredTaskScope;

public class StructuredConcurrencyHttpExample {

    // Create one HttpClient for reuse (thread-safe)
    private static final HttpClient httpClient = HttpClient.newHttpClient();

    static String fetchUser() throws Exception {
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://jsonplaceholder.typicode.com/users/1"))
                .GET()
                .build();

        // Blocking call, but runs inside virtual thread, so it's cheap
        HttpResponse<String> response = httpClient.send(request, HttpResponse.BodyHandlers.ofString());
        return response.body();
    }

    static String fetchPosts() throws Exception {
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://jsonplaceholder.typicode.com/posts?userId=1"))
                .GET()
                .build();

        HttpResponse<String> response = httpClient.send(request, HttpResponse.BodyHandlers.ofString());
        return response.body();
    }

    public static void main(String[] args) throws Exception {
        try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
            // Fork multiple concurrent API calls
            var userTask = scope.fork(StructuredConcurrencyHttpExample::fetchUser);
            var postsTask = scope.fork(StructuredConcurrencyHttpExample::fetchPosts);

            // Wait for both tasks to finish (like Promise.all)
            scope.join();
            scope.throwIfFailed();

            // Get results (like await)
            String userJson = userTask.get();
            String postsJson = postsTask.get();

            System.out.println("👤 User Response:");
            System.out.println(userJson);
            System.out.println("\n📝 Posts Response:");
            System.out.println(postsJson);
        }
    }
}

```

- `fetchUser()` and `fetchPosts()` are real HTTP GET calls.
- Both methods run in virtual threads concurrently thanks to `scope.fork()`.
- `scope.join()` waits for both, like `await Promise.all([...])`.
- `task.get()` is just like `await` — clean, no callbacks, no futures chaining.
