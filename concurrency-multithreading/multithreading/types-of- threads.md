⏺️ ➡️ 🟦 🔵 🟢🔴⭕🟠🟣🟥🟧✔️ ☑️ • ‣ → ⁕

# ⏺️ Tomcat thread pool, FokJoin thread pool and Custom Executor thread pool

- Tomcat thread pool, FokJoin thread pool and Custom Executor thread pool all are different

```text
Tomcat Pool
    Handles HTTP requests

ForkJoin Pool
    Shared async computations

Custom ExecutorService
    Your dedicated isolated worker pool
```

#### 🟦 If having Machine/Server/EC2 Instance

```text
Machine:
5 CPU cores
16 GB RAM
```

- All kinds of Java threads ultimately compete for the SAME these 5 machine CPU cores.
- Those which don't get cpu will wait in the OS Waiting Queue.
- **OS Scheduler decides:**
  - Which thread runs, For how long and On which core

### ➡️ Scenario 1 — Pure Synchronous (Real External API Call)

##### 🟦 Service Class calling external Service

```java
@Service
public class PaymentService {

    @Autowired
    private RestTemplate restTemplate;

    public String processPayment() {

        String response =
                restTemplate.getForObject(
                        "http://payment-service/pay",
                        String.class
                );

        return response;
    }
}
```

##### 🟦 Flow

```text
Client Request
      ↓
Tomcat Thread starts request
(http-nio-8080-exec-1)
      ↓
Controller
      ↓
PaymentService
      ↓
RestTemplate makes HTTP call
      ↓
Tomcat thread WAITS/BLOCKS
for payment service response
      ↓
Response received
      ↓
Tomcat thread returns response
```

### ➡️ Scenario 2 — ForkJoinPool

##### 🟦 Service Class calling external Service

```java
@Service
public class PaymentService {

    @Autowired
    private RestTemplate restTemplate;

    public String processPayment() throws Exception {

        CompletableFuture<String> future =
                CompletableFuture.supplyAsync(() -> {

                    return restTemplate.getForObject(
                            "http://payment-service/pay",
                            String.class
                    );

                });

        return future.get();
    }
}
```

##### 🟦 Flow

```text
Tomcat Thread
      ↓
submits task to ForkJoinPool
      ↓
ForkJoin worker thread
executes RestTemplate call
      ↓
ForkJoin worker thread blocks
waiting for HTTP response
      ↓
Response received
      ↓
Future completed
      ↓
Tomcat thread gets result
```

### ➡️ Scenario 3 — Custom Executor

- We can use this approach in Bulkhead Pattern

##### 🟦 Configuration

```jav
@Configuration
public class ExecutorConfig {

    @Bean
    public ExecutorService paymentExecutor() {

        return Executors.newFixedThreadPool(50);
    }
}
```

##### 🟦 Service Class calling external Service

```java
@Service
public class PaymentService {

    @Autowired
    private RestTemplate restTemplate;

    @Autowired
    private ExecutorService paymentExecutor;

    public String processPayment() throws Exception {

        CompletableFuture<String> future =
                CompletableFuture.supplyAsync(() -> {

                    return restTemplate.getForObject(
                            "http://payment-service/pay",
                            String.class
                    );

                }, paymentExecutor);

        return future.get();
    }
}
```

##### 🟦 Flow

```text
Tomcat Thread
      ↓
submits task to paymentExecutor
      ↓
paymentExecutor thread
(pool-1-thread-1)
      ↓
RestTemplate HTTP call
      ↓
paymentExecutor thread blocks
waiting for response
      ↓
Response received
      ↓
Future completed
      ↓
Tomcat thread gets result

```
