[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/7TXVPuTD)
<br></br>
## 1 – Why we need to use OOP ? Some major OOP languages ? 

OOP models real-world entities using classes and objects, making software development more intuitive and organized. It promotes reusability, scalability, and maintainability by encapsulating data and behavior into objects. This modular approach makes it easier to debug, extend, and collaborate on projects. Additionally, OOP principles like **encapsulation**, **inheritance**, **abstraction** and **polymorphism** help developers write clean and efficient code.

Some major OOP languages are C++, C#, Java, Ruby, Python.
#### Real-Life Example:
**Book** is an object. It has **attributes** like title, page, author etc. and **methods** like borrow(), return(), displayInfo() etc.
<br></br>

## 2 – Interface vs Abstract class ?

Both interfaces and abstract classes support abstraction, making code cleaner and more structured. However, they have key differences in terms of functionality and usage.

| Feature              | Interface | Abstract Class |
|----------------------|-----------|---------------|
| **Method Definition** | Only abstract methods (before Java 8). Supports `default` and `static` methods since Java 8. | Can have both abstract and implemented methods |
| **Fields (Variables)** | Always `public static final` (constants) | Can have instance variables |
| **Constructors**     |  Not allowed |  Allowed |
| **Multiple Inheritance** |  Yes (a class can implement multiple interfaces) |  No (a class can extend only one abstract class) |
| **Access Modifiers** | Methods are always `public` | Methods can be `public`, `protected`, or `private` |
### When to Use:
- Use an **interface** when you need to define a contract for multiple unrelated classes.
- Use an **abstract class** when you want to share code among related classes.
<br></br>

## 3 – Why we need equals and hashcode ? When to override ?

**equals()** and **hashCode()** are two important methods in Java that are used to compare objects and manage them in hash-based collections:

1. **equals()**:
   - Used to compare two objects for **equality** based on their values (not memory references).
   - Must be overridden to provide meaningful comparisons for custom objects.

2. **hashCode()**:
   - Generates a unique integer (hash code) for an object.
   - Used by hash-based collections like `HashMap`, `HashSet`, and `Hashtable` to store and retrieve objects efficiently.

### When to Override:

- Override **equals()** and **hashCode()** when creating custom objects that will be used in hash-based collections.
- If you override **equals()**, you **must** override **hashCode()** to maintain consistency between the two methods.
<br></br>

## 4 – Diamond problem in Java ? How to fix it?

Inheritance is a major OOP concept in Java. Unlike some other languages, Java does not support multiple inheritance. If a class tries to inherit from two or more parent classes that have the same method, Java won't know which method to use. This results in the diamond problem. To resolve this issue, we can use interfaces. Java allows a class to implement as many interfaces as needed, providing a flexible alternative to multiple inheritance.
### Example:
```java
class A { void print() { System.out.println("A"); } }
class B extends A { void print() { System.out.println("B"); } }
class C extends A { void print() { System.out.println("C"); } }
// class D extends B, C { } // Not allowed in Java
```
### Solution with Interfaces (with default keyword):
```java
interface A { default void print() { System.out.println("A"); } }
interface B extends A { default void print() { System.out.println("B"); } }
interface C extends A { default void print() { System.out.println("C"); } }

class D implements B, C {
    @Override
    public void print() { System.out.println("D"); } // Resolves ambiguity
}

public class Main {
    public static void main(String[] args) {
        D obj = new D();
        obj.print(); // Output: D
    }
}
```
`Note: Codes are intentionally shortened.`
<br></br>
## 5 – Why we need Garbage Collector ? How does it run ?

The Garbage Collector is one of the most important features in Java. It automatically removes unreferenced objects from the heap, helping prevent memory leaks and improving application performance. While the GC runs automatically, it can also be triggered manually using methods like **System.gc()** though it’s not guaranteed to run immediately. In the past, developers had to manage memory manually, but the GC now handles this task efficiently. Additionally, Java provides the **finalize()** method, which can be overridden to perform cleanup actions before an object is garbage collected. However, this method is deprecated as of Java 9.

<br>As an extra note, there are four types of Garbage Collectors in Java:</br>
1. **Serial GC**: Suitable for single-threaded applications.
2. **Parallel GC**: Optimized for multi-threaded applications.
3. **G1 GC**: Designed for low-latency applications.
4. **Z GC**: Ideal for applications with very large heaps.
<br></br>
## 6 – Java ‘static’ keyword usage ?

The static keyword in Java is used with variables and methods. When a variable or method is declared as static, it is created when the class is loaded into memory and belongs to the class itself, not individual instances. These static members are stored in the method area, a specific memory area in the JVM. Because of this, we can access static members from any other class without creating an object. Additionally, there is a static initializer block that runs when the class is loaded, even before the constructor is called.

### Example: 
```java
public class Example {
    static int count = 0; // Static variable

    static { // Static block
        System.out.println("Static block executed.");
    }

    static void incrementCount() { // Static method
        count++;
        System.out.println("Count: " + count);
    }

    public static void main(String[] args) {
        incrementCount(); // Call static method
        incrementCount(); // Call static method again
    }
}
```
### Output:
```java
Static block executed.
Count: 1
Count: 2
```
<br></br>
## 7 – Immutability means ? Where, How and Why to use it ?

Immutability means an object’s state cannot be changed after creation. Any change results in a new object. This concept is key for writing clean, predictable, and thread-safe code.

#### **Where is it Used?**
- **Strings & Wrapper Classes**: Immutable by design.
- **Multi-threading**: Thread-safe, no synchronization needed.
- **Caching**: Used in the **String Pool** to avoid redundant objects.
- **Hash-based Collections**: Ensures consistent hash codes for `HashMap`, `HashSet`.
- **Functional Programming**: Encourages stateless programming.

#### **How to Use It?**
1. **Design Immutable Classes**:
   - Use `final` class, `private final` fields, no setters, constructor initialization, and return copies of mutable objects.
2. **Use Immutable Objects**:
   - Prefer immutable objects for thread safety, predictable behavior, or reliable hashing.
   - Example: Use `String` instead of `StringBuilder` for constant values.
3. **Immutable Collections**:
   - Use `List.of()`, `Set.of()`, `Map.of()` for data integrity.
   - Example:
     ```java
     List<String> languages = List.of("Java", "Python", "C++");
     ```
4. **Functional Programming**:
   - Write stateless functions without side effects.
5. **Caching**:
   - Use immutable objects in caches (e.g., `String Pool`) for performance.
6. **Hash-based Collections**:
   - Use immutable objects as keys in `HashMap` or `HashSet`.

#### **Why Use It?**
- **Thread-Safety**: No synchronization issues.
- **Reliable Hashing**: Consistent hash codes for collections.
- **Predictable Behavior**: No unintended changes.
- **Memory Efficiency**: Optimized object reuse (e.g., `String Pool`).
<br></br>
## 8 – Composition and Aggregation means and differences ?
Both Composition and Aggregation represent a **"has-a" relationship** in OOP, but they differ in dependency and coupling strength. 
Composition means tight coupling, Aggregation means loose coupling.


| **Feature**     | **Composition** (Tight Coupling) | **Aggregation** (Loose Coupling) |
|---------------|--------------------------------|--------------------------------|
| **Dependency** | Child depends on the parent | Child can exist independently |
| **Life Cycle** | Parent destroys child | Parent does not destroy child |
| **Flexibility** | Less flexible | More flexible |
| **Example** | `Car → Engine` | `University → Student` |
### Explanation of Examples:
- **Composition (`Car → Engine`)**: The engine is an integral part of the car. If the car is destroyed, the engine is also destroyed. This represents a **strong "has-a" relationship**.
- **Aggregation (`University → Student`)**: The student is associated with the university but can exist independently. If the university is destroyed, the student still exists. This represents a **weak "has-a" relationship**.
<br></br>
## 9 – Cohesion and Coupling means and differences ?

**Cohesion** and **Coupling** are two important additional concepts in OOP:

| **Aspect**            | **Cohesion**                                        | **Coupling**                                      |
|------------------------|----------------------------------------------------|--------------------------------------------------|
| **Definition**         | How closely related the responsibilities of a class are. | The degree of dependency between classes.        |
| **Goal**               | **High cohesion**: A class should have a single, well-defined responsibility. | **Low coupling**: Classes should be independent and interact minimally. |
| **Good Practice**      | A class should do **one thing** and do it well.     | Classes should depend on abstractions, not concrete implementations. |
| **Bad Practice**       | A class handles **multiple unrelated tasks** (low cohesion). | Classes are **tightly dependent** on each other (high coupling). |
| **Impact**             | Improves readability, maintainability, and reusability. | Reduces flexibility and makes the system harder to maintain. |
### Example:

- **High Cohesion**: A `User` class that only handles user-related operations (e.g., `login`, `logout`).
- **Low Coupling**: A `User` class that depends on an abstract `Database` interface rather than a concrete `PostgreSQLDatabase` class.
<br></br>
## 10 - Heap and Stack means and differences ?

In Java, **Heap** and **Stack** are two memory areas used for different purposes:

| **Aspect**            | **Stack**                                            | **Heap**                                           |
|------------------------|------------------------------------------------------|---------------------------------------------------|
| **Stores**             | Primitive types, local variables, object references. | Objects and their instance variables.             |
| **Memory Allocation**  | Static (fixed size at compile time).                 | Dynamic (size can grow or shrink at runtime).     |
| **Speed**              | Faster access.                                       | Slower access compared to stack.                  |
| **Size**               | Smaller in size.                                     | Larger in size.                                   |
| **Lifetime**           | Short-lived (cleared when method execution ends).    | Long-lived (managed by Garbage Collector).        |
| **Structure**          | Last-In-First-Out (LIFO).                            | No specific order (dynamic memory allocation).    |
| **Thread Safety**      | Each thread has its own stack.                       | Shared across all threads.                        |

<br></br>
## 11 – Exception means ? Type of Exceptions ?

**Exceptions** are events that disrupt the normal flow of a program. They are used to handle errors and other exceptional events. There are two main types of exceptions:

| **Aspect**            | **Checked Exceptions**                              | **Unchecked Exceptions**                          |
|------------------------|----------------------------------------------------|--------------------------------------------------|
| **Checked at**         | Compile time.                                      | Runtime.                                         |
| **Handling**           | Must be handled using `try-catch` or `throws`.     | No need to handle explicitly.                    |
| **Inheritance**        | Extend `Exception` class (but not `RuntimeException`). | Extend `RuntimeException` class.                |
| **Examples**           | `IOException`, `SQLException`, `ClassNotFoundException`. | `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException`. |
| **Purpose**            | For recoverable errors (e.g., file not found).      | For programming errors (e.g., null reference).   |
### Example:
```java
// Checked Exception Example
try {
    FileInputStream file = new FileInputStream("file.txt");
} catch (IOException e) {
    System.out.println("File not found: " + e.getMessage());
}

// Unchecked Exception Example
int[] numbers = {1, 2, 3};
System.out.println(numbers[5]); // Throws ArrayIndexOutOfBoundsException
```
<br></br>
## 12 – How to summarize ‘clean code’ as short as possible ?

Clean code is the art of writing and understanding code intentionally. It emphasizes **simplicity**, **readability**, and **maintainability** by following principles like **SOLID**, **DRY**, and **KISS**, as well as using design patterns. The goal is to avoid unnecessary complexity and make the code easy to read, maintain, and extend for everyone.

In my experience, clean code has been a game-changer. For example, I recently refactored a class to follow the **Single Responsibility Principle**, so it easier to test and debug. Clean code not only improves the quality of the software but also makes collaboration with teammates much smoother.

### Key Principles:

1. **SOLID**:
   - **Single Responsibility**: A class should have only one reason to change.
   - **Open/Closed**: Classes should be open for extension but closed for modification.
   - **Liskov Substitution**: Subtypes must be substitutable for their base types.
   - **Interface Segregation**: Clients should not be forced to depend on interfaces they don’t use.
   - **Dependency Inversion**: Depend on abstractions, not concrete implementations.

2. **DRY (Don’t Repeat Yourself)**:
   - Avoid duplication by abstracting common logic into reusable methods or classes.

3. **KISS (Keep It Simple, Stupid)**:
   - Simplicity should be a key goal. Avoid over-engineering.

4. **Design Patterns**:
   - Use proven solutions to common problems (e.g., Singleton, Factory, Observer).
<br></br>
## 13 - What is the method of hiding in Java ?

Method hiding in Java occurs with static methods in the context of polymorphism. When a child class defines a static method with the same signature as a static method in the parent class, the method in the parent class is hidden. For example, if we create a child object with a parent reference and call the static method, the parent class method is executed instead of the child class method. This happens because static methods are bound at compile time based on the reference type, not the object type. In contrast, instance methods are bound at runtime using dynamic method dispatch.
### Example:
```java
class Parent {
    static void print() {
        System.out.println("Parent static method");
    }
}

class Child extends Parent {
    static void print() {
        System.out.println("Child static method");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.print(); // Output: Parent static method (method hiding)
    }
}
```
<br></br>
## 14 - What is the difference between abstraction and polymorphism in Java ?

**Abstraction** and **Polymorphism** are two of the four major OOP concepts in Java. While they are related to OOP, they serve different purposes and have distinct characteristics.

| **Aspect**            | **Abstraction**                                      | **Polymorphism**                                   |
|------------------------|------------------------------------------------------|---------------------------------------------------|
| **Purpose**            | Hides implementation details and shows essential features. | Allows objects to take many forms based on context. |
| **Focus**              | **What** an object does.                             | **How** an object behaves in different contexts.  |
| **Achieved through**   | Abstract classes and interfaces.                     | Method overriding, method overloading, and dynamic method dispatch. |
| **Example**            | Defining a method signature in an interface.         | Overriding a method in a subclass.                |
| **Usage**              | Simplifies design by focusing on high level logic.   | Improves flexibility, code reusability, and extensibility.        |
