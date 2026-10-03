# Q11 Virtual Constructor Destructor

**Interview Answer:**
Can a Constructor be virtual?
No. A constructor cannot be virtual in C++.

Why?
The virtual mechanism relies on a VTABLE (Virtual Table) and VPTR (Virtual Pointer). The VPTR is initialized inside the constructor after the object’s memory is allocated. At the time the constructor runs, the object is still being constructed, and the VPTR does not yet point to the correct VTABLE. The object’s dynamic type is not fully determined until the constructor completes. So virtual dispatch cannot work during construction.

Also, a virtual call needs an existing object to look up the VTABLE. But a constructor is called to create the object — there is no complete object yet. So it’s logically impossible.

Can a Destructor be virtual?
Yes. A destructor can and should be virtual if the class is intended to be used as a base class and objects will be deleted via a base class pointer.

Why?
When you delete a derived object through a base pointer, a virtual destructor ensures the derived class destructor is called first, then the base class destructor. Without it, only the base destructor runs → memory leak and undefined behavior.

Code Example
cpp
class Base {
public:
    Base() { cout << "Base Constructor\n"; }
    virtual ~Base() { cout << "Base Destructor\n"; }  // Virtual destructor
};

class Derived : public Base {
public:
    Derived() { cout << "Derived Constructor\n"; }
    ~Derived() { cout << "Derived Destructor\n"; }
};

int main() {
    Base* bp = new Derived();
    delete bp;   // Calls Derived destructor, then Base destructor
    return 0;
}
Output:

text
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor
If ~Base() were not virtual, output would be:

text
Base Constructor
Derived Constructor
Base Destructor   // Derived destructor skipped! Memory leak.
Diagram: Why Constructor Cannot Be Virtual
text
Object creation:
1. Memory allocated for object.
2. VPTR is set up inside constructor.
3. Constructor body runs.

At step 2, VPTR is being initialized — no VTABLE lookup possible yet.
So virtual dispatch during construction is impossible.
Diagram: Virtual Destructor Working
text
Base* bp = new Derived();

bp -> [ VPTR ] ---> Derived VTABLE
                     - Derived::~Derived()
                     - Base::~Base()

delete bp;  // Uses VPTR to find Derived::~Derived()
Key Points to Impress
Constructor cannot be virtual — VTABLE/VPTR not ready during construction.

Destructor can be virtual — and should be, for polymorphic base classes.

Virtual destructor ensures correct cleanup order: derived → base.

If a class has any virtual function, it should have a virtual destructor.

A pure virtual destructor is allowed: virtual ~Base() = 0; but must be defined outside the class.

Summary to impress:

Constructor: No — object type not fully determined, VTABLE not ready.

Destructor: Yes — needed to avoid memory leaks when deleting via base pointer.

Rule: Base class with virtual functions → virtual destructor.

Virtual destructor is a cornerstone of safe polymorphic deletion.
