# Q29 Constructor Overloading

**Interview Answer:**
Constructor overloading means having more than one constructor in the same class with different parameters (different number or types). The compiler chooses the appropriate constructor based on the arguments passed during object creation.

Code:

cpp
class Complex {
    double real, imag;
public:
    Complex() : real(0), imag(0) {}                     // default
    Complex(double r) : real(r), imag(0) {}             // 1 arg
    Complex(double r, double i) : real(r), imag(i) {}   // 2 args
};

int main() {
    Complex c1;           // default
    Complex c2(5);        // 1 arg
    Complex c3(5, 6);     // 2 args
}
Summary: Constructor overloading allows objects to be initialized in different ways.
