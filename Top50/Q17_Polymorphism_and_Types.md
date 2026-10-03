# Q17 Polymorphism and Types

**Interview Answer:**
Polymorphism means “many forms.” In OOP, it is the ability of a single interface to represent different underlying forms or behaviors. It allows the same function call to behave differently depending on the object it is invoked on. This makes code more flexible, extensible, and maintainable.

Types of Polymorphism
There are two main types:

Compile-Time Polymorphism (Static Polymorphism)
Resolved at compile time. Achieved via:

Function Overloading

Operator Overloading

Runtime Polymorphism (Dynamic Polymorphism)
Resolved at runtime. Achieved via:

Method Overriding using virtual functions in C++.

1. Compile-Time Polymorphism
The compiler decides which function to call based on the arguments or operator.

Function Overloading:

cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
};
Same function name add, different parameters. Compiler picks the right one.

Operator Overloading:

cpp
class Complex {
    double real, imag;
public:
    Complex(double r, double i) : real(r), imag(i) {}
    Complex operator+(const Complex& other) {
        return Complex(real + other.real, imag + other.imag);
    }
};
Redefines + for Complex objects.

2. Runtime Polymorphism
The actual function called is determined at runtime based on the object’s type. Requires inheritance and virtual functions.

Method Overriding:

cpp
class Shape {
public:
    virtual double area() { return 0; }
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14 * r * r; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double w, double h) : w(w), h(h) {}
    double area() override { return w * h; }
};

void printArea(Shape* s) {
    cout << s->area() << endl;   // Calls correct area() at runtime
}
printArea works with any Shape without knowing the exact type.

Diagram: Polymorphism Types
text
                Polymorphism
               /            \
   Compile-Time             Runtime
   (Static)                 (Dynamic)
      |                        |
Function Overloading      Method Overriding
Operator Overloading      (using virtual functions)
Key Differences Table
Feature	Compile-Time Polymorphism	Runtime Polymorphism
Binding	Early binding (compile time)	Late binding (runtime)
Achieved by	Function/Operator overloading	Method overriding with virtual functions
Inheritance	Not required	Required
Performance	Faster (resolved at compile time)	Slightly slower (vtable lookup)
Flexibility	Less flexible	More flexible, extensible
Key Points to Impress
Polymorphism = “many forms” – one interface, multiple behaviors.

Compile-time: function overloading, operator overloading.

Runtime: method overriding using virtual functions.

Runtime polymorphism uses VTABLE and VPTR for dynamic dispatch.

It enables extensibility: new shapes can be added without changing printArea.

Rule: Use virtual in base class, override in derived (C++11) for safety.

Summary to impress:

Polymorphism allows the same call to behave differently.

Two types: compile-time (overloading) and runtime (overriding).

Compile-time is faster; runtime is more flexible.

Runtime polymorphism is achieved via virtual functions and inheritance.

It’s the backbone of extensible OOP design.
