# TOPIC 11: Explicit Keyword (C++)

Marks constructors so they do NOT implicitly convert types. Optional for constructors taking exactly one argument (only single-argument constructors are usable for typecasting).

## Without `explicit`:

```cpp
class Complex {
   double real, imag;
public:
   Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}
   bool operator == (Complex rhs) { return (real == rhs.real && imag == rhs.imag); }
};
int main() {
   Complex com1(3.0, 0.0);
   if (com1 == 3.0) cout << "Same";  // 3.0 implicitly converted to Complex
}
// Output: Same
```

This is a conversion constructor — the compiler implicitly converts `3.0` to `Complex`. As discussed in this article, in C++, if a class has a constructor which can be called with a single argument, then this constructor becomes a conversion constructor because such a constructor allows conversion of the single argument to the class being constructed. In this case, when `com1 == 3.0` is called, 3.0 is implicitly converted to Complex type because the default constructor can be called with only 1 argument because both parameters are default arguments and we can choose not to provide them. We can avoid such implicit conversions as these may lead to unexpected results.

## With `explicit`:

```cpp
explicit Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}
```

Now `com1 == 3.0` → compile error: no match for `operator==` in `com1 == 3.0e+0`.

Still possible via explicit cast: `if (com1 == (Complex)3.0)` → works fine.

```cpp
// C++ program to illustrate default constructor with 'explicit' keyword
#include <iostream>
using namespace std;

class Complex {
private:
    double real;
    double imag;
public:
    // Default constructor
    explicit Complex(double r = 0.0, double i = 0.0):
        real(r), imag(i)
    {
    }
    // A method to compare two Complex numbers
    bool operator == (Complex rhs)
    {
        return (real == rhs.real &&
                imag == rhs.imag);
    }
};

// Driver Code
int main()
{
    // a Complex object
    Complex com1(3.0, 0.0);

    if (com1 == (Complex)3.0)
        cout << "Same";
    else
        cout << "Not Same";
    return 0;
}
// Output: Same
```

**Note:** `explicit` can be used with a constant expression — the function is explicit only if that expression evaluates true.
