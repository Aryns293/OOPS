# Q10 Virtual Destructor

**Interview Answer:**
We need a virtual destructor to ensure that when we delete a derived class object through a base class pointer, the derived class destructor is called first, followed by the base class destructor. Without it, only the base class destructor runs, leading to memory leaks and undefined behavior.

The Problem (Without Virtual Destructor)
cpp
class Base {
public:
    Base() { cout << "Base Constructor\n"; }
    ~Base() { cout << "Base Destructor\n"; }  // Not virtual
};

class Derived : public Base {
    int* data;
public:
    Derived() {
        data = new int[100];
        cout << "Derived Constructor\n";
    }
    ~Derived() {
        delete[] data;
        cout << "Derived Destructor\n";
    }
};

int main() {
    Base* bp = new Derived();
    delete bp;   // Only Base destructor called! Derived destructor skipped.
    return 0;
}
Output:

text
Base Constructor
Derived Constructor
Base Destructor
Problem: Derived::~Derived() is never called → data is never freed → memory leak. This is undefined behavior according to the C++ standard.

The Solution (Virtual Destructor)
cpp
class Base {
public:
    Base() { cout << "Base Constructor\n"; }
    virtual ~Base() { cout << "Base Destructor\n"; }  // Virtual destructor
};

class Derived : public Base {
    int* data;
public:
    Derived() {
        data = new int[100];
        cout << "Derived Constructor\n";
    }
    ~Derived() {
        delete[] data;
        cout << "Derived Destructor\n";
    }
};

int main() {
    Base* bp = new Derived();
    delete bp;   // Both destructors called in correct order
    return 0;
}
Output:

text
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor
Now the derived destructor runs first, freeing data, then the base destructor runs.

How It Works (VTABLE and VPTR)
When a class has a virtual function (including a virtual destructor), the compiler creates a VTABLE (Virtual Table) for that class.

Each object gets a hidden VPTR (Virtual Pointer) pointing to its class’s VTABLE.

When delete bp is called, the compiler uses the VPTR to look up the correct destructor in the VTABLE at runtime.

This ensures the most derived destructor is called first, then base destructors up the hierarchy.

Diagram:

text
Base* bp = new Derived();

bp -> [ VPTR ] ---> Derived VTABLE
                     - Derived::~Derived()
                     - Base::~Base()

delete bp;  // Uses VPTR to find Derived::~Derived()
When to Make Destructor Virtual?
If a class is intended to be used as a base class and objects will be deleted via base pointer.

If the class has any virtual function, it should have a virtual destructor (to avoid undefined behavior).

If the class is not meant to be deleted polymorphically, you can skip it (but it’s safer to make it virtual if there’s any doubt).

Key Points to Impress
Without virtual destructor: derived destructor not called → memory leak.

With virtual destructor: derived destructor called first, then base → correct cleanup.

Works via VTABLE and VPTR → runtime resolution.

Rule: If a class has virtual functions, give it a virtual destructor.

A pure virtual destructor is also possible (virtual ~Base() = 0;) and must be defined outside the class.

Summary to impress:

Virtual destructor ensures proper cleanup when deleting derived objects via base pointers.

Prevents memory leaks and undefined behavior.

Essential for any polymorphic base class.

Always remember: Base pointer + derived object + delete → virtual destructor needed.
