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

This is a conversion constructor — the compiler implicitly converts `3.0` to `Complex`.

## With `explicit`:

```cpp
explicit Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}
```

Now `com1 == 3.0` → compile error: no match for `operator==` in `com1 == 3.0e+0`.

Still possible via explicit cast: `if (com1 == (Complex)3.0)` → works fine.

**Note:** `explicit` can be used with a constant expression — the function is explicit only if that expression evaluates true.
