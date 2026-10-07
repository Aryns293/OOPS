# Q17 Polymorphism and Types

## 🎯 Interview-Ready Answer
Polymorphism means "many forms." It allows the same interface or operation to exhibit different implementations or behaviors depending on the context.

In C++, there are two commonly discussed types:

1. **Compile-time polymorphism:** The function to execute is determined by the compiler. It is commonly achieved through function overloading, operator overloading, and templates.
2. **Runtime polymorphism:** The function to execute is determined at runtime based on the actual object. It is achieved using inheritance and virtual functions.

For example, if `Circle` and `Rectangle` both inherit from `Shape` and override a virtual `area()` function, I can write:

```cpp
Shape* s = new Circle();
s->area();
```

Even though the pointer type is `Shape*`, `Circle::area()` is called because `area()` is virtual. This is called **dynamic dispatch** (requires the combination of: inheritance + virtual function + base pointer/reference).

Compile-time polymorphism is also called **static** or **early binding**, while runtime polymorphism is called **dynamic** or **late binding**.

Internally, C++ implementations *typically* use mechanisms such as a **vtable** and **vptr** to implement virtual dispatch.

---

## ❓ Why is Polymorphism Useful? (Follow-up Question)
It reduces coupling and makes code extensible. For example, a `printArea(Shape* s)` function can work with any future `Shape` without modifying its implementation. We can add a `Triangle` or `Square` simply by implementing the required virtual function. 

Polymorphism isn't just about "same function, different behavior"; its real design value is allowing code to depend on an abstraction rather than concrete classes.

---

## 🌟 Detailed Breakdown

### 1️⃣ Compile-Time Polymorphism (Static Polymorphism)
The compiler decides which function to call based on the arguments or operator.

#### Function Overloading:
```cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
};
```
> **Note:** Same function name `add`, different parameters. Compiler picks the right one.

#### Operator Overloading:
```cpp
class Complex {
    double real, imag;
public:
    Complex(double r, double i) : real(r), imag(i) {}
    Complex operator+(const Complex& other) {
        return Complex(real + other.real, imag + other.imag);
    }
};
```
> **Note:** Redefines `+` for `Complex` objects.

*(Templates are also a major form of compile-time polymorphism in C++)*

### 2️⃣ Runtime Polymorphism (Dynamic Polymorphism)
The actual function called is determined at runtime based on the object’s type.

#### Method Overriding:
```cpp
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
    cout << s->area() << endl;
}
```
> **Note:** `printArea` doesn't need to know whether it received a `Circle` or a `Rectangle`. It only knows that it has a `Shape*`. Because `area()` is virtual, C++ performs dynamic dispatch and calls the appropriate derived implementation.

---

## 📊 Diagram: Polymorphism Types

```text
                Polymorphism
               /            \
   Compile-Time             Runtime
   (Static)                 (Dynamic)
      |                        |
Function Overloading      Method Overriding
Operator Overloading      (using virtual functions)
Templates
```

---

## ⚖️ Key Differences Table

| Feature | Compile-Time Polymorphism | Runtime Polymorphism |
|---------|---------------------------|----------------------|
| **Binding** | Early binding (compile time) | Late binding (runtime) |
| **Achieved by** | Function/Operator overloading, Templates | Method overriding with virtual functions |
| **Inheritance** | Not required | Required |
| **Performance** | Generally no runtime dispatch overhead | Small runtime indirection (Note: modern compilers can sometimes devirtualize calls) |
| **Flexibility** | Less flexible at runtime | Highly flexible, extensible at runtime |
