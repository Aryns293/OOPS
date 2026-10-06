# TOPIC 15: Abstraction

Hiding implementation details, showing only functionality — because the user isn't interested in implementation, and it's safer from a security standpoint.

## In C++
* **Using classes** — access specifiers decide which members are visible externally; the main pillar of abstraction in C++.
* **Header files** — e.g., `pow()` in `math.h` — call the function without knowing how it evaluates the answer.

## In Java

### Using Abstract Class:

* Note: achieves 0–100% abstraction
* Cannot be instantiated
* Contains both abstract AND concrete methods
* Must be inherited to be used

**NOTE:** In C++, a class is abstract when it contains at least one pure virtual function. Abstraction and Abstract Class are conceptually the same in Java and C++, differing only in syntax.

```java
public abstract class ClassName {
   public abstract methodName();
}
```

### Using Interface:
Contains empty methods (no implementation) and variables — a collection of abstract methods and static constants. Every method is public and abstract; no constructor. Along with abstraction, helps achieve multiple inheritance. Implementation provided by clients who implement the interface.

* Note: achieves 100% abstraction.

**Features:**
* Total abstraction
* Multiple interfaces in a class → multiple inheritance
* Loose coupling

```java
public interface XYZ { public void method(); }
```

```java
interface CarStart { void start(); }
interface CarStop { void stop(); }

public class Car implements CarStart, CarStop {
   public void start() { System.out.println("The car engine has been started."); }
   public void stop() { System.out.println("The car engine has been stopped."); }
   
   public static void main(String args[]) {
      Car c = new Car(); c.start(); c.stop();
   }
}
```

## Abstract Class vs Interface

| Abstract Class | Interface |
| :--- | :--- |
| Abstract AND non-abstract methods | Only abstract methods (Java 8+: default/static too) |
| No multiple inheritance | Supports multiple inheritance |
| Final, non-final, static, non-static variables | Only static and final variables |
| Can implement an interface | Cannot provide implementation of an abstract class |
| `abstract` keyword | `interface` keyword |
| Extends one class, implements multiple interfaces | Extends only another interface |
| `extends` | `implements` |
| Can have private/protected members | Members public by default |
| `public abstract class Shape { public abstract void draw(); }` | `public interface Drawable { void draw(); }` |

* Abstraction is hiding complex code
* Abstract class = partial abstraction (0–100%); Interface = full abstraction (100%)
* Abstraction hides implementation, showing only required data/features — hides complexity, provides a clean programming interface
