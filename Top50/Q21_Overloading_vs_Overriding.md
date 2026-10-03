# Q21 Overloading vs Overriding

**Interview Answer:**
Overloading and Overriding are both forms of polymorphism in C++, but they are completely different concepts. The key difference is when the method is resolved and where it occurs.

Overloading happens within the same class (or same scope). Multiple functions have the same name but different parameters. The compiler decides which one to call at compile time based on the arguments. This is compile-time (static) polymorphism.

Overriding happens between a base class and a derived class. The derived class redefines a virtual method of the base class with the exact same signature. The actual method called is decided at runtime based on the object’s type. This is runtime (dynamic) polymorphism.

Code Example: Overloading
cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
};
All three functions are named add but have different parameters. The compiler picks the right one based on the arguments.

Code Example: Overriding
cpp
class Animal {
public:
    virtual void sound() { cout << "Animal sound\n"; }
};

class Dog : public Animal {
public:
    void sound() override { cout << "Dog barks\n"; }
};

int main() {
    Animal* a = new Dog();
    a->sound();   // Output: Dog barks (resolved at runtime)
}
Dog overrides Animal::sound(). The call through Animal* executes Dog::sound() at runtime.

Key Differences Table
Feature	Overloading	Overriding
Binding	Compile-time (static)	Runtime (dynamic)
Scope	Same class or same scope	Base class and derived class
Signature	Must differ (parameters)	Must be identical
Inheritance	Not required	Required
Virtual keyword	Not needed	Base method must be virtual
Return type	Can differ	Must be same (or covariant)
Purpose	Convenience, readability	Runtime polymorphism
Resolution	By compiler based on arguments	By VTABLE/VPTR at runtime
Access modifier	Can be anything	Cannot be more restrictive (in Java); in C++ access is checked at compile time
Example	add(int, int) vs add(double, double)	Animal::sound() vs Dog::sound()
Diagram: Overloading vs Overriding
text
Overloading (Compile-time)
Same class:
  add(int, int)
  add(double, double)
  add(int, int, int)
Compiler picks based on arguments.

Overriding (Runtime)
Base class:  virtual sound()
Derived class: sound() override
Animal* a = new Dog();
a->sound();  -> Dog::sound()  (via VTABLE)
Key Points to Impress
Overloading = same name, different parameters, same class, compile-time.

Overriding = same name, same parameters, base + derived, runtime, requires virtual.

Overloading is about convenience; overriding is about polymorphism.

Overriding needs inheritance; overloading does not.

Use override keyword in C++11 to catch mistakes.

Overloading is resolved by the compiler; overriding is resolved by the VTABLE at runtime.

Summary to impress:

Overloading: same name, different signature, compile-time, same class.

Overriding: same name, same signature, runtime, base-derived, virtual.

Overloading = static polymorphism; overriding = dynamic polymorphism.

Know the difference — it’s a classic interview question.
