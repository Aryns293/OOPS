# Q35 Pure Virtual Function

**Interview Answer:**
A pure virtual function is a virtual function declared with = 0. It has no implementation in the base class. A class with at least one pure virtual function is an abstract class. It cannot be instantiated — only inherited.

Code:

cpp
class Shape {
public:
    virtual double area() = 0;  // pure virtual
    virtual ~Shape() {}
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14 * r * r; }
};

int main() {
    // Shape s;  // ERROR: abstract
    Shape* s = new Circle(5);  // OK
}
Summary: Pure virtual functions define a contract; derived classes must implement them or become abstract.
