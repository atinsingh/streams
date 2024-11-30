Introduction to Java 8 Streams
Java 8 introduced the Stream API as part of its java.util.stream package, bringing functional-style operations to Java. Streams allow you to process sequences of data in a declarative manner, enabling you to focus on what to do with data, rather than how to do it.

What is a Stream?
A Stream is a sequence of elements that can be processed in parallel or sequentially.
Unlike collections, streams do not store data. They are simply a mechanism to process data from collections, arrays, or other data sources.
Streams can be processed lazily and are designed to be composable (you can chain operations).
Why Use Streams?
Declarative: Write more concise and readable code.
Parallel Processing: Streams make it easier to process large datasets in parallel using multi-core processors.
Chaining Operations: Supports function chaining for cleaner and more expressive code.
Creating Streams
Streams can be created from a variety of data sources such as collections, arrays, or individual values.

1. From a Collection
You can create a stream from a collection using the stream() method:

List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
Stream<Integer> stream = list.stream();
2. From an Array
You can create a stream from an array using Arrays.stream():

String[] array = {"a", "b", "c"};
Stream<String> stream = Arrays.stream(array);
3. From Individual Values
You can create a stream directly from individual values using Stream.of():

Stream<String> stream = Stream.of("apple", "banana", "cherry");
4. Using Stream.builder()
You can also use Stream.builder() to create a stream in a more flexible way:

Stream<Integer> stream = Stream.<Integer>builder()
    .add(10)
    .add(20)
    .build();
Stream Operations
Stream operations are classified into intermediate and terminal operations.

Intermediate Operations
Intermediate operations are lazy and do not trigger any computation until a terminal operation is invoked. These operations return a new stream.

1. filter()
The filter() method allows you to filter out elements based on a condition:

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> evenNumbers = numbers.stream()
                                   .filter(n -> n % 2 == 0)
                                   .collect(Collectors.toList());
System.out.println(evenNumbers);  // Output: [2, 4]
2. map()
The map() method transforms each element of the stream using a given function:

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squaredNumbers = numbers.stream()
                                       .map(n -> n * n)
                                       .collect(Collectors.toList());
System.out.println(squaredNumbers);  // Output: [1, 4, 9, 16, 25]
3. distinct()
The distinct() method removes duplicates from the stream:

List<Integer> numbers = Arrays.asList(1, 1, 2, 3, 3, 4);
List<Integer> distinctNumbers = numbers.stream()
                                       .distinct()
                                       .collect(Collectors.toList());
System.out.println(distinctNumbers);  // Output: [1, 2, 3, 4]
4. sorted()
The sorted() method sorts the stream in natural order:

List<Integer> numbers = Arrays.asList(5, 3, 8, 1, 2);
List<Integer> sortedNumbers = numbers.stream()
                                     .sorted()
                                     .collect(Collectors.toList());
System.out.println(sortedNumbers);  // Output: [1, 2, 3, 5, 8]
Terminal Operations
Terminal operations trigger the processing of the stream and produce a result or a side-effect.

1. collect()
The collect() method is used to accumulate the elements of the stream into a collection:

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> result = numbers.stream()
                              .filter(n -> n % 2 == 0)
                              .collect(Collectors.toList());
System.out.println(result);  // Output: [2, 4]
2. forEach()
The forEach() method performs an action for each element:

List<String> fruits = Arrays.asList("apple", "banana", "cherry");
fruits.stream()
      .forEach(fruit -> System.out.println(fruit));
3. reduce()
The reduce() method combines elements of the stream into a single result, such as summing the elements:

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream()
                 .reduce(0, Integer::sum);
System.out.println(sum);  // Output: 15
4. count()
The count() method returns the number of elements in the stream:

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
long count = numbers.stream().count();
System.out.println(count);  // Output: 5
Real-World Examples
Example 1: Processing a List of Employees
Imagine you have a list of employees, and you want to:

Filter employees based on salary.
Get the names of employees who are older than 30.
Sort them alphabetically.
class Employee {
    String name;
    int age;
    double salary;

    Employee(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }
}

List<Employee> employees = Arrays.asList(
    new Employee("John", 25, 50000),
    new Employee("Jane", 32, 70000),
    new Employee("Mark", 45, 80000),
    new Employee("Alice", 35, 60000)
);

List<String> result = employees.stream()
    .filter(e -> e.salary > 60000)  // Filter employees with salary > 60k
    .filter(e -> e.age > 30)        // Filter employees older than 30
    .map(e -> e.name)               // Get names of employees
    .sorted()                       // Sort names alphabetically
    .collect(Collectors.toList());

System.out.println(result);  // Output: [Alice, Jane, Mark]
Parallel Streams
Java 8 Streams provide a powerful way to process large datasets in parallel, making it easier to take advantage of multi-core processors.

How to Use Parallel Streams
You can convert a sequential stream to a parallel stream by calling parallelStream():

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> result = numbers.parallelStream()
                               .map(n -> n * n)
                               .collect(Collectors.toList());
System.out.println(result);
When to Use Parallel Streams
Parallel streams are useful for CPU-bound tasks (e.g., large datasets or computationally heavy operations).
For small datasets, parallel streams may not be beneficial due to the overhead of managing multiple threads.
Performance Considerations
1. Avoid Stateful Operations in Parallel Streams
Stateful operations (like sorted() or distinct()) should be used cautiously with parallel streams because they can affect the correctness of the result.

2. Use Efficient Operations
Chain operations efficiently to minimize unnecessary intermediate steps.

Example of inefficient code:

List<Integer> result = numbers.stream()
    .sorted()
    .filter(n -> n > 5)
    .collect(Collectors.toList());
Optimized version:

List<Integer> result = numbers.stream()
    .filter(n -> n > 5)
    .sorted()
    .collect(Collectors.toList());
Conclusion
Java 8 Streams enable a functional programming style in Java, making data processing more declarative and concise.
Streams support both sequential and parallel processing, allowing you to process data more efficiently.
Intermediate operations (like filter(), map(), and sorted()) are lazy, while terminal operations (like collect(), reduce(), and forEach()) trigger the stream processing.
Use parallel streams for large datasets but ensure they are used where parallelism provides a benefit.
