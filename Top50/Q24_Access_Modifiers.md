# Q24 Access Modifiers

## 🎯 Interview Answer
**Access modifiers** control the visibility of class members.

- **`private`**: Accessible only within the same class. Not accessible in derived classes or outside.
- **`protected`**: Accessible within the same class and by derived classes. Not accessible outside the hierarchy.
- **`public`**: Accessible from anywhere.

### ⚙️ Default Visibility in C++
- **`class`** → members are `private` by default.
- **`struct`** → members are `public` by default.

---

## ⚖️ Visibility Table

| Modifier | Same Class | Derived Class | Outside |
|----------|------------|---------------|---------|
| **`private`** | ✅ Yes | ❌ No | ❌ No |
| **`protected`** | ✅ Yes | ✅ Yes | ❌ No |
| **`public`** | ✅ Yes | ✅ Yes | ✅ Yes |

---

## 💻 Code Example

```cpp
class Base {
private:   
    int a;  // Accessible only by Base
protected: 
    int b;  // Accessible by Base + Derived
public:    
    int c;  // Accessible by everyone
};

class Derived : public Base {
    void func() {
        // a = 10; // ERROR: private member is inaccessible
        b = 20;    // OK: protected member is accessible in derived class
        c = 30;    // OK: public member is accessible anywhere
    }
};
```

---

## 🎯 Summary to Impress
- Use **`private`** for data encapsulation.
- Use **`protected`** when you want to allow inheritance but hide from the outside world.
- Use **`public`** for defining the interface (methods).
