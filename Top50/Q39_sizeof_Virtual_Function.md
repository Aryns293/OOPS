# Q39 `sizeof` Virtual Function

## 🎯 Interview Answer
When a class has at least one virtual function, the compiler (typically) inserts a hidden **VPTR (Virtual Pointer)** into every object of that class to enable dynamic dispatch. This increases the total size of the object in memory.

### ⚙️ Key Points
- On a **64-bit system**, a pointer (VPTR) is typically **8 bytes**.
- A class without any virtual functions has no VPTR, so its size is simply the sum of its data members (plus any necessary alignment padding).

---

## 💻 Code Example

```cpp
class A { 
    int x; 
};            
// sizeof(A) = 4 bytes (size of int)

class B { 
    int x; 
    virtual void f() {} 
};  
// sizeof(B) = 16 bytes (int (4) + padding (4) + VPTR (8) on a 64-bit system)
```

---

## 🎯 Summary to Impress
Adding virtual functions to a class introduces a hidden **VPTR** to support runtime polymorphism, which increases the object's footprint in memory.
