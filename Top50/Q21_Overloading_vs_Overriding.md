# Q21 Overloading vs Overriding

## 🎯 Interview Answer
**Overloading** and **overriding** are two different forms of polymorphism in C++. The key difference is **when** the method is resolved and **where** it occurs.

- **Overloading** means having multiple functions with the same name but different parameter lists. The compiler selects the appropriate function during compile time, so it is compile-time (static) polymorphism.
- **Overriding** occurs when a derived class provides a new implementation of a virtual function inherited from the base class with the same parameter list. When accessed through a base pointer or reference, the appropriate implementation is selected at runtime using dynamic dispatch, so it is runtime (dynamic) polymorphism.

---

## 💻 Code Example: Overloading

```cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
};
```
> **Note:** All three functions are named `add` but have different parameter lists. The compiler picks the right one based on the arguments. (Overloading typically happens within the same class, but can occur across scopes/inheritance if they form an overload set using `using`).

---

## 💻 Code Example: Overriding

```cpp
class Animal {
public:
    virtual void sound() { cout << "Animal sound\n"; }
};

class Dog : public Animal {
public:
    void sound() override { cout << "Dog barks\n"; }
};

int main() {
    Animal* a = new Dog();
    a->sound();   // Output: Dog barks (resolved at runtime)
}
```
> **Note:** `Dog` overrides `Animal::sound()`. The call through `Animal*` executes `Dog::sound()` at runtime because of the `virtual` keyword.

---

## ⚖️ Key Differences Table

| Feature | Overloading | Overriding |
|---------|-------------|------------|
| **Meaning** | Same name, different parameter lists | Derived class provides new implementation of virtual base function |
| **Binding** | Compile-time | Runtime |
| **Where** | Same overload set/scope; commonly same class | Base + derived class |
| **Parameters** | Must differ | Must be the same |
| **Inheritance** | Not required | Required |
| **`virtual`** | Not required | Required in base for runtime dispatch |
| **Return type** | Cannot differ by return type alone | Same or covariant |
| **Purpose** | Multiple ways to perform an operation | Specialized behavior through polymorphism |
| **Resolution** | Overload resolution by compiler | Dynamic dispatch; implementations typically use vtable/vptr |
| **`override`** | Not applicable | Recommended |

---

## 📊 Diagram: Overloading vs Overriding

```text
Overloading (Compile-time)
--------------------------
Same overload set (commonly same class):
  add(int, int)
  add(double, double)
  add(int, int, int)
(Compiler picks based on arguments)


Overriding (Runtime)
--------------------
Base class:    virtual sound()
                    ^
Derived class: override sound()

Animal* a = new Dog();
a->sound();  -> Dog::sound()  (via dynamic dispatch)
```

---

## 💡 Key Points to Impress
- **Overloading** is resolved by the compiler (static polymorphism).
- **Overriding** requires inheritance and a `virtual` base function (dynamic polymorphism).
- Overloading parameter lists **must differ**.
- Overriding parameter lists **must be identical**.
- **Important:** Overloading is not strictly bound to the same class; it applies to any functions in the same overload set. However, for a simple interview answer, saying "typically within the same class" is acceptable.

---

## 🎯 Summary to Impress
- **Overloading:** same name, different parameters, compile time.
- **Overriding:** base/derived, same parameters, virtual function, runtime.
- **Overloading** = static polymorphism; **overriding** = dynamic polymorphism.
- Know the difference — it’s a classic interview question.
