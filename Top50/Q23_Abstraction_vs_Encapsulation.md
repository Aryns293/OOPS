# Q23 Abstraction vs Encapsulation

## 🎯 Interview Answer
**Abstraction** is about hiding implementation details and showing only the essential functionality to the user. It focuses on **what** an object does.

**Encapsulation** is about hiding data by bundling it with methods and restricting direct access. It focuses on **how** data is protected and accessed.

---

## ⚖️ Key Differences Table

| Feature | Abstraction | Encapsulation |
|---------|-------------|---------------|
| **Purpose** | Hide complexity, show essential features | Hide data, protect internal state |
| **Level** | Design level | Implementation level |
| **Focus** | **What** an object does | **How** data is accessed |
| **Achieved by** | Abstract classes, interfaces, pure virtual functions | Private members, public getters/setters |
| **Example** | `Shape` with `area()` – user doesn’t know how area is calculated | `Student` with private name, public `getName()` |

---

## 💻 Code Example

### Abstraction
```cpp
class Shape {
public:
    virtual double area() = 0;  // User only knows area() exists
};
```
> **Note:** The implementation details of how the area is calculated are hidden from the user.

### Encapsulation
```cpp
class Student {
private:
    string name;  // Hidden data
public:
    string getName() { return name; }  // Controlled access
    void setName(string n) { name = n; }
};
```
> **Note:** The data (`name`) is bundled with the methods that operate on it and is protected from direct external modification.

---

## 🎯 Summary to Impress
- **Abstraction** = hide complexity, show only essential.
- **Encapsulation** = hide data, bundle with methods.
- They are **complementary**, not competing concepts.
