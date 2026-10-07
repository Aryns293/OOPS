# Q33 Object Slicing

## 🎯 Interview Answer
**Object slicing** occurs when a derived class object is assigned to a base class object **by value** (rather than by pointer or reference). During this process, the derived class’s additional data members and overridden virtual functions are “sliced off,” leaving only the base class portion intact.

---

## 💻 Code Example

```cpp
class Base { 
public: 
    int a; 
};

class Derived : public Base { 
public: 
    int b; 
};

int main() {
    Derived d;
    Base b = d;  // Slicing occurs here: 'b' only has 'a', 'b' is lost
}
```

---

## 🛠️ Solution
To prevent object slicing and maintain runtime polymorphism, always use **pointers** or **references**:
```cpp
Base* bp = &d;  // OK: No slicing
// OR
Base& br = d;   // OK: No slicing
```

---

## 🎯 Summary to Impress
Slicing loses derived data and breaks runtime polymorphism. To avoid this, **never pass polymorphic objects by value**; always pass them by pointer or reference.
