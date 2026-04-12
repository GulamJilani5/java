🔴🔵☑️✔️ ➡️ ✓→•←⁕⁂※⁜‣

# Different Ways To Create Set(Unique elements)

### ✅ 1. Using HashSet (most common)
```java
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
```
### ✅ 2. Using TreeSet (Sorted order)
```java
Set<String> set = new TreeSet<>();
set.add("Banana");
set.add("Apple");
```

### ✅ 3. Using LinkedHashSet (Maintains insertion order)
```java
Set<String> set = new LinkedHashSet<>();
set.add("A");
set.add("B");
```

### ✅ 4. Using Set.of(...) (Immutable Set – Java 9+)
```java
Set<String> set = Set.of("A", "B", "C"); // Throws exception on duplicates
```

### ✅ 6. Using Stream and Collectors.toSet()
```java
Set<String> set = Stream.of("A", "B", "C").collect(Collectors.toSet());
```

### ✅ 7. Using Arrays.asList() + constructor
```java
Set<String> set = new HashSet<>(Arrays.asList("A", "B", "C"));
```

# Different Methods of Set

| Method                    | Description                                                                          |
| ------------------------- | ------------------------------------------------------------------------------------ |
| `add(E e)`                | Adds element to set if not already present                                           |
| `addAll(Collection c)`    | Adds all elements from another collection                                            |
| `remove(Object o)`        | Removes the specified element                                                        |
| `clear()`                 | Removes all elements                                                                 |
| `contains(Object o)`      | Checks if set contains the element                                                   |
| `isEmpty()`               | Checks if the set is empty                                                           |
| `size()`                  | Returns the number of elements                                                       |
| `iterator()`              | Returns an iterator                                                                  |
| `toArray()`               | Converts set to array                                                                |
| `retainAll(Collection c)` | Retains only the elements in this set that are contained in the specified collection |
| `removeAll(Collection c)` | Removes all elements that exist in the given collection                              |
