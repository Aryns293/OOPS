# Q04 Class vs Struct

**Interview Answer:**
In C++, struct and class are almost identical. The only technical differences are:

Default access specifier:

For class, members are private by default.

For struct, members are public by default.

Default inheritance mode:

When inheriting, class uses private inheritance by default.

struct uses public inheritance by default.

Other than that, struct can do everything a class can — it can have methods, constructors, destructors, inheritance, virtual functions, access specifiers, etc. This is different from C, where struct only holds data.

Key Differences Table
Feature	class	struct
Default member access	private	public
Default inheritance	private	public
Can have methods?	Yes	Yes
Can have constructors/destructors?	Yes	Yes
Can inherit?	Yes	Yes
Can have virtual functions?	Yes	Yes
Typical usage	Objects with behavior and encapsulation	Simple data grouping (POD)
Code Example (C++)
cpp
// Using struct
struct Point {
    int x, y;  // public by default
    Point(int x, int y) : x(x), y(y) {}
    void display() { cout << x << ", " << y; }
};

// Using class
class PointClass {
    int x, y;  // private by default
public:
    PointClass(int x, int y) : x(x), y(y) {}
    void display() { cout << x << ", " << y; }
};
Both work. The only difference is that in struct, x and y are public; in class, they are private and need public:.

Inheritance example:

cpp
struct Base { int a; };
struct Derived : Base { };   // public inheritance by default

class BaseClass { int a; };
class DerivedClass : BaseClass { };  // private inheritance by default
When to use which?
struct: Usually for passive data structures that just hold data, like Point, Rectangle, Node in a linked list. No complex behavior.

class: Usually for objects that have encapsulation, invariants, and behavior, like BankAccount, Employee, Shape.

This is a convention, not a rule. Technically, you can use either.

Summary to impress:

In C++, struct and class are functionally the same.

Only differences: default access and default inheritance mode.

struct defaults to public, class defaults to private.

Use struct for simple data holders; use class for encapsulated objects.

Never say “struct doesn’t support inheritance” in C++ — that’s wrong. It does.
