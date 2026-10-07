# Q38 `final` Keyword

## 🎯 Interview Answer
The `final` keyword in C++ is used to prevent further inheritance of a class or to prevent further overriding of a virtual method.

### ⚙️ Usage
- **`final` class**: A class marked as `final` cannot be inherited by any other class.
- **`final` method**: A virtual method marked as `final` cannot be overridden in any derived classes.

---

## 💻 Code Example

### Preventing Class Inheritance
```cpp
class Base final {  
    // This class cannot be inherited
};

class Derived : public Base {  // ERROR: cannot derive from 'final' base 'Base'
};
```

### Preventing Method Overriding
```cpp
class A {
public:
    virtual void show() final {}  // This method cannot be overridden
};

class B : public A {
    void show() override {}  // ERROR: declaration of 'show' overrides a 'final' function
};
```

---

## 🎯 Summary to Impress
The `final` keyword enforces strict design constraints and can also help the compiler perform optimizations (like devirtualization) by explicitly stating that a class or method will not be extended.
