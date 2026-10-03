# Q12 Inheritance and Types

**Interview Answer:**
Inheritance is a mechanism in OOP where one class (called the child/derived/subclass) acquires the properties (data members) and behaviors (member functions) of another class (called the parent/base/superclass). It represents an “is-a” relationship — for example, a Car is-a Vehicle. It promotes code reusability and is the foundation for runtime polymorphism.

Types of Inheritance (with simple diagrams)
1. Single Inheritance
One base class → one derived class.

text
   A
   |
   B
cpp
class A { };
class B : public A { };
2. Multilevel Inheritance
A derived class becomes a base class for another class.

text
   A
   |
   B
   |
   C
cpp
class A { };
class B : public A { };
class C : public B { };
3. Hierarchical Inheritance
One base class → multiple derived classes.

text
     A
   / | \
  B  C  D
cpp
class A { };
class B : public A { };
class C : public A { };
class D : public A { };
4. Multiple Inheritance
One derived class inherits from more than one base class.

text
  A   B
   \ /
    C
cpp
class A { };
class B { };
class C : public A, public B { };
Note: Supported in C++. Not supported via classes in Java (to avoid diamond problem).

5. Hybrid (Virtual) Inheritance
Combination of multiple and hierarchical inheritance. Often uses virtual base classes to solve the diamond problem.

text
     A
   /   \
  B     C
   \   /
     D
cpp
class A { };
class B : virtual public A { };
class C : virtual public A { };
class D : public B, public C { };
Code Example (Single Inheritance)
cpp
class Vehicle {
public:
    void fuel() {
        cout << "Refueling\n";
    }
};

class Car : public Vehicle {
public:
    void drive() {
        cout << "Driving\n";
    }
};

int main() {
    Car c;
    c.fuel();   // Inherited from Vehicle
    c.drive();  // Own method
    return 0;
}
Output:

text
Refueling
Driving
Key Points to Impress
Inheritance = “is-a” relationship.

Promotes code reusability and extensibility.

Types: Single, Multilevel, Hierarchical, Multiple, Hybrid.

C++ supports all types; Java does not support multiple inheritance via classes (but supports it via interfaces).

Multiple inheritance can cause ambiguity (e.g., same method in both base classes) — solved using scope resolution or virtual base classes.

Access specifiers (public, protected, private) control how base members are inherited.

Inheritance creates tight coupling — prefer composition when the relationship is “has-a” instead of “is-a”.

Summary to impress:

Inheritance lets a child class reuse and extend a parent class.

Types: Single, Multilevel, Hierarchical, Multiple, Hybrid.

C++ supports multiple inheritance; Java doesn’t (via classes).

Used for code reuse and runtime polymorphism.

Always consider composition over inheritance for flexibility.
