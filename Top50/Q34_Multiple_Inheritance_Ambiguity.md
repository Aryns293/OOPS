# Q34 Multiple Inheritance Ambiguity

**Interview Answer:**
When a class inherits from two base classes that both have a member with the same name, accessing that member is ambiguous. The compiler doesn’t know which one to use.

Code:

cpp
class A { public: void show() { cout << "A\n"; } };
class B { public: void show() { cout << "B\n"; } };
class C : public A, public B { };

int main() {
    C obj;
    // obj.show();  // ERROR: ambiguous
    obj.A::show();   // OK: A::show
    obj.B::show();   // OK: B::show
}
Solution: Use scope resolution operator :: to specify which base class’s member to use.

Summary: Multiple inheritance can cause ambiguity; resolve with :: or virtual inheritance for diamond problem.
