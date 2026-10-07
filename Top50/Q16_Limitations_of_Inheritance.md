# Q16 Limitations of Inheritance

## 🎯 Interview Answer
Inheritance is powerful, but it comes with several limitations that can make code rigid and hard to maintain. Interviewers often ask this to see if you understand **when NOT to use inheritance**.

---

## 🚫 Main Limitations of Inheritance

### 1️⃣ Tight Coupling
The child class is tightly coupled to the parent. Any change in the parent’s interface or behavior can break the child. This makes the inheritance hierarchy **fragile**.

### 2️⃣ Fragile Base Class Problem
A seemingly safe change in the base class can unknowingly break derived classes. For example, adding a new method to the base might conflict with a method in a derived class, or changing a method’s implementation can alter behavior in unexpected ways.

### 3️⃣ Complexity in Deep Hierarchies
Multiple levels of inheritance create a complex web. Understanding, debugging, and maintaining deep hierarchies becomes extremely difficult. Method resolution and state tracking can be confusing.

### 4️⃣ Inflexibility
The inheritance relationship is fixed at compile time. You cannot change the parent class at runtime. This limits flexibility compared to **composition**, where you can swap components dynamically.

### 5️⃣ Breaks Encapsulation
To allow derived classes to reuse code, the base class often exposes `protected` members. This weakens encapsulation because derived classes depend on the base class’s internal implementation details.

### 6️⃣ Diamond Problem (Multiple Inheritance)
In languages that support multiple inheritance (like C++), the diamond problem causes ambiguity and requires virtual inheritance, adding extra complexity and memory overhead.

### 7️⃣ Overuse Leads to Poor Design
Inheritance is often misused for mere code reuse when the relationship isn’t truly “is-a.” This leads to wrong abstractions and rigid, unnatural designs.

---

## 💻 Code Example: Fragile Base Class & Name Hiding

```cpp
class Base {
public:
    void foo() { cout << "Base::foo\n"; }
};

class Derived : public Base {
public:
    void foo(int x) { cout << "Derived::foo(int)\n"; }  // Hides Base::foo
};

int main() {
    Derived d;
    // d.foo();      // ERROR: Base::foo is hidden by Derived::foo(int)
    d.Base::foo();   // OK, but awkward
}
```
> Adding `foo(int)` in `Derived` hides `Base::foo()`, which can surprise developers and break existing code that expects `d.foo()` to work.

---

## 🛡️ How to Avoid These Limitations
- **Favor Composition over Inheritance** when the relationship is not clearly “is-a.”
- **Keep inheritance hierarchies shallow.**
- **Design base classes carefully** — they should be stable and built with extension in mind.
- **Use interfaces (pure abstract classes)** to define contracts without tying down the implementation.
- **Apply the Liskov Substitution Principle:** Derived classes must be perfectly usable in place of base classes without breaking expected behavior.

---

## 🎯 Summary to Impress
- **Key Limitations:** Tight coupling, fragile base class, deep complexity, inflexibility, weakened encapsulation, diamond problem.
- These issues make code **brittle and hard to change**.
- **Solution:** Use **composition** for “has-a” relationships, keep hierarchies shallow, and program to interfaces.
- **Golden Rule:** Always ask: “Is this truly an *is-a* relationship?” If not, use composition.
