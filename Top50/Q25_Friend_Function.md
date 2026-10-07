# Q25 Friend Function

## 🎯 Interview Answer
A **friend function** is a non-member function that is granted access to the `private` and `protected` members of a class. It is declared inside the class with the `friend` keyword, but defined outside.

### ⚙️ Characteristics:
- **Not in the scope** of the class.
- **Cannot be called using an object** (e.g., `obj.friendFunc()` is invalid).
- **Invoked like a normal function**.
- Can be a global function or a member of another class.
- **Violates encapsulation** (C++ is not considered purely OOP partly because of this feature).

---

## 💻 Code Example

```cpp
class Box {
private:
    int length;
public:
    Box(int l) : length(l) {}
    
    // friend declaration
    friend void printLength(Box b);  
};

void printLength(Box b) {
    cout << b.length;  // can access private member 'length'
}
```

---

## 🎯 Summary to Impress
Friend functions are extremely useful for **operator overloading** (like `<<` and `>>` for streams) and in scenarios where two tightly coupled classes need to share internal details securely without exposing them publicly.
