# Q24 Access Modifiers

**Interview Answer:**
Access modifiers control the visibility of class members.

Private: Accessible only within the same class. Not accessible in derived classes or outside.

Protected: Accessible within the same class and by derived classes. Not accessible outside the hierarchy.

Public: Accessible from anywhere.

Default in C++:

class → members are private by default.

struct → members are public by default.

Table:

Modifier	Same Class	Derived Class	Outside
private	Yes	No	No
protected	Yes	Yes	No
public	Yes	Yes	Yes
Code:

cpp
class Base {
private:   int a;  // only Base
protected: int b;  // Base + Derived
public:    int c;  // everyone
};

class Derived : public Base {
    void func() {
        // a = 10; // ERROR: private
        b = 20;    // OK: protected
        c = 30;    // OK: public
    }
};
Summary: Use private for data, protected for inheritance, public for interface.
