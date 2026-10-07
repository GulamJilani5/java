# Different Ways To Loop Over The Arrays

### ➡️1)Using a for Loop with Index

       int[] numbers = {10, 20, 30, 40, 50};
       for (int i = 0; i < numbers.length; i++) {
           System.out.println("Element at index " + i + ": " + numbers[i]);
       }

### ➡️2)Using an Enhanced for Loop (foreach)

       int[] numbers = {10, 20, 30, 40, 50};
       for (int num : numbers) {
           System.out.println("Element: " + num);
       }

### ➡️3)Using Stream with Arrays.stream()

       import java.util.Arrays;
       int[] numbers = {10, 20, 30, 40, 50};
       Arrays.stream(numbers)
             .forEach(num -> System.out.println("Element: " + num));

### ➡️4)Using a While Loop

     int[] numbers = {10, 20, 30, 40, 50};
     int i = 0;
     while (i < numbers.length) {
         System.out.println("Element at index " + i + ": " + numbers[i]);
         i++;
     }

### ➡️5)Using Stream with IntStream.range()

    import java.util.stream.IntStream;
    int[] numbers = {10, 20, 30, 40, 50};
    IntStream.range(0, numbers.length)
             .forEach(i -> System.out.println("Element at index " + i + ": " + numbers[i]));

### ➡️6)Using Iterator with Arrays.asList() (for Object Arrays)

    import java.util.Arrays;
    import java.util.Iterator;

    String[] names = {"Alice", "Bob", "Charlie"};
    Iterator<String> iterator = Arrays.asList(names).iterator();
    while (iterator.hasNext()) {
        System.out.println("Element: " + iterator.next());
    }

### ➡️7)Using ListIterator with Arrays.asList() (for Object Arrays)

import java.util.Arrays;
import java.util.ListIterator;

String[] names = {"Alice", "Bob", "Charlie"};
ListIterator<String> iterator = Arrays.asList(names).listIterator();
while (iterator.hasNext()) {
System.out.println("Element: " + iterator.next());
}

### ➡️8) Using Spliterator with Arrays.spliterator()

     import java.util.Arrays;
     import java.util.Spliterator;

     int[] numbers = {10, 20, 30, 40, 50};
     Spliterator.OfInt spliterator = Arrays.spliterator(numbers);
     spliterator.forEachRemaining(num -> System.out.println("Element: " + num));
