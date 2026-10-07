# Q31 Virtual Function in Constructor

## 🎯 Interview Answer
Can you call a virtual function in a constructor? **Yes, but with a catch**: during construction and destruction, virtual dispatch does not work polymorphically as you might expect. The call resolves to the **current class’s version**, not the most derived class’s version.

### ❓ Why does this happen?
- **During base class construction**, the derived part of the object doesn’t exist yet. Calling a derived method would be dangerous.
- **During base class destruction**, the derived part of the object is already destroyed.
- Internally, as each base/derived layer is constructed or destroyed, the VPTR (Virtual Pointer) points to the VTABLE of the **current class being initialized or destroyed**, not the final derived class.

---

## 💻 Code Example

```cpp
class Base {
public:
    Base() { 
        show();                 // Calls Base::show()
    }          
    virtual void show() { 
        cout << "Base\n"; 
    }
};

class Derived : public Base {
public:
    Derived() { 
        show();                 // Calls Derived::show()
    }       
    void show() override { 
        cout << "Derived\n"; 
    }
};

int main() {
    Derived d;  
    // Output: 
    // Base
    // Derived
}
```

---

## 🎯 Summary to Impress
**Avoid calling virtual functions in constructors and destructors**. The behavior is not polymorphic, and it often leads to unexpected results or bugs because the object is in an incomplete state.
