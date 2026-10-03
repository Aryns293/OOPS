# Q19 Operator Overloading

**Interview Answer:**
Operator Overloading is a feature in C++ that allows us to redefine the behavior of existing operators (like +, -, *, ==, <<, etc.) for user-defined types (classes/structs). It lets us use operators with objects in a natural, intuitive way, just like with built-in types. It is a form of compile-time polymorphism.

For example, we can overload + for a Complex class so that c1 + c2 adds two complex numbers.

Why Operator Overloading?
Makes code more readable and intuitive (e.g., c1 + c2 instead of c1.add(c2)).

Allows user-defined types to behave like built-in types.

Enhances expressiveness without sacrificing performance.

Example: Overloading + for Complex Numbers
cpp
class Complex {
private:
    double real, imag;
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // Overload + operator
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    void display() const {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(2, 3), c2(4, 5);
    Complex c3 = c1 + c2;   // Calls operator+
    c3.display();           // Output: 6 + 8i
    return 0;
}
Here, c1 + c2 is translated by the compiler to c1.operator+(c2).

Which Operators Cannot Be Overloaded?
The following operators cannot be overloaded in C++:

Operator	Description
::	Scope resolution operator
sizeof	Size-of operator
.	Member selector (dot operator)
.*	Member pointer selector
?:	Ternary conditional operator
Why?

:: and sizeof are resolved at compile time and are not associated with objects.

. and .* are used to access members; overloading them would create ambiguity and break the language’s core syntax.

?: is a control-flow operator; overloading it would complicate parsing and is unnecessary.

Note: You also cannot create new operators (e.g., ** for exponentiation) or change an operator’s precedence, associativity, or number of operands.

Rules for Operator Overloading
At least one operand must be a user-defined type (class/struct/enum). You cannot overload operators for only built-in types.

You cannot change the number of operands (arity) of an operator.

You cannot change the precedence or associativity.

Some operators must be overloaded as member functions:

=, [], (), ->, ->*

Some operators must be overloaded as non-member functions (usually friend):

<<, >> for streams.

Operators that cannot be overloaded are listed above.

Diagram: Operator Overloading Categories
text
Operator Overloading
        |
   +----+----+
   |         |
Member    Non-Member
(Operator)  (Friend/Global)
   |         |
=, [], (), ->   <<, >>, +, -, ==
Key Points to Impress
Operator overloading = compile-time polymorphism.

Redefines existing operators for user-defined types.

Makes code intuitive and readable.

Cannot overload: ::, sizeof, ., .*, ?:.

Cannot create new operators or change precedence/associativity.

At least one operand must be user-defined.

Some operators must be members; some are better as non-members.

Use it judiciously — overuse can make code confusing.

Summary to impress:

Operator overloading lets you use operators with objects naturally.

Example: Complex c3 = c1 + c2; is cleaner than c1.add(c2).

Cannot overload: ::, sizeof, ., .*, ?:.

Follow rules: at least one user-defined operand, no arity/precedence changes.

It’s a powerful tool for intuitive and expressive code.
