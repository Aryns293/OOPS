# Q28 Static Member Function

## 🎯 Interview Answer
A **static member function** is a function declared with the `static` keyword inside a class. It works for the class as a whole, rather than for a specific object instance.

### ⚙️ Key Points:
- **Called using class name**: e.g., `ClassName::func()`.
- **No object required**: Can be called without creating an object of the class.
- **Restricted access**: Can access **only** static data members and other static member functions (cannot access non-static members directly).
- **No `this` pointer**: Because it is not bound to any specific object instance.
- **Cannot be virtual**: Static member functions cannot participate in runtime polymorphism.

---

## 💻 Code Example

```cpp
class Math {
    static int count;
public:
    static int add(int a, int b) { 
        return a + b; 
    }
    
    static void increment() { 
        count++; 
    }
};

// definition of static data member
int Math::count = 0;

int main() {
    cout << Math::add(2, 3);  // Output: 5 (Called using class name, no object needed)
}
```

---

## 🎯 Summary to Impress
Static member functions are **class-level utilities**; they are independent of any object instance and are commonly used for factory methods or utility functions (like math operations).
