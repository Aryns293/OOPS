# Q37 explicit Keyword

**Interview Answer:**
The explicit keyword is used on constructors to prevent implicit type conversions. Without explicit, a single-argument constructor can act as a conversion operator.

Code:

cpp
class Complex {
    double real;
public:
    explicit Complex(double r) : real(r) {}
};

void func(Complex c) {}

int main() {
    // func(3.0);  // ERROR: no implicit conversion
    func(Complex(3.0));  // OK: explicit
}
Summary: explicit avoids unintended implicit conversions; good practice for single-argument constructors.
