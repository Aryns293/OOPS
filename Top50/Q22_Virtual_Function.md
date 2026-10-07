# Q22 Virtual Function

## 🎯 Interview Answer
A **Virtual Function** is a member function declared in a base class using the `virtual` keyword and overridden by a derived class. When called through a base class pointer or reference to a derived object, the derived class version is executed — resolved at runtime. This is the foundation of runtime polymorphism in C++.

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
    bp->show();   // Output: Base (wrong!)
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
The magic happens through two hidden mechanisms inserted by the compiler:

### 1️⃣ VTABLE (Virtual Table)
- A static array of function pointers, **one per class** that contains virtual functions.
- Each entry points to the most-derived version of a virtual function for that class.

### 2️⃣ VPTR (Virtual Pointer)
- A hidden data member inserted into **every object** of a class that has virtual functions.
- It points to the VTABLE of the object’s class.
- It is initialized in the constructor.

### 🔄 The Call Process
When a virtual function is called via a pointer/reference:
1. The compiler fetches the object’s VPTR.
2. Goes to the VTABLE.
3. Looks up the correct function pointer for that function.
4. Calls the function at runtime — this is **late binding** or **dynamic dispatch**.

---

## 📊 Diagram: VTABLE and VPTR

```text
Base* bp = new Derived();

Object Derived:
+-------------------+
| VPTR ------------>|-----> Derived VTABLE
| ... data ...      |       +---------------------+
+-------------------+       | &Derived::show()    |
                            | &Base::show()       | (if any other virtual)
                            +---------------------+

bp->show();

Step 1: bp points to Derived object.
Step 2: Fetch VPTR from object.
Step 3: VPTR points to Derived VTABLE.
Step 4: Look up show() in VTABLE -> Derived::show().
Step 5: Call it.
```

---

## 💻 Code Example with Multiple Virtual Functions

```cpp
class Animal {
public:
    virtual void sound() { cout << "Animal sound\n"; }
    virtual void move() { cout << "Animal moves\n"; }
    virtual ~Animal() {}   // virtual destructor
};

class Dog : public Animal {
public:
    void sound() override { cout << "Dog barks\n"; }
    void move() override { cout << "Dog runs\n"; }
};

int main() {
    Animal* a = new Dog();
    a->sound();   // Dog barks
    a->move();    // Dog runs
    delete a;     // Correct destructor order
    return 0;
}
```

### VTABLE for Dog:
```text
Dog VTABLE:
+---------------------+
| &Dog::sound()       |
| &Dog::move()        |
| &Dog::~Dog()        |
+---------------------+
```

---

## 💡 Key Points to Impress
- **Virtual function** = member function declared `virtual` in base, overridden in derived.
- Enables **runtime polymorphism** (dynamic dispatch).
- Works via **VTABLE** (per class) and **VPTR** (per object).
- VPTR is initialized in the constructor; so virtual calls in a constructor call the base version only.
- Use `override` keyword (C++11) for safety.
- Always give polymorphic base classes a **virtual destructor**.
- Virtual functions have a small performance overhead (vtable lookup) but enable great flexibility.
- **Pure virtual function** (`= 0`) makes the class abstract and forces derived classes to implement it.

---

## 🎯 Summary to Impress
- Virtual function allows a derived class to override base behavior.
- Call resolved at **runtime** based on actual object type.
- **Mechanism:** VTABLE (array of function pointers) + VPTR (hidden pointer in object).
- `virtual` keyword triggers this mechanism.
- Essential for runtime polymorphism, extensible design, and safe deletion.
- Without `virtual`, you get **static binding** based on pointer type — usually wrong for polymorphic use.
