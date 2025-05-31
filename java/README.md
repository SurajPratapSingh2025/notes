# Java Comprehensive Guide

## Table of Contents

* [Java Concept](#java-concept)
* [Java Core](#java-core)
    1. [Basic Syntax](#basic-syntax)
    2. [Data Types](#data-types)
    3. [Variables](#variables)
    4. [Operators](#operators)
    5. [Control Flow](#control-flow)
    6. [Arrays](#arrays)
    7. [Classes and Objects](#classes-and-objects)
    8. [Inheritance](#inheritance)
    9. [Interfaces](#interfaces)
    10. [Packages](#packages)
    11. [Exceptions](#exceptions)
    12. [Collections Framework](#collections-framework)
    13. [Generics](#generics)
    14. [Lambda Expressions](#lambda-expressions)
    15. [Streams API](#streams-api)
    16. [Multithreading](#multithreading)
    17. [I/O Streams](#io-streams)
    18. [Java 8+ Features](#java-8-features)
* [Reference Information](#reference-information)

## Java Concept

*   Java was created in 1995 by <<!nav>>James Gosling<<!/nav>> at Sun Microsystems (now owned by {Link: Oracle https://www.oracle.com/})
*   Key principles: "Write Once, Run Anywhere" (WORA) through the Java Virtual Machine (JVM)
*   Key features: Object-oriented, platform-independent, robust, secure, multithreaded

## Java Core

# Java Core

<a name="basic-syntax"></a>
## 1. Basic Syntax
Java is a statically typed, object-oriented language. Every Java application starts with a `main` method:
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```
- Case-sensitive
- Class names should be uppercase; method/variable names lowercase camelCase
- Every statement ends with a `;`

<a name="data-types"></a>
## 2. Data Types
Java has two categories of data types:
- **Primitive**: byte, short, int, long, float, double, char, boolean
- **Non-Primitive**: String, Arrays, Classes, Interfaces

<a name="variables"></a>
## 3. Variables
Variables store data values. Types:
- **Local**: declared inside methods
- **Instance**: declared in a class but outside methods
- **Static**: declared with `static` keyword, shared across instances

```java
int a = 10;
String name = "Java";
```

<a name="operators"></a>
## 4. Operators
Used to perform operations on variables and values.
- Arithmetic: `+ - * / %`
- Relational: `== != > < >= <=`
- Logical: `&& || !`
- Assignment: `= += -= *= /=`
- Unary: `++ --`
- Bitwise: `& | ^ ~ << >>`

<a name="control-flow"></a>
## 5. Control Flow
Directs the order of execution.
- Conditional: `if`, `else if`, `else`, `switch`
- Looping: `for`, `while`, `do-while`, `for-each`
- Branching: `break`, `continue`, `return`

<a name="arrays"></a>
## 6. Arrays
Stores multiple values of the same type.
```java
int[] numbers = {1, 2, 3};
String[] names = new String[5];
```

<a name="classes-and-objects"></a>
## 7. Classes and Objects
Java is class-based; objects are instances of classes.
```java
class Car {
    String model;
    void drive() {
        System.out.println("Driving...");
    }
}

Car myCar = new Car();
myCar.drive();
```

<a name="inheritance"></a>
## 8. Inheritance
Mechanism to acquire properties from another class.
```java
class Animal {
    void eat() {}
}

class Dog extends Animal {
    void bark() {}
}
```
- Supports single inheritance, not multiple inheritance

<a name="interfaces"></a>
## 9. Interfaces
A contract that classes implement.
```java
interface Vehicle {
    void start();
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike starting...");
    }
}
```

<a name="packages"></a>
## 10. Packages
Organize related classes and interfaces.
```java
package com.example.myapp;

import java.util.Scanner;
```
Use `package` to define and `import` to access.

<a name="exceptions"></a>
## 11. Exceptions
Handle runtime errors gracefully.
```java
try {
    int x = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
} finally {
    System.out.println("Done");
}
```
Custom exceptions can be created by extending `Exception`.

<a name="collections-framework"></a>
## 12. Collections Framework
Provides data structures like:
- List: `ArrayList`, `LinkedList`
- Set: `HashSet`, `TreeSet`
- Map: `HashMap`, `TreeMap`
- Queue: `PriorityQueue`

```java
List<String> names = new ArrayList<>();
names.add("John");
```

<a name="generics"></a>
## 13. Generics
Allows type parameters for classes/methods.
```java
List<String> list = new ArrayList<>();
```
Prevents `ClassCastException`, increases type safety.

<a name="lambda-expressions"></a>
## 14. Lambda Expressions
Introduced in Java 8 for concise syntax of functional interfaces.
```java
interface MathOperation {
    int operation(int a, int b);
}

MathOperation add = (a, b) -> a + b;
```

<a name="streams-api"></a>
## 15. Streams API
Process collections in a functional style.
```java
List<String> names = Arrays.asList("John", "Jane", "Jack");
names.stream().filter(n -> n.startsWith("J")).forEach(System.out::println);
```

<a name="multithreading"></a>
## 16. Multithreading
Allows concurrent execution.
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Running...");
    }
}
new MyThread().start();
```
Or implement `Runnable` interface.

<a name="io-streams"></a>
## 17. I/O Streams
Used to read/write data (character or byte-based).
- Input: `FileInputStream`, `BufferedReader`
- Output: `FileOutputStream`, `PrintWriter`

```java
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));
String line = reader.readLine();
```

<a name="java-8-features"></a>
## 18. Java 8+ Features
- **Default and static methods in interfaces**
- **Streams API**
- **Lambda expressions**
- **Optional class**
- **Date and Time API (`java.time`)**
- **Functional interfaces (`@FunctionalInterface`)**

```java
Optional<String> name = Optional.of("John");
name.ifPresent(System.out::println);
```

<a name="reference-information"></a>
# Reference Information
For more detailed documentation, visit:
- [Oracle Java Docs](https://docs.oracle.com/javase/8/docs/)
- [Baeldung Java Tutorials](https://www.baeldung.com/)
- [GeeksForGeeks Java](https://www.geeksforgeeks.org/java/)
- [JavaTPoint](https://www.javatpoint.com/java-tutorial)

---

## 📜 License

MIT – free for learning and experimentation.

---

### 🙋‍♂️ Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.


