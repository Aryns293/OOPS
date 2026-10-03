# Q33 Object Slicing

**Interview Answer:**
Object slicing occurs when a derived class object is assigned to a base class object by value (not by pointer/reference). The derived class’s additional data members and overridden virtual functions are “sliced off,” leaving only the base class portion.

Code:

cpp
class Base { public: int a; };
class Derived : public Base { public: int b; };

int main() {
    Derived d;
    Base b = d;  // slicing: b only has 'a', 'b' is lost
}
Solution: Use pointers or references: Base* bp = &d; or Base& br = d;

Summary: Slicing loses derived data and polymorphism; avoid passing by value in polymorphic hierarchies.
