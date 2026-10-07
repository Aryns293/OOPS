# Q04 Class vs Struct

## 🎯 Interview Answer
In C++, `struct` and `class` are almost identical. The only technical differences are:

1. **Default access specifier:**
   - For `class`, members are `private` by default.
   - For `struct`, members are `public` by default.
2. **Default inheritance mode:**
   - When inheriting, `class` uses `private` inheritance by default.
   - `struct` uses `public` inheritance by default.

Other than that, a `struct` can do everything a `class` can — it can have methods, constructors, destructors, inheritance, virtual functions, access specifiers, etc. This is very different from C, where a `struct` only holds data.

---

## ⚖️ Key Differences Table

| Feature | `class` | `struct` |
|---------|---------|----------|
| **Default member access** | `private` | `public` |
| **Default inheritance** | `private` | `public` |
| **Can have methods?** | Yes | Yes |
| **Can have constructors/destructors?** | Yes | Yes |
| **Can inherit?** | Yes | Yes |
| **Can have virtual functions?** | Yes | Yes |
| **Typical usage** | Objects with behavior and encapsulation | Simple data grouping (POD - Plain Old Data) |

---

## 💻 Code Example (C++)

### Default Access
```cpp
// Using struct
struct Point {
    int x, y;  // public by default
    Point(int x, int y) : x(x), y(y) {}
    void display() { cout << x << ", " << y; }
};

// Using class
class PointClass {
    int x, y;  // private by default
public:
    PointClass(int x, int y) : x(x), y(y) {}
    void display() { cout << x << ", " << y; }
};
```
> **Note:** Both work identically. The only difference is that in `struct`, `x` and `y` are public; in `class`, they are private and the constructor/methods require the `public:` specifier.

### Default Inheritance
```cpp
struct Base { int a; };
struct Derived : Base { };           // public inheritance by default

class BaseClass { int a; };
class DerivedClass : BaseClass { };  // private inheritance by default
```

---

## ❓ When to use which?
- **`struct`**: Usually used for passive data structures that just group data together (e.g., `Point`, `Rectangle`, `Node` in a linked list). No complex behavior or invariants.
- **`class`**: Usually used for objects that have encapsulation, invariants, and behavior (e.g., `BankAccount`, `Employee`, `Shape`).

This is a **convention**, not a strict rule. Technically, you can use either for any purpose.

---

## 🎯 Summary to Impress
- In C++, `struct` and `class` are functionally the same.
- **Only differences**: default access and default inheritance mode.
- `struct` defaults to `public`, `class` defaults to `private`.
- Use `struct` for simple data holders; use `class` for encapsulated objects.
- **Never say** “struct doesn’t support inheritance” in C++ — that’s completely wrong. It does.
