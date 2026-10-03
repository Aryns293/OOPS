# Q38 final Keyword

**Interview Answer:**
final is used to prevent inheritance or overriding.

final class: Cannot be inherited.

final method: Cannot be overridden in derived classes.

Code:

cpp
class Base final {  // cannot be inherited
};

class Derived : public Base {  // ERROR
};

class A {
public:
    virtual void show() final {}  // cannot be overridden
};

class B : public A {
    void show() override {}  // ERROR
};
Summary: final enforces design constraints and can help with optimization.
