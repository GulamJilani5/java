
# Different Ways To Loop Over An Set

### 1. Enhanced for-loop
```java
for (String s : set) {
System.out.println(s);
}
```

### 2. Using forEach + Lambda
```java
set.forEach(item -> System.out.println(item));
```

### 3. . Using Stream API
```java
set.stream().forEach(System.out::println);
```

### 4. Using Method Reference
```java
set.forEach(System.out::println);
```

### 5. Using Iterator
```java
Iterator<String> iterator = set.iterator();
   while (iterator.hasNext()) {
   System.out.println(iterator.next());
   }
```
