# TOPIC 8: Virtual Functions

A member function declared in a base class and redefined (overridden) by a derived class. Calling it via a base class pointer/reference to a derived object executes the derived version.

* Ensures correct function is called regardless of reference/pointer type
* Achieves Runtime Polymorphism
* Declared with `virtual` keyword in base class
* Resolved at runtime

## Rules
* Cannot be static
* CAN be a friend function of another class
* Accessed via pointer/reference of base class type for runtime polymorphism
* Prototype must match in base and derived class
* Not mandatory to override — if not, base version is used
* Can have a virtual destructor, but cannot have a virtual constructor

## Early vs Late Binding

```cpp
class base {
public:
   virtual void print() { cout << "print base class\n"; }
   void show() { cout << "show base class\n"; }
};
class derived : public base {
public:
   void print() { cout << "print derived class\n"; }
   void show() { cout << "show derived class\n"; }
};
int main() {
   base *bptr; derived d; bptr = &d;
   bptr->print();   // virtual → runtime → "print derived class"
   bptr->show();    // non-virtual → compile time → "show base class"
}
```

* Runtime polymorphism achieved only through base-type pointer/reference
* Late binding (runtime) depends on the content the pointer points to; Early binding depends on the type of the pointer
* If a base virtual function is overridden in derived, you don't need to repeat `virtual` — it's automatically virtual there too

## VTABLE and VPTR

When a class has a virtual function, the compiler:

* Inserts a **VPTR** (virtual pointer) as a data member of every object of that class, pointing to the class's VTABLE
* Maintains a static array of function pointers per class, called **VTABLE**, regardless of whether an object exists

```cpp
class base {
public:
   void fun_1() { cout << "base-1\n"; }
   virtual void fun_2() { cout << "base-2\n"; }
   virtual void fun_3() { cout << "base-3\n"; }
   virtual void fun_4() { cout << "base-4\n"; }
};
class derived : public base {
public:
   void fun_1() { cout << "derived-1\n"; }
   void fun_2() { cout << "derived-2\n"; }
   void fun_4(int x) { cout << "derived-4\n"; }  // different signature!
};
int main() {
   base *p; derived obj1; p = &obj1;
   p->fun_1();  // base-1 (early binding, non-virtual)
   p->fun_2();  // derived-2 (late binding)
   p->fun_3();  // base-3 (late binding, not overridden)
   p->fun_4();  // base-4 (late binding — derived's fun_4(int) is a DIFFERENT function)
}
```

* **Diagram:** P (pointer) → OBJ1 (containing vptr) → points to VTABLE for class derived, which holds: address of DERIVED version of fun_2, address of BASE version of fun_3, address of BASE version of fun_4. The separate VTABLE for class base holds addresses of base versions of fun_2/3/4.
* **How compiler fills VTABLE:** for each virtual function slot, check if overridden in the derived class — if yes, point to derived version, else point to base version. For chain A→B→C, check C first, then B, then A.
* VTABLEs are formed at compile time but are static arrays — all instances of a class share the same VTABLE
* VTABLE is object-independent; VPTR is object-dependent
* `Emp* a = new engineer();` — VPTR assigned according to object type, not pointer type — this is late binding/runtime polymorphism, since object type is only known at execution

### How the compiler performs runtime resolution (2 mechanisms)
* **vtable:** table of function pointers, maintained per class
* **vptr:** pointer to vtable, maintained per object instance

**Diagram:** an Array of emp(0) entries points to Actual Objects (Manager Object with vptr, Engineer Object with vptr, Manager Object with vptr) which point into a shared VTable containing &managerssalary(), &manager.promotes(), &engineerssalary(), &Engineer.promots.

Compiler adds code at two places:
1. In every constructor — sets the object's vptr to point to its class's vtable
2. At every polymorphic call — inserts code to fetch vptr via the base pointer/reference, access the vtable, and call the correct function address

## Limitations of Virtual Functions
* **Slower** — harder for compiler to optimize since it doesn't know exactly which function will run at compile time
* **Difficult to debug** — hard to trace where a call originates in complex systems

## Without Virtual Functions — Example

A `Shape` base class with non-virtual `get_Area()`; derived `Square`/`Rectangle` override it — called via `Shape*`, it ALWAYS calls the BASE version ("This is call to parent class area" printed both times), because binding is compile-time (pointer type), not runtime (object type). With virtual, the correct derived version is called each time.

## Real-Life Use Case

Employee management: base Employee with virtual `raiseSalary()`, `promote()`; derived Manager etc. override with specific logic.

```cpp
void globalRaiseSalary(Employee* emp[], int n) {
   for (int i = 0; i < n; i++) { 
       emp[i]->raiseSalary(); // Polymorphic call
   }  
}
```

## Virtual Destructor

Deleting a derived object via a base pointer with a non-virtual destructor causes undefined behavior.

```cpp
class Base {
public:
   virtual void show(){ cout<<"now we are in base class"<<endl; }
   Base() { cout << "Base created\n"; }
   ~Base() { cout << "Base destroyed\n"; }   // NOT virtual — problematic
};
class Derived: public Base {
public:
   void show(){ cout<<"now we are in Derived class"<<endl; }
   Derived() { cout << "Derived created\n"; }
   ~Derived() { cout << "Derived destroyed\n"; }
};
int main() { Base *b = new Derived; delete b; }
// Output (undefined behavior — Derived destructor NOT called):
// Base created / Derived created / Base destroyed
```

## Virtual Functions — Practice Questions

**Q2:** `Base` has `virtual void show()`, `Derived` overrides. `Base *bp = new Derived; bp->show();` then `Base &br = *bp; br.show();`
* **Answer:** (C) In Derived / In Derived — since `show()` is virtual, it's called according to the object type being pointed/referred to, not the pointer/reference type.

**Q3:** `Base *bp = new Derived; bp->show();` then reassign `bp = &b;` (a `Base` object) and call again.
* **Answer:** (D) In Derived / In Base — pointer initially points to a Derived object, then is reassigned to point to a Base object.

**Q4:** Which is true about pure virtual functions — 1) implementation not provided in the declaring class, 2) class becomes abstract, can't be instantiated?
* **Answer:** (C) Only 2 (Corrected — source gives no explanation for why statement 1 is false; likely because C++ does allow providing a function body for a pure virtual function, as shown later with the pure virtual destructor.)

**Q5:** `Base b; Base *bp;` where `Base` has a pure virtual function.
* **Answer:** (B) Compiler error in line "Base b;" — Base is abstract due to the pure virtual function, so an instance can't be created. `Base *bp;` is fine — we can have pointers/references of abstract classes.

**Q6:** `Base` has pure virtual `show()`; `Derived : public Base {}` does NOT override it; `Derived q;` in main.
* **Answer:** Compiler error — since `Derived` doesn't override the pure virtual function, `Derived` also becomes abstract, so `Derived q;` fails.

**Q7:** `Derived d; Base &br = d; br.show();` where Derived properly overrides.
* **Answer:** (C) In Derived — works correctly via base reference.

**Q9:** Can a destructor be virtual?
* **Answer:** Yes — compiles fine. Needed to call the correct (derived) destructor when deleting via a base pointer.

**Q10:** `Base *Var = new Derived(); delete Var;` where destructor IS virtual.
* **Answer:** (A) Constructor: Base / Constructor: Derived / Destructor: Derived / Destructor: Base — since the destructor is virtual, the derived class destructor is called, which in turn calls the base class destructor.

**Q11:** Can static functions be virtual? `virtual static void fun(){}`
* **Answer:** No — compiler error. Static functions are class-specific, not called on objects; virtual functions are resolved per-object, so combining them is contradictory.

**Q12:** `sizeof(A)` (has a virtual function) vs `sizeof(B)` (no virtual function, otherwise identical).
* **Answer:** (A) a > b — Class A has a VPTR that class B doesn't; the compiler places a VPTR with every object of a class containing (or inheriting) a virtual function.

**Q13:** `class A { virtual void fun(); }; class B: public A { void fun(); }; class C: public B { void fun(); }; B *bp = new C; bp->fun();`
* **Answer:** (C) C::fun() — B::fun() is virtual even without the virtual keyword, since it overrides a virtual base function. When a class has a virtual function, functions with the same signature in ALL descendant classes automatically become virtual too — no need to repeat the virtual keyword.

**Q14:** `Base *bp = new Derived; bp->Base::show();` (note the explicit scope resolution).
* **Answer:** (A) In Base — a base class function can be accessed via the scope resolution operator even if the function is virtual — this explicitly bypasses the virtual dispatch mechanism.

## Pure Virtual Destructor

Yes, a destructor CAN be pure virtual — but it must still have a function body provided.

**Why?** Unlike other functions, destructors aren't "overridden" — they're always called in reverse order of class derivation (derived first, then base). If no body exists for the pure virtual destructor, there'd be nothing to call during destruction, so the compiler/linker enforces a body.

```cpp
class Base {
public:
   virtual ~Base() = 0;   // Pure virtual destructor
};
Base::~Base() {           // Explicit definition still required
   std::cout << "Pure virtual destructor is called";
}
class Derived : public Base {
public:
   ~Derived() { std::cout << "~Derived() is executed\n"; }
};
int main() { Base* b = new Derived(); delete b; }
// Output: ~Derived() is executed / Pure virtual destructor is called
```

A class becomes abstract when it contains a pure virtual destructor (or any pure virtual function) — even a function with no definition qualifies.

## Virtual Constructor — Not Possible
* No VTABLE exists yet while the constructor is being called
* Because the object isn't created yet, virtual construction is impossible
* The compiler must know the object's type BEFORE creating it

## Can Virtual Functions Be Private?

Yes.

```cpp
class base {
public:
   virtual ~base(){ ... }
   void show(){ ... }
   virtual void print(){ std::cout << "print() called on base class\n"; }
};
class derived : public base {
public:
   derived() : base(){ ... }
   virtual ~derived(){ ... }
private:
   virtual void print(){ std::cout << "print() called on derived class\n"; }  // private!
};
int main(){
   base* b_ptr = new derived();
   b_ptr->show();
   b_ptr->print();   // Still works! Calls derived's private print()
   delete b_ptr;
}
```

Even with `print()` private in derived, calling it through a base class pointer still works — the base class defines a public interface, and the derived class merely overrides the implementation. Access is checked against the static declaring type, not the access level at the polymorphic call site.
