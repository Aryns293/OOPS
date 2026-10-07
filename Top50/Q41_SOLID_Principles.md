# Q41 SOLID Principles

## 🎯 Interview Answer
**SOLID** is an acronym for five design principles intended to make software designs more understandable, flexible, and maintainable. 

---

## 📚 The 5 Principles with Examples

### 1️⃣ S – Single Responsibility Principle (SRP)
> *A class should have one, and only one, reason to change. It should encapsulate a single responsibility.*

**Interview Example:**
Instead of having a `User` class that handles both user data and saving to a database, split it into two classes: `User` (for data) and `UserRepository` (for database operations).
```cpp
// ❌ Bad: Two responsibilities
class User {
public:
    string name;
    void saveToDatabase() { /* logic */ } 
};

// ✅ Good: Single responsibility
class User {
public:
    string name;
};

class UserRepository {
public:
    void save(User user) { /* logic */ }
};
```

### 2️⃣ O – Open/Closed Principle (OCP)
> *Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.*

**Interview Example:**
If you want to add a new shape area calculation, you shouldn't modify the existing `AreaCalculator`. Instead, extend a base `Shape` class.
```cpp
// ✅ Good: Open for extension (new shapes), closed for modification
class Shape {
public:
    virtual double getArea() = 0;
};

class Rectangle : public Shape {
    double w, h;
public:
    double getArea() override { return w * h; }
};

class Circle : public Shape {
    double r;
public:
    double getArea() override { return 3.14 * r * r; }
};
```

### 3️⃣ L – Liskov Substitution Principle (LSP)
> *Subtypes must be completely substitutable for their base types without altering the correctness of the program.*

**Interview Example:**
A `Penguin` inherits from `Bird`, but if `Bird` has a `fly()` method, `Penguin` violates LSP because it cannot fly.
```cpp
// ❌ Bad: Violates LSP
class Bird {
public:
    virtual void fly() { cout << "Flying"; }
};

class Penguin : public Bird {
public:
    void fly() override { throw exception(); /* Penguins can't fly! */ }
};

// ✅ Good: Separate behaviors
class Bird { };
class FlyingBird : public Bird {
public:
    virtual void fly() = 0;
};
class Penguin : public Bird { /* No fly method */ };
```

### 4️⃣ I – Interface Segregation Principle (ISP)
> *Many client-specific, small interfaces are better than one general-purpose, large interface. Clients shouldn't be forced to depend on methods they don't use.*

**Interview Example:**
Instead of a giant `IWorker` interface, split it into smaller ones.
```cpp
// ❌ Bad: Robot is forced to implement eat()
class IWorker {
    virtual void work() = 0;
    virtual void eat() = 0;
};

// ✅ Good: Segregated interfaces
class IWorkable {
    virtual void work() = 0;
};
class IFeedable {
    virtual void eat() = 0;
};

class Robot : public IWorkable {
    void work() override { /* ... */ }
};
```

### 5️⃣ D – Dependency Inversion Principle (DIP)
> *High-level modules should not depend on low-level modules. Both should depend on abstractions (interfaces). Abstractions should not depend on details; details should depend on abstractions.*

**Interview Example:**
A `Car` should depend on an `IEngine` interface rather than a concrete `V8Engine` class.
```cpp
class IEngine {
public:
    virtual void start() = 0;
};

class V8Engine : public IEngine {
public:
    void start() override { cout << "V8 started"; }
};

// ✅ Good: Car depends on abstraction (IEngine)
class Car {
    IEngine* engine;
public:
    Car(IEngine* e) : engine(e) {}
    void startCar() { engine->start(); }
};
```

---

## 🎯 Summary to Impress
Following the **SOLID** principles leads to code that is **highly maintainable, loosely coupled, flexible, and easy to test**. It transitions your code from a rigid procedural style to a robust object-oriented architecture.
