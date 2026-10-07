# Q02 Four Pillars of OOP

## 🎯 Interview Answer
The four pillars of OOP are **Encapsulation**, **Abstraction**, **Inheritance**, and **Polymorphism**. Together, they make software modular, reusable, secure, and flexible.

---

### 1️⃣ Encapsulation
- **Definition:** Bundling data and the methods that operate on that data into a single unit (class), and restricting direct access to the internal state.
- **Why:** Protects data from unintended modifications, enforces validation, and hides complexity.

```cpp
class Student {
private:
    string name;
    int rollNo;
public:
    void setName(string n) { name = n; }
    string getName() { return name; }
};
```
> **Note:** Here, `name` and `rollNo` are private. External code can only access them via public methods, where we can add validation.

---

### 2️⃣ Abstraction
- **Definition:** Hiding complex implementation details and exposing only the essential functionality to the user.
- **Why:** Reduces complexity, lets us focus on **what** an object does rather than **how** it does it.

```cpp
class Car {
public:
    virtual void start() = 0;  // Pure virtual
    virtual void accelerate() = 0;
};
```
> **Note:** The user just calls `start()` or `accelerate()` without knowing the internal engine mechanics.

---

### 3️⃣ Inheritance
- **Definition:** A mechanism where one class (child/derived) acquires the properties and behaviors of another class (parent/base).
- **Why:** Promotes code reusability and establishes an “is-a” relationship.

```cpp
class Vehicle {
public:
    void fuel() { cout << "Refueling"; }
};

class Car : public Vehicle {
public:
    void drive() { cout << "Driving"; }
};
```
> **Note:** `Car` inherits `fuel()` from `Vehicle` and adds its own `drive()`.

---

### 4️⃣ Polymorphism
- **Definition:** The ability of a single interface to represent different underlying forms. A method can behave differently based on the object.
- **Why:** Enables flexibility and extensibility — same function call, different behavior.

```cpp
class Shape {
public:
    virtual double area() = 0;
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14 * r * r; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, h) : w(w), h(h) {}
    double area() override { return w * h; }
};

void printArea(Shape* s) { 
    cout << s->area(); 
}
```
> **Note:** `printArea()` works with any `Shape` — `Circle`, `Rectangle`, etc. — without knowing the exact type at compile time.

---

## 📊 Quick Diagram (Mental Picture)

```text
               OOP Pillars
                    |
   +---------+---------+---------+---------+
   |         |         |         |         |
Encapsulation Abstraction Inheritance Polymorphism
   |         |         |         |
Data Hiding  Hide Impl   Reuse Code  Many Forms
```

---

## 🎯 Summary to Impress
- **Encapsulation** = Data security.
- **Abstraction** = Simplicity.
- **Inheritance** = Reusability.
- **Polymorphism** = Flexibility.

These four pillars together enable modular, maintainable, and scalable software design.
