# Q37 `explicit` Keyword

## 🎯 Interview Answer
The `explicit` keyword in C++ is used on constructors (specifically single-argument constructors) to prevent **implicit type conversions**. 

Without `explicit`, a single-argument constructor can act as an implicit conversion operator. This means the compiler might silently convert a value of the argument type into an object of the class type, which can lead to subtle bugs and unintended behavior.

---

## 💻 Code Example

```cpp
class Complex {
    double real;
public:
    // Marking it explicit prevents implicit double -> Complex conversions
    explicit Complex(double r) : real(r) {}
};

void func(Complex c) {
    // some operations
}

int main() {
    // func(3.0);          // ERROR: no implicit conversion allowed
    
    func(Complex(3.0));    // OK: explicitly constructing the object
    
    return 0;
}
```

---

## 🎯 Summary to Impress
- The `explicit` keyword prevents the compiler from using that constructor for implicit type conversions.
- It helps avoid unintended, silent conversions that can cause hard-to-find bugs.
- **Best Practice:** It is highly recommended to mark single-argument constructors as `explicit` unless you explicitly want to allow implicit conversions.
