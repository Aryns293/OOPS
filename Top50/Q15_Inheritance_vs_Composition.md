# Q15 Inheritance vs Composition

**Interview Answer:**
Inheritance and Composition are two ways to reuse code and establish relationships between classes. The key difference is the type of relationship they represent.

Inheritance is an “is-a” relationship. For example, a Car is-a Vehicle. The child class inherits the interface and implementation of the parent class. It creates tight coupling between the parent and child.

Composition is a “has-a” relationship. For example, a Car has-an Engine. The containing class holds an object of another class as a member. It provides code reuse without the tight coupling of inheritance. It is more flexible and avoids the fragile base class problem.

Code Example
Inheritance (is-a):

cpp
class Vehicle {
public:
    void fuel() { cout << "Refueling\n"; }
};

class Car : public Vehicle {   // Car IS-A Vehicle
public:
    void drive() { cout << "Driving\n"; }
};
Composition (has-a):

cpp
class Engine {
public:
    void start() { cout << "Engine started\n"; }
};

class Car {
private:
    Engine engine;   // Car HAS-AN Engine
public:
    void drive() {
        engine.start();
        cout << "Driving\n";
    }
};
Diagram: Inheritance vs Composition
text
Inheritance (is-a):
   Vehicle
      ^
      |
    Car

Composition (has-a):
   Car  --->  Engine
   (Car contains an Engine object)
Key Differences Table
Feature	Inheritance	Composition
Relationship	is-a	has-a
Coupling	Tight coupling	Loose coupling
Flexibility	Less flexible; relationship fixed at compile time	More flexible; can change at runtime
Reuse	Reuses interface and implementation	Reuses implementation via delegation
Fragile Base Class	Yes — changes in base can break child	No — changes in part don’t break the whole
Encapsulation	Breaks encapsulation (child depends on parent’s internals)	Preserves encapsulation (part is hidden)
When to use	When there is a true subtype relationship	When you just need to use functionality of another class
Why Prefer Composition Over Inheritance?
Loose coupling: The containing class only depends on the public interface of the part, not its internal details.

Flexibility: You can change the part at runtime (e.g., swap different engines) if you use pointers or references.

Avoids fragile base class problem: Changes to the parent class don’t force changes in the child.

Better encapsulation: The internal details of the part are hidden.

Easier to test: You can mock the part easily.

Rule of thumb: Use inheritance for “is-a” and composition for “has-a”. When in doubt, prefer composition.

Key Points to Impress
Inheritance = is-a, tight coupling, reuses interface and implementation.

Composition = has-a, loose coupling, reuses implementation via delegation.

Composition is more flexible and avoids the fragile base class problem.

Favor composition over inheritance (a key design principle from the Gang of Four).

Use inheritance only when the subtype relationship is stable and truly “is-a”.

Summary to impress:

Inheritance: “is-a”, tight coupling, fragile base class.

Composition: “has-a”, loose coupling, flexible, safer.

Prefer composition over inheritance for better maintainability and flexibility.

Use inheritance only when there is a clear, permanent subtype relationship.
