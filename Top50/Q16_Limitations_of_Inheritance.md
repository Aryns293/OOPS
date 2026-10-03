# Q16 Limitations of Inheritance

**Interview Answer:**
Inheritance is powerful, but it comes with several limitations that can make code rigid and hard to maintain. Interviewers often ask this to see if you understand when not to use inheritance.

Main Limitations of Inheritance
Tight Coupling
The child class is tightly coupled to the parent. Any change in the parent’s interface or behavior can break the child. This makes the hierarchy fragile.

Fragile Base Class Problem
A seemingly safe change in the base class can unknowingly break derived classes. For example, adding a new method to the base might conflict with a method in a derived class, or changing a method’s implementation can alter behavior in unexpected ways.

Complexity in Deep Hierarchies
Multiple levels of inheritance create a complex web. Understanding, debugging, and maintaining deep hierarchies becomes difficult. Method resolution can be confusing.

Inflexibility
The inheritance relationship is fixed at compile time. You cannot change the parent class at runtime. This limits flexibility compared to composition, where you can swap components dynamically.

Breaks Encapsulation
To allow derived classes to reuse code, the base class often exposes protected members. This weakens encapsulation because derived classes depend on the base class’s internal implementation details.

Diamond Problem (Multiple Inheritance)
In languages that support multiple inheritance (like C++), the diamond problem causes ambiguity and requires virtual inheritance, adding complexity.

Overuse Leads to Poor Design
Inheritance is often misused for code reuse when the relationship isn’t truly “is-a.” This leads to wrong abstractions and rigid designs.

Code Example: Fragile Base Class
cpp
class Base {
public:
    void foo() { cout << "Base::foo\n"; }
};

class Derived : public Base {
public:
    void foo(int x) { cout << "Derived::foo(int)\n"; }  // Hides Base::foo
};

int main() {
    Derived d;
    d.foo();      // ERROR: Base::foo is hidden by Derived::foo(int)
    d.Base::foo(); // OK
}
Adding foo(int) in Derived hides Base::foo(), which can surprise developers and break existing code.

How to Avoid These Limitations
Favor Composition over Inheritance when the relationship is not clearly “is-a.”

Keep inheritance hierarchies shallow.

Design base classes carefully — they should be stable.

Use interfaces (pure abstract classes) to define contracts without implementation.

Apply the Liskov Substitution Principle: derived classes must be usable in place of base classes without breaking behavior.

Key Points to Impress
Tight coupling and fragile base class are the biggest problems.

Deep hierarchies are hard to understand and maintain.

Inheritance is static; composition is dynamic and more flexible.

Overuse leads to wrong abstractions.

Prefer composition over inheritance – a core design principle.

Use inheritance only when there is a true, permanent is-a relationship.

Summary to impress:

Inheritance limitations: tight coupling, fragile base class, complexity, inflexibility, breaks encapsulation, diamond problem.

These issues make code brittle and hard to change.

Solution: use composition for “has-a” relationships, keep hierarchies shallow, and program to interfaces.

Always ask: “Is this truly an is-a relationship?” If not, use composition.
