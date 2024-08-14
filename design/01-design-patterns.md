# Design Patterns
https://refactoring.guru/design-patterns/java

## Creational
Creational patterns are ones that create objects, rather than having to instantiate objects directly. This gives the program more flexibility in deciding which objects need to be created for a given case.
 - **Abstract factory**: groups object factories that have a common theme.

 - **Builder**: constructs complex objects by separating construction and representation.

 - **Factory**: method creates objects without specifying the exact class to create.

 - **Prototype**: creates objects by cloning an existing object.

 - **Singleton**: restricts object creation for a class to only one instance.

# Structural
These concern class and object composition. They use inheritance to compose interfaces and define ways to compose objects to obtain new functionality.
 - **Adapter**: allows classes with incompatible interfaces to work together by wrapping its own interface around that of an already existing class.

 - **Bridge**: decouples an abstraction from its implementation so that the two can vary independently.
 ```java
/*
Key Components:
 - Abstraction: Shape
 - Refined Abstraction: Specific shapes like Circle and Square
 - Implementor: Color
 - Concrete Implementors: Specific colors like Red and Blue
*/

  public interface Color {
    void applyColor();
  }

  // Abstraction
  public abstract class Shape {
    //Composition - implementor
    protected Color color;

    //constructor with implementor as input argument
    public Shape(Color c) {
      this.color = c;
    }

    abstract public void applyColor();
  }

  // Refined abstraction
  public class Triangle extends Shape {

    public Triangle(Color c) {
      super(c);
    }

    @Override
    public void applyColor() {
      System.out.print("Triangle filled with color ");
      color.applyColor();
    }
  }
  public class Square extends Shape {
    ...
  }
  
  public class RedColor implements Color {
    public void applyColor() {
      System.out.println("red.");
    }
  }
  public class BlueColor implements Color {
    ... 
  }
 ```

 - **Composite**: composes zero-or-more similar objects so that they can be manipulated as one object.

 - **Decorator**: dynamically adds/overrides behaviour in an existing method of an object.
 ```java
 // abstract decorator class - **note**: that it implements Window
 abstract class WindowDecorator implements Window {
     private final Window windowToBeDecorated; // the Window being decorated

     public WindowDecorator (Window windowToBeDecorated) {
         this.windowToBeDecorated = windowToBeDecorated;
     }
     @Override
     public void draw() {
         windowToBeDecorated.draw(); //Delegation
     }
     @Override
     public String getDescription() {
         return windowToBeDecorated.getDescription(); //Delegation
     }
 }

 // The first concrete decorator which adds vertical scrollbar functionality
 class VerticalScrollBarDecorator extends WindowDecorator {
     public VerticalScrollBarDecorator (Window windowToBeDecorated) {
         super(windowToBeDecorated);
     }

     @Override
     public void draw() {
         super.draw();
         drawVerticalScrollBar();
     }

     private void drawVerticalScrollBar() {
         // Draw the vertical scrollbar
     }

     @Override
     public String getDescription() {
         return super.getDescription() + ", including vertical scrollbars";
     }
 }

 // The second concrete decorator which adds horizontal scrollbar functionality
 class HorizontalScrollBarDecorator extends WindowDecorator {
     public HorizontalScrollBarDecorator (Window windowToBeDecorated) {
         super(windowToBeDecorated);
     }

     @Override
     public void draw() {
         super.draw();
         drawHorizontalScrollBar();
     }

     private void drawHorizontalScrollBar() {
         // Draw the horizontal scrollbar
     }

     @Override
     public String getDescription() {
         return super.getDescription() + ", including horizontal scrollbars";
     }
 }
 ```

 - **Facade**: provides a simplified interface to a large body of code.

 - **Flyweight**: reduces the cost of creating and manipulating a large number of similar objects.
```c#
 // Defines Flyweight object that repeats itself.
public class Flyweight
{
    public string CompanyName { get; set; }
    public string CompanyLocation { get; set; }
    public string CompanyWebsite { get; set; }
    // Bulky data
    public byte[] CompanyLogo { get; set; }
}

public static class FlyweightPointer
{
    public static readonly Flyweight Company = new Flyweight
    {
        CompanyName = "Abc",
        CompanyLocation = "XYZ",
        CompanyWebsite = "www.example.com"
        // Load CompanyLogo here
    };
}

public class MyObject
{
    public string Name { get; set; }
    public string Company => FlyweightPointer.Company.CompanyName;
}
```

 - **Proxy**: provides a placeholder for another object to control access, reduce cost, and reduce complexity.

Example: cache, lazy loading

## Behavioral
Most of these design patterns are specifically concerned with communication between objects.
 - **Chain of responsibility**: delegates commands to a chain of processing objects.

 - **Command**: creates objects that encapsulate actions and parameters.

 - **Interpreter**: implements a specialized language.

 - **Iterator**: accesses the elements of an object sequentially without exposing its underlying representation.

 - **Mediator**: allows loose coupling between classes by being the only class that has detailed knowledge of their methods.

 - **Memento**: provides the ability to restore an object to its previous state (undo).

 - **Observer**: is a publish/subscribe pattern, which allows a number of observer objects to see an event.

 - **State**: allows an object to alter its behavior when its internal state changes.

 - **Strategy**: allows one of a family of algorithms to be selected on-the-fly at runtime.

 - **Template**: method defines the skeleton of an algorithm as an abstract class, allowing its subclasses to provide concrete behavior.

 - **Visitor**: separates an algorithm from an object structure by moving the hierarchy of methods into one object.


# SOLID Principles:
1. **Single Responsibility Principle (SRP)**
   - **Definition:** A class should have only one reason to change, meaning it should have only one job or responsibility.
   - **Explanation:** By adhering to SRP, you ensure that each class in your codebase addresses a single concern, making it easier to understand, test, and maintain. Changes in one part of the application will not affect unrelated parts.

   **Example:** A class handling user authentication should not also be responsible for logging user activities. These should be separate classes.

2. **Open/Closed Principle (OCP)**
   - **Definition:** Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
   - **Explanation:** This principle encourages developers to write code that can be extended without modifying existing code, thereby reducing the risk of introducing bugs when new features are added.

   **Example:** If you have a base class `Shape` with a method `draw()`, you can extend it by creating subclasses like `Circle` and `Rectangle` that override the `draw()` method, without altering the `Shape` class itself.

3. **Liskov Substitution Principle (LSP)**
   - **Definition:** Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.
   - **Explanation:** This principle ensures that a subclass can stand in for its superclass and behave in the same way without causing errors or unexpected behavior.

   **Example:** If you have a class `Bird` with a method `fly()`, and a subclass `Penguin` which cannot fly, then `Penguin` should not inherit from `Bird`. Instead, you might need a different design to respect LSP.

4. **Interface Segregation Principle (ISP)**
   - **Definition:** Clients should not be forced to depend on interfaces they do not use.
   - **Explanation:** This principle advocates for creating specific interfaces rather than a large, general-purpose one. This way, classes that implement these interfaces are only concerned with the methods that are relevant to them.

   **Example:** Instead of a single `Animal` interface with methods `eat()`, `sleep()`, `fly()`, and `swim()`, you could have separate interfaces like `IFlyable` and `ISwimmable` for animals that can fly or swim, respectively.

5. **Dependency Inversion Principle (DIP)**
   - **Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces). Additionally, abstractions should not depend on details. Details should depend on abstractions.
   - **Explanation:** This principle encourages decoupling software modules to enhance flexibility and reusability. By depending on abstractions rather than concrete implementations, changes in low-level modules do not directly impact high-level modules.

   **Example:** Instead of a class `Database` directly depending on a specific `MySQLDatabase` class, it should depend on an interface `IDatabase` that `MySQLDatabase` implements. This way, you can switch to a different database implementation with minimal changes.

### Summary:
- **SRP**: One class, one responsibility.
- **OCP**: Extendable without modification.
- **LSP**: Subtypes should be substitutable for their base types.
- **ISP**: Prefer small, specific interfaces.
- **DIP**: Depend on abstractions, not concretions.
