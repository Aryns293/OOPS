# Q34 Multiple Inheritance Ambiguity

## 🎯 Interview Answer
When a class inherits from two base classes that both have a member (function or variable) with the exact same name, accessing that member directly is **ambiguous**. The compiler doesn’t know which base class's member you intend to use.

---

## 💻 Code Example

```cpp
class A { 
public: 
    void show() { cout << "A\n"; } 
};

class B { 
public: 
    void show() { cout << "B\n"; } 
};

class C : public A, public B { 
};

int main() {
    C obj;
    // obj.show();  // ERROR: ambiguous (is it A::show or B::show?)
    
    obj.A::show();   // OK: Explicitly calls A::show
    obj.B::show();   // OK: Explicitly calls B::show
}
```

---

## 🛠️ Solution
To resolve the ambiguity, use the **scope resolution operator (`::`)** to explicitly specify which base class’s member you want to access.

---

## 🎯 Summary to Impress
Multiple inheritance can easily cause ambiguity when base classes share member names. You can resolve this using the `::` scope resolution operator. (Note: if the ambiguity is caused by inheriting from the same base class twice, e.g., the Diamond Problem, you should use **virtual inheritance**).
