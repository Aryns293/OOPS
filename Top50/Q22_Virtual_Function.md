# Q22 Virtual Function

## 🎯 Interview Answer
A **Virtual Function** is a member function declared with `virtual` in a base class that allows derived classes to override it. When the function is called through a base-class pointer or reference, the call is dynamically dispatched based on the actual object's type. This enables runtime polymorphism.

For example, if `Animal*` points to a `Dog` and `sound()` is virtual, calling `animal->sound()` invokes `Dog::sound()`.

A common implementation uses a vtable and a hidden vptr to perform this dynamic dispatch.

---

## ❓ Why Do We Need Virtual Functions?
Without `virtual`, the function called is determined by the **pointer type**, not the object type. With `virtual`, the function called is determined by the **actual object type** at runtime.

### 🚫 Example Without Virtual:
```cpp
class Base {
public:
    void show() { cout << "Base\n"; }
};

class Derived : public Base {
public:
    void show() { cout << "Derived\n"; }
};

int main() {
    Base* bp = new Derived();
    bp->show();   // Output: Base (wrong for polymorphic use!)
}
```

### ✅ With Virtual:
```cpp
class Base {
public:
    virtual void show() { cout << "Base\n"; }
};

class Derived : public Base {
public:
    void show() override { cout << "Derived\n"; }
};

int main() {
    Base* bp = new Derived();
    bp->show();   // Output: Derived (correct!)
}
```

---

## ⚙️ How Does It Work? (VTABLE and VPTR)
The C++ standard guarantees dynamic dispatch behavior for virtual functions. A **common implementation** of this uses a vtable and vptr:

### 1️⃣ VTABLE (Virtual Table)
- A compiler-generated table used by a class implementation to support virtual dispatch.
- Each entry corresponds to a virtual function and points to the implementation appropriate for that class.

### 2️⃣ VPTR (Virtual Pointer)
- Typically, each polymorphic object contains a hidden pointer (often called a vptr) that points to an appropriate virtual table for its class.

### 🔄 The Call Process
When a virtual function is called via a pointer/reference:
1. Fetch the object’s VPTR.
2. Go to the VTABLE.
3. Look up the correct function pointer for that function.
4. Call the function at runtime — this is **dynamic dispatch**.

---

## 📊 Diagram: VTABLE and VPTR (Conceptual)

```text
Base* bp = new Derived();

Object Derived:
+-------------------+
| VPTR ------------>|-----> Derived VTABLE
| ... data ...      |       +---------------------+
+-------------------+       | &Derived::show()    |
                            | &Base::other_func() | (if not overridden)
                            +---------------------+

bp->show();

Step 1: bp points to Derived object.
Step 2: Fetch VPTR from object.
Step 3: VPTR points to Derived VTABLE.
Step 4: Look up show() in VTABLE -> Derived::show().
```

---

## ⚖️ Virtual Function vs Pure Virtual Function

| Feature | Virtual function | Pure virtual function |
|---------|------------------|-----------------------|
| **Syntax** | `virtual void f() {}` | `virtual void f() = 0;` |
| **Base implementation** | Can have a base implementation | Declared with `= 0` |
| **Overriding** | Derived class *may* override | Concrete derived class generally *must* override |
| **Instantiation** | Base class can still be instantiated (if concrete) | Makes containing class abstract |

> **Note on Pure Virtual:** A class containing a pure virtual function is abstract and cannot be instantiated. A **concrete** derived class must provide an override for the pure virtual function.

---

## 💡 Key Points to Impress
- **Dynamic Dispatch:** `virtual` allows a derived class to override base behavior, resolving the call at runtime based on the actual object type.
- **Implementation:** Mechanisms like VTABLE and VPTR are common ways compilers implement this behavior.
- **Constructors/Destructors:** Virtual calls made from constructors or destructors do not dispatch to the more-derived class (they call the version for the subobject currently being constructed/destroyed).
- **Virtual Destructors:** If a class is intended to be used polymorphically and objects may be deleted through a base pointer, the base destructor should be virtual.
- **Performance:** Virtual dispatch can introduce a small runtime indirection compared with a statically resolved call. Modern compilers can sometimes devirtualize the call.
- Without `virtual`, you get **static binding** based on pointer type — usually wrong for polymorphic use.

---

## 🎯 Summary to Impress
- **What it is:** A base class function marked `virtual` that allows runtime polymorphism.
- **How it works:** Dynamic dispatch (commonly via vtable/vptr) routes the call to the actual object's implementation.
- **Why it matters:** Essential for extensible OOP design, treating derived objects uniformly through base abstractions.
