# Q14 Modes of Inheritance

**Interview Answer:**
In C++, inheritance modes determine how the members of the base class are accessed in the derived class. There are three modes: public, protected, and private.

1. Public Inheritance
Public members of base → remain public in derived.

Protected members of base → remain protected in derived.

Private members of base → never accessible directly in derived (but can be accessed via public/protected base methods).

Represents an “is-a” relationship.
This is the most common and intuitive form.

cpp
class Base {
public:    int a;
protected: int b;
private:   int c;
};

class Derived : public Base {
    // a is public
    // b is protected
    // c is NOT accessible
};
2. Protected Inheritance
Public and protected members of base → become protected in derived.

Private members → still not accessible.

Used when you want to restrict access to derived classes only.

cpp
class Derived : protected Base {
    // a is protected
    // b is protected
    // c is NOT accessible
};
3. Private Inheritance
Public and protected members of base → become private in derived.

Private members → still not accessible.

Represents a “implemented-in-terms-of” relationship. The derived class uses the base class internally but does not expose its interface. Composition is usually preferred over private inheritance.

cpp
class Derived : private Base {
    // a is private
    // b is private
    // c is NOT accessible
};
Summary Table: Base Member Access in Derived Class
Base Member →	public inheritance	protected inheritance	private inheritance
public	public	protected	private
protected	protected	protected	private
private	Not accessible	Not accessible	Not accessible
Default Inheritance Mode
For a class, default inheritance is private.

For a struct, default inheritance is public.

cpp
class Derived : Base { };        // private inheritance
struct Derived : Base { };       // public inheritance
Code Example
cpp
class Vehicle {
public:
    void fuel() { cout << "Fueling\n"; }
protected:
    int speed;
private:
    int vin;
};

// Public inheritance
class Car : public Vehicle {
public:
    void setSpeed(int s) { speed = s; }  // protected accessible
    // vin is not accessible
};

int main() {
    Car c;
    c.fuel();        // public -> public
    // c.speed = 10; // ERROR: speed is protected in Car
    return 0;
}
Key Points to Impress
Public inheritance = “is-a” → most common, interface inheritance.

Protected inheritance = rarely used; base interface becomes protected in derived.

Private inheritance = “implemented-in-terms-of”; prefer composition instead.

Private members of base are never directly accessible in derived, regardless of mode.

Default mode: class → private, struct → public.

Access specifiers control encapsulation and visibility across the inheritance hierarchy.

Summary to impress:

Three modes: public, protected, private.

They change the access level of base members in the derived class.

Public: public→public, protected→protected.

Protected: public/protected→protected.

Private: public/protected→private.

Private members of base always remain inaccessible.

Default: class is private, struct is public.

Use public for “is-a”; use composition instead of private inheritance for “has-a”.
