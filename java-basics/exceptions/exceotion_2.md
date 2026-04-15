⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ throw vs throws

### ➡️ throw

- Written inside a method/block
- Throws one exception object
- used to throw exception manually

```java
  throw new ArithmeticException("Invalid value");

 if(age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
  }
```

### ➡️ throws

- Written in method signature
- Can declare multiple exceptions
- Mostly used for checked exceptions
- used to declare exception to caller

```java
void readFile() throws IOException
```

# ⏺️ final, finally and finalize

### ➡️ Final

- Final variable (field)
  - Value cannot be changed once assigned
- final method
  - Cannot be overridden in child class
- final class
  - Cannot be extended (inherited)

### ➡️ Finally

##### 🟦 Always executes

- whether exception occurs or not
- return inside try/catch

##### 🟦 It may NOT run if:

- JVM is terminated → `System.exit(0)`
- JVM crashes (e.g., `OutOfMemoryError`, fatal error)
- Infinite loop / thread killed abruptly

```java
try {
    // code
} catch (Exception e) {
    // handle exception
} finally {
    // always runs ✅
}
```

### ➡️ finalize

- Deprecated since Java 9
- Use alternatives like:
  - try-with-resources
  - AutoCloseable
- Method called before object is garbage collected
- Used for cleanup (like closing resources)

```java
@Override
protected void finalize() throws Throwable {
    // cleanup code
}
```

### ➡️ try-with-resources vs finally

##### 🟦 try-with-resources is safer than finally

- try-with-resources is safer because it automatically closes resources and prevents resource leaks while correctly handling suppressed exceptions
- Automatic resource management
  - Resources (like DB connections, files, streams) are automatically closed
- No chance of forgetting to close them
- No resource leak risk
- Even if an exception occurs → resource still closes properly
- Handles multiple exceptions correctly
  - If:
    - exception occurs in try
    - AND another exception occurs during close()
    - Java preserves the original exception and marks others as suppressed
    - (With finally, original exception can get lost)
- Cleaner & less error-prone code
  - No manual closing needed

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    return br.readLine();
}
```

##### 🟦 What happens if an exception is thrown in finally?

- The exception from finally block survives
- The original exception (from try or catch) is lost / suppressed

```java
try {
    throw new RuntimeException("Exception in try");
} finally {
    throw new RuntimeException("Exception in finally");
}
```

- Output
  - `Exception in thread "main" java.lang.RuntimeException: Exception in finally`

```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("file.txt"));
    return br.readLine();
} finally {
    if (br != null) {
        br.close(); // ❗ can throw exception
    }
}
```

- Issues:
  - You might forget to close resource
  - `close()` can throw exception and override original exception
  - More boilerplate code
