# Q19 Operator Overloading

## 🎯 Interview Answer
**Operator Overloading** allows an existing C++ operator to be given a meaning for a user-defined type. It lets us use operators with objects in a natural, intuitive way, just like with built-in types. It is a form of compile-time polymorphism.

For example, we can overload `+` for a `Complex` class so that `c1 + c2` adds two complex numbers.

### ❓ Why Operator Overloading?
- Makes code more readable and intuitive (e.g., `c1 + c2` instead of `c1.add(c2)`).
- Allows user-defined types to behave like built-in types.
- Enhances expressiveness without sacrificing performance.

---

## 💻 Example: Overloading `+` for Complex Numbers

```cpp
class Complex {
private:
    double real, imag;
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // Overload + operator
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    void display() const {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(2, 3), c2(4, 5);
    Complex c3 = c1 + c2;   // Calls operator+
    c3.display();           // Output: 6 + 8i
    return 0;
}
```
> **Note:** For this member overload, `c1 + c2` is equivalent to calling `c1.operator+(c2)`. If it were implemented as a non-member, the conceptual transformation would instead be `operator+(c1, c2)`.

---

## 🚫 Which Operators Cannot Be Overloaded?
The following operators **cannot** be overloaded in C++:

| Operator | Description |
|----------|-------------|
| `::` | Scope resolution operator |
| `sizeof` | Size-of operator |
| `.` | Member selector (dot operator) |
| `.*` | Member pointer selector |
| `?:` | Ternary conditional operator |

### Why?
- `::` and `sizeof` are resolved at compile time and are not associated with objects.
- `.` and `.*` are used to access members; overloading them would create ambiguity and break the language’s core syntax.
- `?:` is a control-flow operator; overloading it would complicate parsing and is unnecessary.

> **Note on memory operators:** `new` and `delete` **CAN** be overloaded (along with `new[]` and `delete[]`). Don't assume memory-related operators are off-limits!

---

## 📜 Rules for Operator Overloading
1. At least one operand must involve a user-defined type (class/struct/enum).
2. Cannot change the operator's arity (number of operands).
3. Cannot change precedence.
4. Cannot change associativity.
5. Cannot create new operators (e.g., `**` for exponentiation).
6. `=`, `[]`, `()`, `->`, `->*` must be **non-static member functions**.
7. `<<` and `>>` are typically non-member functions, often declared as `friend`, especially for stream I/O.

---

## 🌟 Deep Dive: Why is `<<` Usually a Non-Member?
Consider printing an object: `cout << obj;`

The operands are:
- Left operand: `cout` (an `ostream` object)
- Right operand: `obj` (a `Complex` object)

If you made `operator<<` a member of `Complex`, the left operand would have to be the `Complex` object, forcing you to write `obj << cout;`. To keep the natural syntax `cout << obj;`, it is implemented as a non-member (often a `friend`):
```cpp
friend ostream& operator<<(ostream& out, const Complex& obj)
```

---

## 📊 Diagram: Operator Overloading Categories

```text
       Operator Overloading
               |
          +----+----+
          |         |
       Member    Non-Member
          |         |
=, [], (), ->, ->*  <<, >>, +, -, ==
```
*(Note: `+`, `-`, `==`, and many others can technically be either member or non-member, while `=`, `[]`, `()`, `->`, `->*` strictly require membership).*

---

## 💡 Key Points to Impress
- **Operator overloading** = compile-time polymorphism.
- Redefines existing operators for user-defined types.
- Makes code intuitive and readable.
- **Cannot overload:** `::`, `sizeof`, `.`, `.*`, `?:`.
- **Cannot create** new operators or change precedence/associativity.
- At least **one operand** must be user-defined.
- `=`, `[]`, `()`, `->`, `->*` must be non-static members.
- `<<` and `>>` are better as non-members to allow standard `cout << obj` syntax.

---

## 🎯 Summary to Impress
- Operator overloading lets you use operators with objects naturally.
- Example: `Complex c3 = c1 + c2;` is cleaner than `c1.add(c2)`.
- **Cannot overload:** `::`, `sizeof`, `.`, `.*`, `?:`.
- **Follow rules:** at least one user-defined operand, no arity/precedence changes.
- It’s a powerful tool for intuitive and expressive code.
