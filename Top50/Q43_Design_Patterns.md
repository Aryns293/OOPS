# Q43 Design Patterns

## 🎯 Interview Answer
A **design pattern** is a general, reusable solution to a commonly occurring problem in software design. It is not a finished design that can be transformed directly into source code, but rather a template or description of how to solve a problem.

### 📚 Common Patterns
- **Singleton**: Ensures a class has only one instance and provides a global point of access to it.
- **Factory**: Creates objects without exposing the instantiation logic to the client and refers to newly created objects using a common interface.
- **Observer**: Defines a one-to-many dependency so that when one object changes state, all its dependents are notified and updated automatically.
- **Strategy**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable.

---

## 💻 Code Example (Singleton)

```cpp
class Singleton {
private:
    static Singleton* instance;
    Singleton() {}  // Private constructor prevents direct instantiation
    
public:
    static Singleton* getInstance() {
        if (!instance) {
            instance = new Singleton();
        }
        return instance;
    }
};

// Initialize static member
Singleton* Singleton::instance = nullptr;
```

---

## 🎯 Summary to Impress
Design patterns provide **proven solutions** to common architectural problems. Knowing the most common ones (like Singleton, Factory, and Observer) demonstrates mature design thinking.
