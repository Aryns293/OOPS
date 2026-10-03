# Q31 Virtual Function in Constructor

**Interview Answer:**
Yes, but with a catch: during construction and destruction, virtual dispatch does not work as expected. The call resolves to the current class’s version, not the derived class’s.

Why?

During base class construction, the derived part doesn’t exist yet.

During base class destruction, the derived part is already destroyed.

The VPTR points to the current class’s VTABLE.

Code:

cpp
class Base {
public:
    Base() { show(); }          // calls Base::show()
    virtual void show() { cout << "Base\n"; }
};

class Derived : public Base {
public:
    Derived() { show(); }       // calls Derived::show()
    void show() override { cout << "Derived\n"; }
};

int main() {
    Derived d;  // Output: Base, then Derived
}
Summary: Avoid calling virtual functions in constructors/destructors; behavior is not polymorphic.
