# Q40 Output of Virtual Dispatch

## 🎯 Interview Answer

### 💻 Given Code:
```cpp
class Base {
public:
    virtual void show() { cout << "In Base\n"; }
};

class Derived : public Base {
public:
    void show() override { cout << "In Derived\n"; }
};

int main() {
    Base *bp = new Derived;
    bp->show();
    bp->Base::show();
    return 0;
}
```

### 🖨️ Output:
```text
In Derived
In Base
```

### 🧠 Explanation:
1. `bp->show()` uses **virtual dispatch** → It calls `Derived::show()` because the actual object being pointed to is of type `Derived`.
2. `bp->Base::show()` uses the **scope resolution operator (`::`)** → It explicitly calls `Base::show()`, completely bypassing the virtual dispatch mechanism.

---

## 🎯 Summary to Impress
A standard virtual call uses the **actual object type** (dynamic dispatch). However, using the scope resolution operator forces the compiler to call the **statically specified base version**, bypassing polymorphism.
