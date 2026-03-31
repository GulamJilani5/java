# Annotations

### @EnableScheduler

- Add the @EnableScheduling annotation in your Spring Boot main class (or any @Configuration class)

### @Scheduler

- Use the @Scheduled annotation on methods in a @Component or @Service.
- **Under the hood how it works:**
  - Spring uses **TaskScheduler** interface behind the scenes.
  - By default, it registers a **ThreadPoolTaskScheduler** bean with only 1 thread.
  - That **ThreadPoolTaskScheduler** internally wraps a **ScheduledExecutorService** (from `java.util.concurrent`).
