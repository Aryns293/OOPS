# Q36 Interface vs Abstract Class

## 🎯 Interview Answer
In C++, there is no separate `interface` keyword (unlike Java or C#). An **interface** in C++ is simply modeled as an abstract class that contains **only** pure virtual functions and has **no data members**.

---

## ⚖️ Key Differences Table

| Feature | Abstract Class | Interface (C++ style) |
|---------|----------------|-----------------------|
| **Methods** | Can have pure virtual + concrete methods | Only pure virtual methods |
| **Data members** | Can have data members | Should not have any data members |
| **Constructors** | Can have constructors | Usually not needed |
| **Multiple inheritance**| Usually inherits from one base class | Can safely inherit from multiple interfaces |
| **Use case** | "is-a" relationship with shared code | "can-do" contract definition |

---

## 💻 Code Example

### 🧩 Interface
```cpp
class Drawable {
public:
    virtual void draw() = 0;    // Pure contract
    virtual ~Drawable() {}      // Virtual destructor
};
```

### 📦 Abstract Class
```cpp
class Shape {
protected:
    int x, y;                   // Data members
public:
    Shape(int x, int y) : x(x), y(y) {}  // Constructor
    virtual double area() = 0;           // Pure virtual function
};
```

---

## 🎯 Summary to Impress
- **Interface** = pure contract (what it can do).
- **Abstract class** = partial implementation + contract (what it is + shared logic).
