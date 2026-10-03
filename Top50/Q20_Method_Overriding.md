# Q20 Method Overriding

**Interview Answer:**
Method Overriding is a feature in OOP where a derived class redefines a method of its base class with the exact same name, parameters, and return type. It is used to achieve runtime polymorphism. When a method is called through a base class pointer or reference, the derived class version is executed based on the actual object type at runtime.

Rules for Method Overriding in C++
Inheritance required – There must be a base class and a derived class. Overriding happens across classes, not within the same class.

Same signature – The method name, parameter list, and return type must be identical (or covariant return type in some cases). In C++11, use the override keyword to enforce this.

Virtual function in base – The base class method must be declared virtual. Without virtual, it’s just function hiding, not overriding.

Access modifier – The access level of the overridden method in the derived class can be different, but it’s usually kept same or less restrictive. (In C++, access is checked at compile time based on the static type.)

Cannot override non-virtual functions – Only virtual functions can be overridden.

Cannot override static functions – Static member functions cannot be virtual, so they cannot be overridden.

Cannot override constructors/destructors – Constructors cannot be virtual. Destructors can be virtual and should be overridden if needed.

Code Example
cpp
class Animal {
public:
    virtual void sound() {          // virtual function
        cout << "Animal makes a sound\n";
    }
    virtual ~Animal() {}            // virtual destructor (good practice)
};

class Dog : public Animal {
public:
    void sound() override {         // override keyword (C++11)
        cout << "Dog barks\n";
    }
};

class Cat : public Animal {
public:
    void sound() override {
        cout << "Cat meows\n";
    }
};

int main() {
    Animal* a1 = new Dog();
    Animal* a2 = new Cat();

    a1->sound();   // Output: Dog barks
    a2->sound();   // Output: Cat meows

    delete a1;
    delete a2;
    return 0;
}
Here, sound() is called through Animal* pointers, but the derived versions execute because of runtime polymorphism.

Diagram: Runtime Polymorphism via Overriding
text
        Animal (base)
        virtual sound()
           ^
           |
   +-------+-------+
   |               |
 Dog             Cat
 override sound()  override sound()

Animal* a = new Dog();
a->sound();  --> Dog::sound()  (resolved at runtime via VTABLE)
Overriding vs Overloading (Quick Note)
Feature	Overriding	Overloading
Scope	Base and derived classes	Same class
Binding	Runtime (dynamic)	Compile-time (static)
Signature	Must be identical	Must differ (parameters)
Virtual	Requires virtual in base	No virtual needed
Purpose	Runtime polymorphism	Readability/convenience
Key Points to Impress
Overriding = redefining a virtual base method in derived class with same signature.

Enables runtime polymorphism.

Base method must be virtual.

Use override keyword (C++11) to catch errors.

Cannot override non-virtual, static, or constructors.

Destructor can be virtual and should be overridden if needed.

Access modifier can change, but usually kept same.

Works via VTABLE and VPTR.

Summary to impress:

Method overriding lets derived classes provide specific behavior for a base class method.

Rules: same signature, base method virtual, inheritance required.

Achieves dynamic dispatch at runtime.

Use override for safety.

Essential for flexible, extensible OOP design.
