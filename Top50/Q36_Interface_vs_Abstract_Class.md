# Q36 Interface vs Abstract Class

**Interview Answer:**
In C++, there is no separate interface keyword. An interface is typically an abstract class with only pure virtual functions and no data members.

Feature	Abstract Class	Interface (C++ style)
Methods	Pure virtual + concrete	Only pure virtual
Data members	Can have	Should not have
Constructors	Can have	Usually not needed
Multiple inheritance	Can inherit from one class	Can inherit from multiple interfaces
Use case	“is-a” with shared code	“can-do” contract
Code:

cpp
// Interface
class Drawable {
public:
    virtual void draw() = 0;
    virtual ~Drawable() {}
};

// Abstract class
class Shape {
protected:
    int x, y;
public:
    Shape(int x, int y) : x(x), y(y) {}
    virtual double area() = 0;
};
Summary: Interface = pure contract; abstract class = partial implementation + contract.
