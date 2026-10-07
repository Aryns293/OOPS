# Q26 `this` Pointer

## 🎯 Interview Answer
The `this` pointer is a this pointer is an implicit pointer available only inside non-static member functions.
It points to the current object inside a non-static member function.
It tells the function which object it is currently operating on.

### ⚙️ Uses of `this`:
- **Resolve name conflicts**: `this->x = x;` (distinguishes member variables from local parameters).
- **Return the current object**: `return *this;` (useful for method chaining, e.g., in operator overloading).
- **Pass the current object** as a parameter to another function.

### 🚫 Not available in:
- **Static member functions**: Because they are not associated with any specific object.
- **Friend functions**: Because they are not actual members of the class.

---

## 💻 Code Example

```cpp
class Student {
    string name;
public:
    void setName(string name) {
        this->name = name;  // 'this->' distinguishes member from parameter
    }
};
```

---

## 🎯 Summary to Impress
`this` is a hidden pointer passed to the invoking object; it is absolutely essential for disambiguation and method chaining.
