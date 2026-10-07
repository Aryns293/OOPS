# Q29 Constructor Overloading

## 🎯 Interview Answer
**Constructor overloading** means having more than one constructor in the same class with different parameters (different number or types of parameters). The compiler chooses the appropriate constructor based on the arguments passed during object creation. It is a form of compile-time polymorphism.

---

## 💻 Code Example

```cpp
class Complex {
    double real, imag;
public:
    // Default constructor
    Complex() : real(0), imag(0) {}                     
    
    // Parameterized constructor (1 arg)
    Complex(double r) : real(r), imag(0) {}             
    
    // Parameterized constructor (2 args)
    Complex(double r, double i) : real(r), imag(i) {}   
};

int main() {
    Complex c1;           // Calls default constructor
    Complex c2(5);        // Calls 1-arg constructor
    Complex c3(5, 6);     // Calls 2-arg constructor
}
```

---

## 🎯 Summary to Impress
Constructor overloading allows objects of a class to be **initialized in multiple different ways** depending on the context and available data, enhancing flexibility and usability.
