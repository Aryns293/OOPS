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


<details>
<summary>Difference between Interface and Abstract Class</summary>

### Difference between Interface and Abstract class

In C++, there is no `interface` keyword like Java. An interface is usually implemented using a class containing **only pure virtual functions**.

#### Main difference

| Feature | Abstract Class | Interface |
|---|---|---|
| **Purpose** | Provides a common base + partial implementation | Defines a contract |
| **Functions** | Can have pure virtual + normal functions | Typically only pure virtual functions |
| **Data members** | Can have data members | Usually no data members |
| **Constructor** | Can have constructor | Can technically have one, but interfaces generally don't use state |
| **Implementation** | Can provide some implementation | Generally provides no implementation |
| **Inheritance** | Can be used as a normal base class | Used mainly to specify required behavior |

#### Example
**Abstract class:**
```cpp
class Animal {
protected:
    int age;

public:
    Animal(int a) : age(a) {}

    virtual void sound() = 0;  // pure virtual

    void sleep() {             // implemented
        cout << "Sleeping";
    }
};
```
It has both:
- a requirement: `sound()`
- shared functionality: `sleep()`
- shared state: `age`
So it's an abstract class.

**Interface-style class:**
```cpp
class Drawable {
public:
    virtual void draw() = 0;
    virtual void resize() = 0;

    virtual ~Drawable() = default;
};
```
It basically says:
*"Any class implementing me must provide draw() and resize()."*
It doesn't provide implementation or maintain object state.

#### Very important for interviews
**Don't say:**
*"An interface cannot have implementation."*
That's language-dependent.

**For C++, the better answer is:**
*"C++ doesn't have a dedicated interface keyword. We generally model an interface using a class with pure virtual functions. An abstract class can contain pure virtual functions but can also contain implemented methods, data members, and constructors. So an interface is essentially a stricter form of an abstract base class intended primarily to define a contract."*

**And one more important point:**
C++ allows multiple inheritance, so a class can implement multiple interface-like classes:
```cpp
class Printable {
public:
    virtual void print() = 0;
};

class Scannable {
public:
    virtual void scan() = 0;
};

class Printer : public Printable, public Scannable {
public:
    void print() override {}
    void scan() override {}
};
```
</details>
