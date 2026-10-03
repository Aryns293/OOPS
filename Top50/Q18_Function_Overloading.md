# Q18 Function Overloading

**Interview Answer:**
Function Overloading is a feature in C++ where we can have multiple functions with the same name but different parameters (different number or types of arguments) in the same scope. The compiler decides which function to call based on the arguments passed. It is a form of compile-time polymorphism.

Rules for overloading:

Same function name.

Different parameter list (number, types, or order).

Return type alone cannot distinguish overloaded functions.

Example:

cpp
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
int add(int a, int b, int c) { return a + b + c; }
The compiler picks the right add based on arguments.

How Does Function Overloading Cause Ambiguity?
Ambiguity occurs when the compiler cannot decide which overloaded function to call. This leads to a compile-time error. Common causes:

1. Type Conversion Ambiguity
When an argument can be converted to multiple parameter types, and more than one conversion is equally valid.

cpp
void fun(int x) { cout << "int"; }
void fun(float x) { cout << "float"; }

int main() {
    fun(1.2);   // 1.2 is double. Can convert to int or float? Both are valid.
    // ERROR: ambiguous call
}
Here, 1.2 is a double. It can be converted to int or float, but neither is an exact match. Compiler cannot decide.

2. Default Arguments Ambiguity
When a function with default arguments conflicts with another overload.

cpp
void fun(int x) { cout << "one arg"; }
void fun(int x, int y = 9) { cout << "two args"; }

int main() {
    fun(12);   // Which one? fun(int) or fun(int, int=9)?
    // ERROR: ambiguous call
}
Both are viable. Compiler cannot choose.

3. Pass by Reference vs Pass by Value Ambiguity
When overloads differ only by reference vs value, and the call site doesn’t clearly distinguish.

cpp
void fun(int x) { cout << "value"; }
void fun(int &x) { cout << "reference"; }

int main() {
    int a = 10;
    fun(a);   // Which one? No syntactical difference at call site.
    // ERROR: ambiguous call
}
The compiler cannot tell whether you want value or reference.

Diagram: Ambiguity Causes
text
Function Overloading Ambiguity
          |
   +------+------+------+
   |             |      |
Type Conversion Default Args  Ref vs Value
Key Points to Impress
Function overloading is compile-time polymorphism.

Same name, different parameter list.

Return type alone cannot overload.

Ambiguity happens when the compiler cannot pick the best match.

Common causes: type conversion, default arguments, reference vs value.

Ambiguity is a compile-time error — the program won’t compile.

To fix: avoid ambiguous overloads, use explicit casts, or rename functions.

Summary to impress:

Function overloading: same name, different parameters, resolved at compile time.

Ambiguity: compiler cannot choose between overloads.

Causes: type conversion, default arguments, ref vs value.

Solution: design overloads carefully, avoid overlapping viable candidates.

It’s a powerful feature but must be used with precision.
