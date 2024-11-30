
# Java 8 Streams and Collectors Tutorial

Java 8 introduced the **Streams API**, which provides a powerful way to process sequences of data in a functional programming style. One of the key aspects of Streams is the **Collectors** utility, which is used to perform mutable reduction operations.

## Table of Contents

1. [Introduction to Streams](#introduction-to-streams)
2. [Stream Operations](#stream-operations)
    - [Intermediate Operations](#intermediate-operations)
    - [Terminal Operations](#terminal-operations)
3. [Introduction to Collectors](#introduction-to-collectors)
4. [Common Collectors](#common-collectors)
    - [toList()](#tolist)
    - [toSet()](#toset)
    - [toMap()](#tomap)
    - [joining()](#joining)
    - [groupingBy()](#groupingby)
    - [partitioningBy()](#partitioningby)
    - [counting()](#counting)
    - [summarizingInt(), summarizingDouble(), summarizingLong()](#summarizing-collectors)
5. [Custom Collectors](#custom-collectors)
6. [Conclusion](#conclusion)

---

## Introduction to Streams

A **Stream** in Java is a sequence of elements from a source that supports aggregate operations. It allows you to process collections of data declaratively.

### Example
```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Convert names to uppercase and print
        names.stream()
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```

---

## Stream Operations

Streams support two types of operations: **Intermediate** and **Terminal**.

### Intermediate Operations
These operations transform a stream into another stream. They are **lazy**, meaning they are not executed until a terminal operation is invoked.

Examples:
- `filter(Predicate)`
- `map(Function)`
- `sorted()`
- `distinct()`

### Terminal Operations
These operations produce a result or a side-effect and consume the stream.

Examples:
- `forEach()`
- `collect()`
- `reduce()`
- `count()`

---

## Introduction to Collectors

**Collectors** is a utility class in `java.util.stream` that provides various reduction operations, such as converting a stream into a collection, summarizing elements, grouping, and partitioning.

---

## Common Collectors

### 1. `toList()`

Collects elements into a `List`.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class ToListExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Collect to list
        List<String> uppercaseNames = names.stream()
                                           .map(String::toUpperCase)
                                           .collect(Collectors.toList());

        System.out.println(uppercaseNames);
    }
}
```

---

### 2. `toSet()`

Collects elements into a `Set`.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class ToSetExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Alice");

        // Collect to set (removes duplicates)
        Set<String> uniqueNames = names.stream()
                                       .collect(Collectors.toSet());

        System.out.println(uniqueNames);
    }
}
```

---

### 3. `toMap()`

Collects elements into a `Map`. You must provide key and value mapping functions.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class ToMapExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Collect to map
        Map<String, Integer> nameLengthMap = names.stream()
                                                 .collect(Collectors.toMap(name -> name, name -> name.length()));

        System.out.println(nameLengthMap);
    }
}
```

---

### 4. `joining()`

Concatenates elements into a single `String`.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class JoiningExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Join names with commas
        String result = names.stream()
                             .collect(Collectors.joining(", "));

        System.out.println(result);
    }
}
```

---

### 5. `groupingBy()`

Groups elements by a classifier function.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class GroupingByExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Anna");

        // Group by first letter
        Map<Character, List<String>> groupedByFirstLetter = names.stream()
                                                                .collect(Collectors.groupingBy(name -> name.charAt(0)));

        System.out.println(groupedByFirstLetter);
    }
}
```

---

### 6. `partitioningBy()`

Partitions elements into two groups based on a predicate.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class PartitioningByExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);

        // Partition into even and odd
        Map<Boolean, List<Integer>> partitioned = numbers.stream()
                                                         .collect(Collectors.partitioningBy(n -> n % 2 == 0));

        System.out.println(partitioned);
    }
}
```

---

### 7. `counting()`

Counts the number of elements.

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class CountingExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Count names
        long count = names.stream()
                          .collect(Collectors.counting());

        System.out.println("Count: " + count);
    }
}
```

---

### 8. `summarizingInt()`, `summarizingDouble()`, `summarizingLong()`

Provides summary statistics (e.g., count, sum, average).

#### Example
```java
import java.util.*;
import java.util.stream.*;

public class SummarizingExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Summarize numbers
        IntSummaryStatistics stats = numbers.stream()
                                            .collect(Collectors.summarizingInt(Integer::intValue));

        System.out.println(stats);
    }
}
```

---

## Custom Collectors

You can create custom collectors using the `Collector` interface.

### Example
```java
import java.util.*;
import java.util.stream.*;

public class CustomCollectorExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Custom collector to concatenate names
        String result = names.stream()
                             .collect(Collector.of(
                                 StringBuilder::new,
                                 (sb, s) -> sb.append(s).append(" "),
                                 StringBuilder::append,
                                 StringBuilder::toString
                             ));

        System.out.println(result.trim());
    }
}
```

---

## Conclusion

The Streams API and Collectors utility provide powerful abstractions for processing collections. By understanding and leveraging these features, you can write concise, efficient, and readable Java code.
