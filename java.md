# Java Cheatsheet

This cheatsheet covers core Java syntax, Object-Oriented Programming (OOP) concepts, data types, control flow, methods, arrays, the Collections Framework, and an introduction to the Streams API.

## Basic Syntax & Setup

*   **Compilation and Execution**:
    1.  Save Java code in a file named `ClassName.java`.
    2.  Compile: `javac ClassName.java` (creates `ClassName.class`)
    3.  Run: `java ClassName`
*   **Main Method**: Entry point of a Java application.
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            // args contains command-line arguments
            System.out.println("Hello, World!");
        }
    }
    ```
*   **Comments**:
    ```java
    // This is a single-line comment

    /*
     * This is a
     * multi-line comment.
     */

    /**
     * This is a Javadoc comment.
     * Used for generating API documentation.
     * @param args Command line arguments
     */
    ```
*   **Packages**: Organize classes into namespaces. Declared at the top of the file.
    ```java
    package com.example.myapp;

    import java.util.List; // Import a specific class
    import java.util.*;   // Import all classes in a package (generally less preferred for clarity)

    public class MyClass {
        // ...
    }
    ```
*   **Basic Output**:
    ```java
    System.out.println("Print with a newline.");
    System.out.print("Print without a newline.");
    System.out.printf("Formatted output: Name = %s, Age = %d\n", "Alice", 30);
    ```

## Data Types

*   **Primitive Types**:
    *   `byte`: 8-bit signed integer.
    *   `short`: 16-bit signed integer.
    *   `int`: 32-bit signed integer (most commonly used for integers).
        ```java
        int age = 25;
        ```
    *   `long`: 64-bit signed integer (use `L` suffix, e.g., `long bigNum = 1234567890L;`).
    *   `float`: 32-bit single-precision floating-point (use `f` suffix, e.g., `float price = 19.99f;`).
    *   `double`: 64-bit double-precision floating-point (default for floating-point numbers).
        ```java
        double pi = 3.14159;
        ```
    *   `char`: 16-bit Unicode character (single quotes).
        ```java
        char initial = 'J';
        ```
    *   `boolean`: `true` or `false`.
        ```java
        boolean isActive = true;
        ```
*   **Reference Types (Objects)**:
    *   `String`: Immutable sequence of characters (double quotes).
        ```java
        String greeting = "Hello";
        String name = new String("Java"); // Also possible, but less common for literals
        ```
    *   Arrays: Fixed-size collection of elements of the same type.
    *   Classes, Interfaces, Enums: User-defined or from libraries.

## Variables

*   **Declaration and Initialization**:
    ```java
    int count;         // Declaration
    count = 10;        // Initialization
    String message = "Initialized directly"; // Declaration and Initialization
    final double TAX_RATE = 0.07; // Constant (cannot be reassigned)
    ```
*   **Scope**: Variables can be local (within a method), instance (non-static, per object), or class (static, shared among all objects of the class).

## Operators

*   **Arithmetic**: `+`, `-`, `*`, `/`, `%` (modulo), `++` (increment), `--` (decrement).
*   **Assignment**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`.
*   **Relational (Comparison)**: `==`, `!=`, `>`, `<`, `>=`, `<=`.
*   **Logical**: `&&` (logical AND), `||` (logical OR), `!` (logical NOT).
*   **Bitwise**: `&`, `|`, `^` (XOR), `~` (complement), `<<`, `>>`, `>>>`.
*   **Ternary Operator**: `condition ? expressionIfTrue : expressionIfFalse`
    ```java
    int x = 10, y = 20;
    int max = (x > y) ? x : y; // max will be 20
    ```
*   **instanceof**: Checks if an object is an instance of a particular class or interface.
    ```java
    Object obj = "Some String";
    if (obj instanceof String) {
        String str = (String) obj; // Casting
        System.out.println(str.toUpperCase());
    }
    ```

## Control Flow Statements

*   **If-Else If-Else**:
    ```java
    int score = 85;
    if (score >= 90) {
        System.out.println("Grade A");
    } else if (score >= 80) {
        System.out.println("Grade B");
    } else {
        System.out.println("Grade C or lower");
    }
    ```
*   **Switch Statement**: Works with `byte`, `short`, `char`, `int`, `Enum`, `String` (Java 7+).
    ```java
    char grade = 'B';
    switch (grade) {
        case 'A':
            System.out.println("Excellent!");
            break; // Important to prevent fall-through
        case 'B':
            System.out.println("Good job!");
            break;
        case 'C':
            System.out.println("Fair.");
            break;
        default:
            System.out.println("Needs improvement.");
    }
    ```
*   **For Loop**:
    ```java
    for (int i = 0; i < 5; i++) {
        System.out.println("Iteration: " + i);
    }
    ```
*   **Enhanced For Loop (For-Each Loop)**: For iterating over arrays or collections.
    ```java
    String[] names = {"Alice", "Bob", "Charlie"};
    for (String name : names) {
        System.out.println(name);
    }
    ```
*   **While Loop**:
    ```java
    int count = 0;
    while (count < 3) {
        System.out.println("Count is: " + count);
        count++;
    }
    ```
*   **Do-While Loop**: Executes at least once.
    ```java
    int k = 0;
    do {
        System.out.println("k is: " + k);
        k++;
    } while (k < 3);
    ```
*   **Break and Continue**:
    *   `break`: Exits the loop or switch statement.
    *   `continue`: Skips the current iteration of a loop and proceeds to the next.

## Object-Oriented Programming (OOP)

*   **Classes and Objects**:
    *   A class is a blueprint for creating objects.
    *   An object is an instance of a class.
    ```java
    // Blueprint
    class Car {
        // Instance variables (fields)
        String color;
        String model;
        int year;

        // Constructor (to initialize objects)
        public Car(String color, String model, int year) {
            this.color = color; // 'this' refers to the current object
            this.model = model;
            this.year = year;
        }

        // Instance methods
        void displayInfo() {
            System.out.println("Model: " + model + ", Color: " + color + ", Year: " + year);
        }

        void startEngine() {
            System.out.println("Engine started for " + model);
        }
    }

    // Creating objects (instances)
    // Car myCar = new Car("Red", "Toyota Camry", 2021);
    // Car anotherCar = new Car("Blue", "Honda Civic", 2022);
    // myCar.displayInfo();
    // anotherCar.startEngine();
    ```
*   **Encapsulation**: Bundling data (attributes) and methods that operate on the data within a single unit (class). Often involves making fields `private` and providing `public` getter and setter methods.
    ```java
    class BankAccount {
        private double balance; // Private field

        public BankAccount(double initialBalance) {
            if (initialBalance >= 0) {
                this.balance = initialBalance;
            } else {
                this.balance = 0;
            }
        }

        public double getBalance() { // Getter
            return balance;
        }

        public void deposit(double amount) { // Setter (logic)
            if (amount > 0) {
                balance += amount;
            }
        }
    }
    ```
*   **Inheritance**: A mechanism where a new class (subclass/derived class) inherits properties and methods from an existing class (superclass/base class). Uses the `extends` keyword.
    ```java
    class Animal {
        String name;
        public Animal(String name) { this.name = name; }
        public void eat() { System.out.println(name + " is eating."); }
        public void makeSound() { System.out.println(name + " makes a sound."); }
    }

    class Dog extends Animal { // Dog inherits from Animal
        public Dog(String name) {
            super(name); // Call superclass constructor
        }

        @Override // Annotation: good practice for overridden methods
        public void makeSound() { // Method overriding
            System.out.println(name + " barks.");
        }

        public void fetch() {
            System.out.println(name + " is fetching.");
        }
    }
    // Dog myDog = new Dog("Buddy");
    // myDog.eat(); // Inherited from Animal
    // myDog.makeSound(); // Overridden method in Dog
    // myDog.fetch(); // Method specific to Dog
    ```
*   **Polymorphism**: The ability of an object to take on many forms. Often achieved through method overriding and interfaces. A superclass reference variable can hold a subclass object.
    ```java
    Animal myAnimal = new Dog("Rex"); // Dog object referred by Animal reference
    myAnimal.makeSound(); // Calls Dog's makeSound() method at runtime (dynamic dispatch)
    // myAnimal.fetch(); // Error: fetch() is not in Animal class
    ```
*   **Abstraction**: Hiding complex implementation details and showing only essential features of the object. Achieved using abstract classes and interfaces.
    *   **Abstract Class**: Cannot be instantiated. Can have abstract methods (no body) and concrete methods.
        ```java
        abstract class Shape {
            String color;
            public Shape(String color) { this.color = color; }
            public String getColor() { return color; }
            public abstract double getArea(); // Abstract method (must be implemented by subclasses)
        }

        class Circle extends Shape {
            double radius;
            public Circle(String color, double radius) {
                super(color);
                this.radius = radius;
            }
            @Override
            public double getArea() { return Math.PI * radius * radius; }
        }
        ```
    *   **Interface**: A completely abstract "class" that can only contain abstract methods (implicitly public abstract before Java 8) and static final constants. A class can `implement` multiple interfaces.
        ```java
        interface Drawable {
            void draw(); // Implicitly public abstract
            // Java 8+ allows default and static methods in interfaces
            default void printInfo() { System.out.println("Drawing something."); }
        }
        class Rectangle implements Drawable {
            public void draw() { System.out.println("Drawing a rectangle."); }
        }
        ```

## Methods

*   **Definition**:
    ```java
    // <access_modifier> <static_keyword?> <return_type> <method_name>(<parameter_list>) {
    //    // method body
    //    return <value_of_return_type>; // if return_type is not void
    // }
    public static int addNumbers(int num1, int num2) {
        return num1 + num2;
    }
    ```
*   **Access Modifiers**: `public`, `private`, `protected`, default (package-private).
*   **`static` Keyword**: Static methods belong to the class, not an instance. Called using `ClassName.methodName()`.
*   **Method Overloading**: Multiple methods with the same name but different parameter lists (different number or types of parameters).
    ```java
    class Calculator {
        public int add(int a, int b) { return a + b; }
        public double add(double a, double b) { return a + b; }
        public int add(int a, int b, int c) { return a + b + c; }
    }
    ```

## Arrays

Fixed-size collection of elements of the same type.
```java
// Declaration
int[] numbers;
String[] names;

// Initialization
numbers = new int[5]; // Array of 5 integers, initialized to 0
names = new String[] {"Alice", "Bob", "Charlie"};
int[] scores = {90, 85, 92, 78}; // Shorthand initialization

// Accessing elements (0-indexed)
scores[0] = 95; // Modify element
System.out.println("First score: " + scores[0]);

// Length of array
System.out.println("Number of scores: " + scores.length);

// Iterating through an array
for (int i = 0; i < scores.length; i++) {
    System.out.println(scores[i]);
}
for (int score : scores) { // Enhanced for loop
    System.out.println(score);
}

// Multi-dimensional arrays
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
System.out.println(matrix[1][1]); // Accesses 5
```

## Strings (`java.lang.String`)

Immutable objects.
```java
String str1 = "Hello";
String str2 = " World";
String str3 = str1 + str2; // Concatenation: "Hello World"
System.out.println("Length: " + str3.length());
System.out.println("Char at index 1: " + str3.charAt(1)); // 'e'
System.out.println("Substring: " + str3.substring(6, 11)); // "World"
System.out.println("Uppercase: " + str3.toUpperCase());
System.out.println("Contains 'World': " + str3.contains("World")); // true
System.out.println("Equals 'hello world': " + str3.equalsIgnoreCase("hello world")); // true

// For mutable strings, use StringBuilder or StringBuffer
StringBuilder sb = new StringBuilder("Initial");
sb.append(" String");
sb.insert(0, "My ");
System.out.println(sb.toString()); // "My Initial String"
```

## Collections Framework (`java.util.*`)

Provides interfaces and classes for data structures.

*   **`List` Interface**: Ordered collection, allows duplicates.
    *   `ArrayList`: Resizable array implementation. Good for random access.
        ```java
        List<String> fruitList = new ArrayList<>(); // Diamond operator (Java 7+)
        fruitList.add("Apple");
        fruitList.add("Banana");
        fruitList.add(0, "Orange"); // Insert at index
        System.out.println(fruitList.get(1)); // Apple
        System.out.println("Size: " + fruitList.size());
        fruitList.remove("Banana");
        for (String fruit : fruitList) { System.out.println(fruit); }
        ```
    *   `LinkedList`: Doubly-linked list implementation. Good for frequent insertions/deletions.
        ```java
        List<Integer> numList = new LinkedList<>();
        numList.add(10);
        numList.addFirst(5); // LinkedList specific method
        ```
*   **`Set` Interface**: Collection of unique elements (no duplicates).
    *   `HashSet`: Unordered set, uses hash table. Good performance.
        ```java
        Set<String> uniqueNames = new HashSet<>();
        uniqueNames.add("Alice");
        uniqueNames.add("Bob");
        uniqueNames.add("Alice"); // Not added again
        System.out.println(uniqueNames.contains("Bob")); // true
        ```
    *   `LinkedHashSet`: Ordered set (insertion order), uses hash table and linked list.
    *   `TreeSet`: Sorted set (natural order or by Comparator), uses a tree structure.
        ```java
        Set<Integer> sortedNumbers = new TreeSet<>();
        sortedNumbers.add(50); sortedNumbers.add(20); sortedNumbers.add(80);
        // Iteration will be 20, 50, 80
        ```
*   **`Map` Interface**: Collection of key-value pairs. Keys must be unique.
    *   `HashMap`: Unordered map, uses hash table. Good performance.
        ```java
        Map<String, Integer> studentAges = new HashMap<>();
        studentAges.put("Alice", 20);
        studentAges.put("Bob", 22);
        studentAges.put("Charlie", 20);
        System.out.println("Bob's age: " + studentAges.get("Bob")); // 22
        System.out.println("Contains key 'David': " + studentAges.containsKey("David")); // false
        studentAges.remove("Charlie");
        for (String key : studentAges.keySet()) {
            System.out.println(key + " -> " + studentAges.get(key));
        }
        for (Map.Entry<String, Integer> entry : studentAges.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        ```
    *   `LinkedHashMap`: Ordered map (insertion order or access order).
    *   `TreeMap`: Sorted map (by key's natural order or by Comparator).
*   **`Queue` Interface**: Ordered collection for holding elements prior to processing (FIFO - First-In, First-Out).
    *   `LinkedList` implements `Queue`.
        ```java
        Queue<String> taskQueue = new LinkedList<>();
        taskQueue.offer("Task 1"); // Add to end
        taskQueue.offer("Task 2");
        System.out.println("Next task: " + taskQueue.peek()); // View head, null if empty
        System.out.println("Processing: " + taskQueue.poll()); // Remove and return head, null if empty
        ```

## Streams API (Java 8+)

A sequence of elements supporting sequential and parallel aggregate operations. Does not store elements.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David", "Eve");

// Example: Filter names starting with 'A' or 'B', convert to uppercase, and collect to a new list.
List<String> filteredAndMappedNames = names.stream() // 1. Get a stream
    .filter(name -> name.startsWith("A") || name.startsWith("B")) // 2. Intermediate operation: filter
    .map(String::toUpperCase) // 3. Intermediate operation: map (method reference)
    .sorted() // 4. Intermediate operation: sort
    .collect(Collectors.toList()); // 5. Terminal operation: collect results

// System.out.println(filteredAndMappedNames); // [ALICE, BOB]

// Example: Sum of squares of even numbers
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
int sumOfSquares = numbers.stream()
    .filter(n -> n % 2 == 0)       // Keep even numbers: [2, 4, 6]
    .mapToInt(n -> n * n)          // Square them: [4, 16, 36] (IntStream for sum)
    .sum();                        // Sum them: 56
// System.out.println("Sum of squares of even numbers: " + sumOfSquares);

// Common Stream Operations:
// - Intermediate: filter(), map(), flatMap(), distinct(), sorted(), peek(), limit(), skip()
// - Terminal: forEach(), collect(), reduce(), count(), anyMatch(), allMatch(), noneMatch(), findFirst(), findAny(), min(), max(), toArray()
```

## Exception Handling

Mechanism to handle runtime errors.
```java
try {
    // Code that might throw an exception
    int[] myNumbers = {1, 2, 3};
    System.out.println(myNumbers[10]); // This will cause an ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    System.err.println("Error: Array index is out of bounds.");
    // e.printStackTrace(); // Prints stack trace
} catch (Exception e) { // Catch any other exceptions (more general)
    System.err.println("An unexpected error occurred: " + e.getMessage());
} finally {
    // Code that is always executed, whether an exception occurred or not
    // Useful for cleanup (e.g., closing resources)
    System.out.println("The try-catch block is finished.");
}

// Throwing an exception
// public void setAge(int age) {
//     if (age < 0) {
//         throw new IllegalArgumentException("Age cannot be negative.");
//     }
//     this.age = age;
// }

// Custom Exceptions
// class MyCustomException extends Exception {
//     public MyCustomException(String message) {
//         super(message);
//     }
// }
```
*   **Checked Exceptions**: Must be declared in method signature (`throws`) or handled in `try-catch`. Compiler enforces this. (e.g., `IOException`, `SQLException`).
*   **Unchecked Exceptions (Runtime Exceptions)**: Do not need to be declared or caught, but can be. (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`).

This provides a comprehensive Java cheatsheet. I'll proceed with `php.md`.The `java.md` cheatsheet has been successfully enhanced with detailed syntax examples, code snippets for OOP principles, data types, control flow, methods, arrays, the Collections Framework, and an introduction to the Streams API, all formatted as requested.

Next, I will enhance `php.md`, focusing on its syntax, array manipulation, string functions, superglobals, and basic OOP.
