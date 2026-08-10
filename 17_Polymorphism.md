# TOPIC 17: Polymorphism

"Many forms" (Greek: poly = many, morphs = forms) — performing a single action in different ways.

## A) Compile-Time (Static) Polymorphism

### a) Function Overloading

Multiple functions, same name, different parameters.

* **Advantage:** increases readability — no need for different names for the same action
* Overloaded via different number of arguments, or different types

**Causes of Ambiguity** (mnemonic diagram: Causes Of Ambiguity → Type Conversion / Function with default arguments / Function with pass by reference):

#### 1. Type Conversion:

```cpp
void fun(int i) { cout << "Value of i is: " << i << endl; }
void fun(float j) { cout << "Value of j is: " << j << endl; }
int main() {
   fun(12);   // fine → fun(int)
   fun(1.2);  // ERROR — ambiguous!
}
```

* **Error:** call of overloaded `fun(double)` is ambiguous — floating point constants are treated as `double`, not `float`, in C++. Fixed if `float` is replaced with `double`.

#### 2. Function with Default Arguments:

```cpp
void fun(int i) { ... }
void fun(int a, int b = 9) { ... }
int main() { fun(12); }  // ERROR — ambiguous!
```

* **Error:** call of overloaded `fun(int)` is ambiguous — compiler can't decide between `fun(int)` and `fun(int, int=9)`.

#### 3. Function with Pass by Reference:

```cpp
void fun(int) { ... }
void fun(int &) { ... }
int main() { int a = 10; fun(a); }  // ERROR
```

* **Ambiguous** — no syntactical difference between `fun(int)` and `fun(int &)` at the call site.

### b) Operator Overloading

E.g., `+` overloaded for a string class to concatenate strings.

**Points to remember:**

* Only for user-defined operators (objects, structures) — NOT for built-in types
* Must contain at least one operand of user-defined type
* Certain operators require member functions (can't use friend function for these)
* Unary operator via member function: no explicit args; via friend function: one argument
* Binary operator via member function: one explicit arg; via friend function: two arguments
* `=` and `&` are already overloaded by default in C++
* Precedence and associativity remain intact

**Cannot be overloaded:** Scope operator `::`, `sizeof`, member selector `.`, member pointer selector `*`, ternary operator `?:` (overloading these would cause serious programming issues — e.g., `sizeof` is evaluated by the compiler, not at runtime).

```cpp
class Complex {
   int real, imag;
public:
   Complex(int r=0, int i=0) { real=r; imag=i; }
   Complex operator+ (Complex const& b) {
      Complex a; a.real = real + b.real; a.imag = imag + b.imag; return a;
   }
   void print() { cout << real << " + i" << imag << endl; }
};
int main() {
   Complex c1(10,5), c2(2,4); 
   Complex c3 = c1 + c2; 
   c3.print();
}
// Output: 12 + i9
```

## B) Runtime (Dynamic) Polymorphism

Achieved via Method Overriding — also called Dynamic Method Dispatch: call resolved at runtime.

**Rules for method overriding:**

* Same name in parent and child
* Same parameters
* Only possible through inheritance

```cpp
class Parent { 
public: 
   void show() { cout << "Inside parent class" << endl; } 
};
class subclass1 : public Parent { 
public: 
   void show() { cout << "Inside subclass1" << endl; } 
};
class subclass2 : public Parent { 
public: 
   void show() { cout << "Inside subclass2"; } 
};
int main() { 
   subclass1 o1; 
   subclass2 o2; 
   o1.show(); 
   o2.show(); 
}
// Output: Inside subclass1 / Inside subclass2
```
