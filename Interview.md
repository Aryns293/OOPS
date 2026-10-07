# 60 OOPs Interview Questions for SDE-1 Freshers (C++)

## Section 1: OOP Fundamentals (Q1–Q8)

---

**Q1. What is Object-Oriented Programming? Why do we need it?**

**Answer:** OOP is a programming paradigm that organizes software design around **objects** rather than functions and logic. An object is an instance of a class that bundles data (attributes) and behavior (methods) into a single unit.

**We need OOP because:**
- **Modularity** – Code is organized into self-contained objects, easier to manage and debug.
- **Reusability** – Through inheritance, we reuse existing code.
- **Security** – Through encapsulation, data is hidden and accessed only via controlled public methods.
- **Maintainability** – Changes in one object don't ripple everywhere.
- **Real-world modeling** – Objects map directly to real-world entities like Student, Account, Car.
- **Flexibility & scalability** – Through abstraction and polymorphism.

It solves the main problem of procedural programming where global data is accessible from anywhere, leading to unintended modifications and namespace pollution.

---

**Q2. What are the four pillars of OOP?**

**Answer:** The four pillars are:

| Pillar | Meaning | One-liner |
|--------|---------|-----------|
| **Encapsulation** | Bundling data + methods, restricting direct access | Data security |
| **Abstraction** | Hiding implementation, showing only functionality | Simplicity |
| **Inheritance** | Child class acquires parent's properties/behaviors | Reusability |
| **Polymorphism** | Same interface, different behaviors | Flexibility |

**Code example (all four):**
```cpp
// Abstraction + Encapsulation
class Shape {
protected:
    double a, b;                    // encapsulated data
public:
    virtual double area() = 0;      // abstraction: contract only
};

// Inheritance
class Rectangle : public Shape {
public:
    Rectangle(double x, double y) { a = x; b = y; }
    double area() override { return a * b; }   // Polymorphism
};

class Circle : public Shape {
public:
    Circle(double r) { a = r; }
    double area() override { return 3.14 * a * a; }
};

void printArea(Shape* s) { cout << s->area(); }  // works for any Shape
```

---

**Q3. Difference between Procedural Oriented Programming (POP) and OOP?**

**Answer:**

| POP | OOP |
|-----|-----|
| Program divided into **functions** | Program divided into **objects** |
| Importance on **functions**, not data | Importance on **data** rather than procedures |
| Follows **Top-Down** approach | Follows **Bottom-Up** approach |
| No access specifiers | Has `public`, `private`, `protected` |
| Data moves freely between functions | Data is encapsulated; controlled access |
| Less secure — no data hiding | More secure — data hiding via encapsulation |
| Overloading not possible | Function/operator overloading possible |
| Examples: C, Pascal, FORTRAN | Examples: C++, Java, C#, Python |

---

**Q4. What is a Class? What is an Object? Difference?**

**Answer:**
- **Class:** A user-defined blueprint/template from which objects are created. It defines structure (data members) and behavior (member functions). No memory is allocated when a class is declared. It is a **logical entity**.
- **Object:** An instance of a class. It is a **real-world/physical entity**. Memory is allocated when an object is created. Each object has its own copy of data members (except static).

**Example:**
```cpp
class Student {
    string name;
    int rollNo;
public:
    void display() { cout << name << " - " << rollNo; }
};

int main() {
    Student s1, s2;    // two objects created
    s1.name = "Alice"; s1.rollNo = 101;
    s2.name = "Bob";   s2.rollNo = 102;
}
```

| Feature | Class | Object |
|---------|-------|--------|
| Definition | Blueprint/Template | Instance of class |
| Existence | Logical | Physical |
| Memory | Not allocated when declared | Allocated when created |
| Quantity | Declared once | Many can be created |
| Values | No specific values | Holds specific values |
| Example | `class Car { };` | `Car c1, c2;` |

---

**Q5. Difference between Class and Structure in C++?**

**Answer:** In C++, `struct` and `class` are almost identical. The only technical differences are:

| Feature | `class` | `struct` |
|---------|---------|----------|
| Default member access | **private** | **public** |
| Default inheritance mode | **private** | **public** |
| Can have methods? | Yes | Yes |
| Can have constructors/destructors? | Yes | Yes |
| Can inherit? | Yes | Yes |
| Can have virtual functions? | Yes | Yes |
| Typical usage | Encapsulated objects with behavior | Simple data grouping (POD) |

**Convention:** Use `struct` for simple data holders (`Point`, `Node`), `class` for encapsulated objects (`BankAccount`, `Employee`).

---

**Q6. What is Encapsulation? Why is it called Data Hiding?**

**Answer:** Encapsulation is the process of **binding data and the methods that operate on that data into a single unit (class)** and restricting direct access to the internal state.

**Why "data hiding"?** Because we make data members `private`, so external code cannot access them directly — they're hidden. Access is only through public methods, where we can add validation.

**Example:**
```cpp
class Student {
private:
    int age;
public:
    void setAge(int a) {
        if (a > 0 && a < 100) age = a;   // validation
        else cout << "Invalid age!";
    }
    int getAge() { return age; }
};
// s.age = -5;   // ERROR: private
// s.setAge(-5); // Rejected by validation
```

**Benefits:** Security, validation, maintainability, modularity.

---

**Q7. Difference between Abstraction and Encapsulation?**

**Answer:**

| Abstraction | Encapsulation |
|-------------|---------------|
| Hides **unnecessary details**, shows only necessary ones | **Binds** data + methods into a single unit |
| Focus: **WHAT** the object does | Focus: **HOW** data is protected/accessed |
| Design/interface level | Implementation level |
| Achieved via abstract classes, interfaces, pure virtual functions | Achieved via access modifiers (private/protected) + getters/setters |
| Example: `Shape` with `area()` — user doesn't know how area is computed | Example: `Student` with private `name` and public `getName()` |

They are **complementary, not competing.** Encapsulation enables abstraction.

---

**Q8. What is the difference between Overloading and Overriding?**

**Answer:**

| Feature | Overloading | Overriding |
|---------|------------|------------|
| Binding | Compile-time (static) | Runtime (dynamic) |
| Scope | Same class or same scope | Base and derived classes |
| Signature | Must **differ** (parameters) | Must be **identical** |
| Inheritance | Not required | Required |
| `virtual` keyword | Not needed | Base method **must** be `virtual` |
| Return type | Can differ | Must be same (or covariant) |
| Purpose | Convenience, readability | Runtime polymorphism |
| Resolution | By compiler based on arguments | By VTABLE/VPTR at runtime |
| Example | `add(int, int)` vs `add(double, double)` | `Animal::sound()` vs `Dog::sound()` |

**Code:**
```cpp
// Overloading
class Calc {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
};

// Overriding
class Animal {
public: virtual void sound() { cout << "Animal\n"; }
};
class Dog : public Animal {
public: void sound() override { cout << "Dog barks\n"; }
};
```

---

## Section 2: Constructors & Destructors (Q9–Q18)

---

**Q9. What is a Constructor? Characteristics?**

**Answer:** A constructor is a **special member function** automatically called when an object is created. It initializes data members.

**Characteristics:**
1. Same name as the class.
2. No return type (not even `void`).
3. Called automatically at object creation.
4. Can be **overloaded**.
5. Cannot be **virtual** (no VTABLE exists yet).
6. Cannot be **inherited**.
7. Cannot be **static**.
8. Address cannot be referenced.
9. Usually declared in **public** section (can be private for special cases).
10. Makes implicit calls to `new`/`delete` during memory allocation.

---

**Q10. What are the types of Constructors?**

**Answer:** Three types:

**1. Default Constructor** — no arguments.
```cpp
class Student { int rollNo; public: Student() { rollNo = 0; } };
```
- If you don't define one, the compiler generates an empty one (garbage values).
- If you define a parameterized constructor, the compiler will **NOT** generate a default one.

**2. Parameterized Constructor** — takes arguments.
```cpp
class Student {
    int rollNo; string name;
public:
    Student(int r, string n) { rollNo = r; name = n; }
};
Student s1(101, "Alice");    // implicit call
Student s2 = Student(102, "Bob");  // explicit call
```

**3. Copy Constructor** — takes an object (by reference) and copies its data.
```cpp
class Student {
    int rollNo;
public:
    Student(const Student &s) { rollNo = s.rollNo; }
};
Student s2 = s1;   // copy constructor called
```

---

**Q11. What is a Copy Constructor? When is it called?**

**Answer:** A copy constructor creates a new object as a copy of an existing object of the same class.

**Syntax:** `ClassName(const ClassName &obj);`

**Called automatically when:**
1. A new object is initialized from another: `Student s2 = s1;`
2. An object is passed **by value** to a function.
3. An object is returned **by value** from a function.

**Why must its argument be passed by reference?**
If passed by value, calling the copy constructor would require making a copy of the argument — which itself would call the copy constructor — leading to **infinite recursion**. So it must take a **reference**.

**Why `const`?** So the original object cannot be accidentally modified, and to allow copying of `const` objects.

---

**Q12. What is the difference between Copy Constructor and Assignment Operator?**

**Answer:**

```cpp
MyClass t1, t2;
MyClass t3 = t1;   // (1) Copy Constructor
t2 = t1;           // (2) Assignment Operator
```

| Copy Constructor | Assignment Operator |
|------------------|---------------------|
| Creates a **new object** from an existing one | Assigns to an **already existing** object |
| Makes new memory storage every time | Does **not** make new memory storage |
| Called during initialization | Called after both objects exist |
| `MyClass t3 = t1;` | `t2 = t1;` |

**Key difference:** Copy constructor makes **new memory storage** every time; assignment operator does **not**.

---

**Q13. What is the Rule of Three?**

**Answer:** If a class needs a custom **destructor**, **copy constructor**, or **copy assignment operator**, it likely needs **all three**.

**Why?** Because they all manage the same resource (e.g., dynamically allocated memory). If you define one, the compiler-generated versions of the others will do shallow copies, leading to double-free, dangling pointers, or memory leaks.

**Example:**
```cpp
class Student {
    int* rollNo;
public:
    Student(int r) { rollNo = new int(r); }
    ~Student() { delete rollNo; }                    // destructor
    Student(const Student& s) {                      // copy constructor
        rollNo = new int(*(s.rollNo));
    }
    Student& operator=(const Student& s) {           // copy assignment
        if (this != &s) {
            delete rollNo;
            rollNo = new int(*(s.rollNo));
        }
        return *this;
    }
};
```

---

**Q14. What is the difference between Shallow Copy and Deep Copy?**

**Answer:**

**Shallow Copy:** Copies all member values; for pointers, copies the **address** (not what they point to). Both objects point to the **same memory**.

**Deep Copy:** Copies all fields and **allocates new memory** for pointers. Objects are **independent**.

| Feature | Shallow Copy | Deep Copy |
|---------|--------------|-----------|
| Pointer handling | Copies address | Allocates new memory, copies data |
| Independence | Objects share memory | Objects are independent |
| Default behavior | Compiler-generated | Must be user-defined |
| Risk | Dangling pointer, double-free | Safe, but slower |
| When needed | Simple classes without pointers | Classes with dynamic memory |

**Diagram:**
```
Shallow:  s1.ptr ---> [ 101 ] <--- s2.ptr   (shared)
Deep:     s1.ptr ---> [ 101 ]
          s2.ptr ---> [ 101 ]                (separate)
```

**Code (Deep Copy):**
```cpp
Student(const Student& s) {
    rollNo = new int(*(s.rollNo));   // allocate new memory
}
```

---

**Q15. What is a Destructor? When is it called?**

**Answer:** A destructor is a special member function that destroys the object and frees acquired resources. It is the **opposite** of a constructor.

**Syntax:** `~ClassName() { }`

**Called automatically when:**
1. Object goes out of scope.
2. Program ends (for global/static objects).
3. A `{}` scope containing a local variable ends.
4. `delete` is called on a dynamically allocated object.

**Rules:**
- Same name as class, preceded by `~`.
- Takes **no parameters**.
- No return type (not even `void`).
- Only **one** destructor per class (no overloading).
- Cannot be `static` or `const`.
- Should be **public** (unless private destructor is intended for special control).
- Default works fine unless class has dynamic memory — then custom destructor needed to avoid leaks.

---

**Q16. What is a Virtual Destructor? Why do we need it?**

**Answer:** A virtual destructor ensures that when we `delete` a derived object through a **base class pointer**, the derived destructor is called first, then the base destructor.

**Without virtual destructor:**
```cpp
class Base { public: ~Base() { cout << "Base destroyed\n"; } };
class Derived : public Base {
    int* data;
public:
    Derived() { data = new int[100]; }
    ~Derived() { delete[] data; cout << "Derived destroyed\n"; }
};
int main() {
    Base* bp = new Derived();
    delete bp;   // Only Base destructor called! Derived destructor skipped → memory leak
}
```

**With virtual destructor:**
```cpp
class Base { public: virtual ~Base() { cout << "Base destroyed\n"; } };
// Now both destructors called in correct order
```

**Rule:** If a class has any virtual function, give it a virtual destructor.

---

**Q17. Can a Constructor be Virtual? Can a Destructor be Virtual?**

**Answer:**

**Constructor — NO.** 
- Virtual mechanism needs VTABLE/VPTR, which is initialized **inside** the constructor.
- At the time constructor runs, the object is still being constructed — VPTR doesn't point to correct VTABLE yet.
- Also, virtual call needs an existing object to look up VTABLE, but constructor is called to **create** the object.

**Destructor — YES.**
- Needed to ensure derived destructor is called when deleting via base pointer.
- Prevents memory leaks and undefined behavior.
- A **pure virtual destructor** is also possible (`virtual ~Base() = 0;`) but must be **defined** outside the class.

---

**Q18. What is a Pure Virtual Destructor? Why does it need a body?**

**Answer:** Yes, a destructor can be pure virtual: `virtual ~Base() = 0;`

**Why must it have a body?** Unlike other functions, destructors are **not "overridden"** — they are always called in reverse order of class derivation (derived first, then base). If no body exists for the pure virtual destructor, there'd be nothing to call during destruction. So the compiler/linker enforces a body.

```cpp
class Base {
public:
    virtual ~Base() = 0;   // Pure virtual destructor
};
Base::~Base() {            // Explicit definition still required
    cout << "Pure virtual destructor called";
}
class Derived : public Base {
public:
    ~Derived() { cout << "~Derived() executed\n"; }
};
int main() { Base* b = new Derived(); delete b; }
// Output: ~Derived() executed / Pure virtual destructor called
```

A class becomes **abstract** when it contains a pure virtual destructor.

---

## Section 3: this Pointer, Static, Friend (Q19–Q24)

---

**Q19. What is the `this` pointer? When is it necessary?**

**Answer:** `this` is an implicit pointer available only inside **non-static member functions**. It points to the current object that invoked the member function.

**Uses:**
1. Resolve name conflicts: `this->x = x;`
2. Return the current object: `return *this;`
3. Pass the current object as a parameter.

**When necessary?** When local variable names match data member names — the compiler won't know which one you mean without `this`.

```cpp
class Mobile {
    string model; int year;
public:
    void set_details(string model, int year) {
        this->model = model;              // necessary!
        this->year = year;
    }
};
```

**Not available in:** static member functions (no object), friend functions (not members).

---

**Q20. What is a Static Data Member?**

**Answer:** A static data member is a class member shared by **all objects** of the class. Only **one copy** exists, regardless of how many objects are created.

**Key points:**
- Declared inside class with `static`, defined outside class.
- Initialized before any object is created (even before `main()`).
- Lifetime = entire program.
- Used for properties common to all objects (e.g., `rateOfInterest`, `companyName`) or as a counter.

```cpp
class Student {
    static int count;
public:
    Student() { count++; }
    static int getCount() { return count; }
};
int Student::count = 0;   // definition outside class

int main() {
    Student s1, s2, s3;
    cout << Student::getCount();   // 3
}
```

---

**Q21. What is a Static Member Function?**

**Answer:** A static member function is declared with `static` inside a class. It works for the class as a whole, not for a specific object.

**Key points:**
- Called using class name: `ClassName::func()`.
- Can be called without creating an object.
- Can access **only static** data members and static member functions.
- Has **no `this` pointer** — that's why it can't access ordinary members.
- Cannot be virtual.

```cpp
class Math {
    static int count;
public:
    static int add(int a, int b) { return a + b; }
    static void increment() { count++; }
};
int Math::count = 0;

int main() {
    cout << Math::add(2, 3);   // 5
}
```

---

**Q22. What is a Friend Function? Characteristics?**

**Answer:** A friend function is a **non-member function** granted access to the **private and protected** members of a class. It is declared inside the class with the `friend` keyword.

**Characteristics:**
- Not in the scope of the class it's a friend of.
- Cannot be called using the object of that class.
- Invoked like a normal function (without object).
- Cannot access member names directly — must use an object and dot operator.
- Can be declared in **public or private** section (no difference).
- Usually has objects as arguments.
- Can be a global function or a member of another class.
- **Violates encapsulation** — that's why C++ is not a "pure" OOP language.

```cpp
class Box {
private: int length;
public:
    Box() { length = 10; }
    friend int printLength(Box b);   // friend declaration
};

int printLength(Box b) {             // no `friend`, no `::`
    b.length += 10;
    return b.length;
}

int main() {
    Box b;
    cout << printLength(b);   // 20
}
```

---

**Q23. What is a Friend Class?**

**Answer:** When a class is declared as a friend of another class, **all member functions** of the friend class become friend functions of the other class.

```cpp
class Other { void fun(); };

class WithFriend {
private:
    int i;
public:
    void getdata();
    friend void Other::fun();   // one member function as friend
    friend class Other;         // entire class as friend
};
```

**Note:** The friend class must be **forward declared** before it can be used in the `friend` declaration.

---

**Q24. Why is C++ not called a "pure" object-oriented language?**

**Answer:** Because of **friend functions**. Friend functions are non-member functions that can access private/protected members of a class. This **violates encapsulation** — one of the core principles of pure OOP.

Other reasons often cited:
- C++ supports **global variables** and **global functions** (not everything is an object).
- C++ supports **primitive data types** (int, char, etc.) that are not objects.
- C++ allows **procedural programming** style as well.

Pure OOP languages (like Smalltalk) treat everything as an object.

---

## Section 4: Inheritance (Q25–Q32)

---

**Q25. What is Inheritance? What are its types?**

**Answer:** Inheritance is a mechanism where one class (child/derived) acquires properties and behaviors of another class (parent/base). It represents an **"is-a"** relationship and promotes code reusability.

**Types (5):**

| Type | Structure | Example |
|------|-----------|---------|
| **Single** | A → B | `class B : public A` |
| **Multilevel** | A → B → C | `class B : public A; class C : public B;` |
| **Hierarchical** | A → B, A → C | One base, multiple derived |
| **Multiple** | A, B → C | `class C : public A, public B` |
| **Hybrid** | Combination | Diamond shape |

**Note:** Java does **not** support multiple inheritance via classes (only via interfaces) to avoid the diamond problem.

---

**Q26. What are the Modes of Inheritance in C++?**

**Answer:** Three modes — `public`, `protected`, `private`.

| Base Member → | Public Derivation | Protected Derivation | Private Derivation |
|---------------|-------------------|----------------------|---------------------|
| `public` | `public` | `protected` | `private` |
| `protected` | `protected` | `protected` | `private` |
| `private` | Not inherited | Not inherited | Not inherited |

**Default mode:**
- `class` → **private** inheritance by default.
- `struct` → **public** inheritance by default.

**Public inheritance** = "is-a" relationship (most common).
**Private inheritance** = "implemented-in-terms-of" (prefer composition instead).

---

**Q27. What is the Diamond Problem? How is it solved in C++?**

**Answer:** The Diamond Problem occurs in **multiple inheritance** when a class D inherits from B and C, and both B and C inherit from a common base A. This creates **two copies** of A's members inside D — one via B, one via C. Accessing A's members through D causes **ambiguity**.

```
      A
     / \
    B   C
     \ /
      D
```

**Problem:**
```cpp
class A { public: int data; };
class B : public A { };
class C : public A { };
class D : public B, public C { };

int main() {
    D obj;
    obj.data = 10;   // ERROR: ambiguous! B::A::data or C::A::data?
}
```

**Solution in C++: Virtual Base Class**
```cpp
class B : virtual public A { };
class C : virtual public A { };
class D : public B, public C { };

int main() {
    D obj;
    obj.data = 10;   // OK: only one shared copy of A
}
```

Now D has only **one** instance of A, shared by B and C. Java avoids this by not supporting multiple inheritance via classes.

---

**Q28. What is the difference between Inheritance and Composition?**

**Answer:**

| Feature | Inheritance | Composition |
|---------|-------------|-------------|
| Relationship | **is-a** | **has-a** |
| Coupling | Tight | Loose |
| Flexibility | Less flexible (fixed at compile time) | More flexible (can change at runtime) |
| Reuse | Reuses interface + implementation | Reuses implementation via delegation |
| Fragile Base Class | Yes | No |
| Encapsulation | Breaks encapsulation | Preserves encapsulation |
| When to use | True subtype relationship | Just need functionality of another class |

**Code:**
```cpp
// Inheritance (is-a)
class Car : public Vehicle { };

// Composition (has-a)
class Car {
    Engine engine;   // Car HAS-AN Engine
};
```

**Rule:** Favor composition over inheritance — a key design principle.

---

**Q29. What are the limitations of Inheritance?**

**Answer:**
1. **Tight coupling** — Child is tightly coupled to parent. Changes in parent can break child.
2. **Fragile Base Class Problem** — A safe-looking change in base can unknowingly break derived classes.
3. **Complexity in deep hierarchies** — Hard to understand, debug, maintain.
4. **Inflexibility** — Relationship fixed at compile time; cannot change at runtime.
5. **Breaks encapsulation** — Base often exposes protected members, weakening encapsulation.
6. **Diamond Problem** — Multiple inheritance causes ambiguity (in C++).
7. **Overuse leads to poor design** — Misused for code reuse when relationship isn't truly "is-a".

**Solution:** Prefer composition, keep hierarchies shallow, program to interfaces.

---

**Q30. What is Object Slicing?**

**Answer:** Object slicing occurs when a derived class object is assigned to a base class object **by value** (not by pointer/reference). The derived class's additional data members and overridden virtual functions are "sliced off," leaving only the base class portion.

```cpp
class Base { public: int a; };
class Derived : public Base { public: int b; };

int main() {
    Derived d;
    Base b = d;   // slicing: b only has 'a', 'b' is lost
}
```

**Solution:** Use pointers or references:
```cpp
Base* bp = &d;   // no slicing
Base& br = d;    // no slicing
```

**Note:** Avoid passing by value in polymorphic hierarchies.

---

**Q31. What is Multiple Inheritance Ambiguity? How to resolve it?**

**Answer:** When a class inherits from two base classes that both have a member with the **same name**, accessing that member is ambiguous.

```cpp
class A { public: void show() { cout << "A\n"; } };
class B { public: void show() { cout << "B\n"; } };
class C : public A, public B { };

int main() {
    C obj;
    // obj.show();    // ERROR: ambiguous
    obj.A::show();    // OK: A::show
    obj.B::show();    // OK: B::show
}
```

**Solution:** Use the **scope resolution operator** `::` to specify which base class's member to use.

**Note:** If one function is defined in the derived class itself, that one is used by default.


## Section 5: Polymorphism & Virtual Functions (Q33–Q42)

---

**Q33. What is Polymorphism? Types?**

**Answer:** Polymorphism means "many forms" — the ability of a single interface to represent different underlying forms/behaviors. Same function call behaves differently based on the object.

**Two types:**

| Type | Binding | Achieved by | Inheritance needed? |
|------|---------|-------------|---------------------|
| **Compile-time (Static)** | Early binding | Function overloading, Operator overloading | No |
| **Runtime (Dynamic)** | Late binding | Method overriding with virtual functions | Yes |

**Diagram:**
```
                Polymorphism
               /            \
   Compile-Time             Runtime
   (Static)                 (Dynamic)
      |                        |
Function Overloading      Method Overriding
Operator Overloading      (using virtual functions)
```

**Compile-time example:**
```cpp
class Calc {
public:
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
};
```

**Runtime example:**
```cpp
class Shape {
public: virtual double area() { return 0; }
};
class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14 * r * r; }
};
void printArea(Shape* s) { cout << s->area(); }   // runtime dispatch
```

---

**Q34. What is a Virtual Function? Why do we need it?**

**Answer:** A virtual function is a member function declared in a base class using the `virtual` keyword and **overridden** by a derived class. When called through a base class pointer/reference to a derived object, the **derived class version** is executed — resolved at **runtime**.

**Why needed?** Without virtual, the function called is determined by the **pointer type**, not the object type.

```cpp
// WITHOUT virtual
class Base { public: void show() { cout << "Base\n"; } };
class Derived : public Base { public: void show() { cout << "Derived\n"; } };
int main() {
    Base* bp = new Derived();
    bp->show();   // Output: Base (wrong!)
}

// WITH virtual
class Base { public: virtual void show() { cout << "Base\n"; } };
class Derived : public Base { public: void show() override { cout << "Derived\n"; } };
int main() {
    Base* bp = new Derived();
    bp->show();   // Output: Derived (correct!)
}
```

---

**Q35. Explain VTABLE and VPTR.**

**Answer:** When a class has a virtual function, the compiler adds two mechanisms:

**1. VTABLE (Virtual Table)** — a static array of function pointers, one per class that has virtual functions. Each entry points to the most-derived version of a virtual function for that class. **Object-independent.**

**2. VPTR (Virtual Pointer)** — a hidden data member inserted into every object of a class with virtual functions. It points to the class's VTABLE. **Object-dependent.**

**How it works:**
1. Compiler adds code in every **constructor** to set the object's VPTR to point to its class's VTABLE.
2. At every **polymorphic call**, compiler inserts code to:
   - Fetch VPTR via the base pointer.
   - Access the VTABLE.
   - Call the correct function address.

**Diagram:**
```
Base* bp = new Derived();
bp -> [ Derived Object ]
        +-----------+
        | VPTR -----|-----> Derived VTABLE
        | data      |       +---------------------+
        +-----------+       | &Derived::show()    |
                            | &Base::show()       |
                            +---------------------+
```

**How compiler fills VTABLE:** For each virtual function, check if overridden in the current class. If yes, point to it; else point to base version.

**Note:** VTABLEs are formed at **compile time** but used at **runtime** for dispatch.

---

**Q36. Rules for Virtual Functions?**

**Answer:**
1. Must be members of some class.
2. Cannot be **static**.
3. Accessed via pointer/reference of base class for runtime polymorphism.
4. Prototype must match in base and derived class.
5. Not mandatory to override — if not, base version is used.
6. Can have a **virtual destructor**, but **cannot** have a **virtual constructor**.
7. Can be a **friend function** of another class.
8. If a base virtual function is overridden in derived, you don't need to repeat `virtual` — it's automatically virtual there too.

---

**Q37. What is a Pure Virtual Function? What is an Abstract Class?**

**Answer:**

**Pure Virtual Function:** A virtual function with **no implementation** in the base class, declared by assigning `0`.
```cpp
virtual void show() = 0;
```

**Abstract Class:** A class that contains **at least one pure virtual function**. It **cannot be instantiated** — only inherited.

```cpp
class Shape {
public:
    virtual double area() = 0;   // pure virtual
    virtual ~Shape() {}
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() override { return 3.14 * r * r; }
};

int main() {
    // Shape s;              // ERROR: abstract
    Shape* s = new Circle(5); // OK: pointer allowed
    cout << s->area();
}
```

**Key points:**
- Derived class **must** implement all pure virtual functions, or it also becomes abstract.
- We can have **pointers/references** of abstract classes.

---

**Q38. Can a Virtual Function be Private?**

**Answer:** Yes. Even if the virtual function is private in the derived class, calling it through a base class pointer still works — because the base class defines a **public interface** and the derived class merely overrides the implementation.

**Access is checked against the static declaring type**, not the access level at the polymorphic call site.

```cpp
class base {
public:
    virtual void print() { cout << "base print\n"; }
};
class derived : public base {
private:
    void print() override { cout << "derived print\n"; }  // private!
};
int main() {
    base* b = new derived();
    b->print();   // Still works! Calls derived's private print()
}
```

---

**Q39. What is the difference between Early Binding and Late Binding?**

**Answer:**

| Early Binding (Static) | Late Binding (Dynamic) |
|------------------------|------------------------|
| Resolved at **compile time** | Resolved at **runtime** |
| Depends on **type of pointer** | Depends on **content pointed to** (object type) |
| Used for non-virtual functions | Used for virtual functions |
| Faster | Slightly slower (vtable lookup) |
| Also called static binding | Also called dynamic binding |

**Example:**
```cpp
class base {
public:
    virtual void print() { cout << "base print\n"; }
    void show() { cout << "base show\n"; }
};
class derived : public base {
public:
    void print() override { cout << "derived print\n"; }
    void show() { cout << "derived show\n"; }
};
int main() {
    base* bptr; derived d; bptr = &d;
    bptr->print();   // Late binding → "derived print"
    bptr->show();    // Early binding → "base show"
}
```

---

**Q40. What happens if a virtual function is called inside a constructor or destructor?**

**Answer:** During construction and destruction, **virtual dispatch does not work as expected**. The call resolves to the **current class's version**, not the derived class's.

**Why?**
- During **base class construction**, the derived part doesn't exist yet.
- During **base class destruction**, the derived part is already destroyed.
- The VPTR points to the **current class's VTABLE**.

```cpp
class Base {
public:
    Base() { show(); }              // calls Base::show()
    virtual void show() { cout << "Base\n"; }
};
class Derived : public Base {
public:
    Derived() { show(); }           // calls Derived::show()
    void show() override { cout << "Derived\n"; }
};
int main() {
    Derived d;   // Output: Base, then Derived
}
```

**Best practice:** Avoid calling virtual functions in constructors/destructors.

---

**Q41. What are the limitations of Virtual Functions?**

**Answer:**
1. **Slower** — The function call takes slightly longer due to the virtual mechanism. Harder for compiler to optimize since it doesn't know which function will run at compile time.
2. **Difficult to debug** — Hard to trace where a call originates in complex systems.
3. **Increased object size** — Every object gets a hidden VPTR (typically 8 bytes on 64-bit systems).
4. **Cannot be static** — Static functions are class-specific, virtual functions are object-specific.

---

**Q42. Real-life use case of Virtual Functions?**

**Answer:** Employee management software for an organization:

```cpp
class Employee {
public:
    virtual void raiseSalary() { /* common raise salary code */ }
    virtual void promote() { /* common promote code */ }
};

class Manager : public Employee {
    void raiseSalary() override { /* Manager-specific raise */ }
    void promote() override { /* Manager-specific promote */ }
};

class Engineer : public Employee {
    void raiseSalary() override { /* Engineer-specific raise */ }
    void promote() override { /* Engineer-specific promote */ }
};

void globalRaiseSalary(Employee* emp[], int n) {
    for (int i = 0; i < n; i++)
        emp[i]->raiseSalary();   // Polymorphic call
}
```

We can create a list of base class pointers and call methods of any derived class **without knowing the exact type**. Each employee type has its own logic, but we don't need to worry — only the correct function is called.

---

## Section 6: Operator Overloading, Templates (Q43–Q48)

---

**Q43. What is Operator Overloading? Rules?**

**Answer:** Operator overloading allows us to **redefine the behavior of existing operators** (like `+`, `-`, `==`, `<<`) for **user-defined types** (classes/structs). It is a form of **compile-time polymorphism**.

**Rules:**
1. Only **existing** operators can be overloaded.
2. At least one operand must be of a **user-defined type**.
3. Cannot change basic meaning, precedence, or associativity.
4. `=`, `&` are already overloaded by default.
5. Some operators **must be member functions**: `=`, `[]`, `()`, `->`, `->*`.
6. Some are better as **non-member (friend)**: `<<`, `>>`.

**Cannot be overloaded:**
- Scope resolution `::`
- `sizeof`
- Member selector `.`
- Member pointer selector `.*`
- Ternary `?:`

**Example:**
```cpp
class Complex {
    int real, imag;
public:
    Complex(int r = 0, int i = 0) : real(r), imag(i) {}
    Complex operator+(const Complex& b) {
        return Complex(real + b.real, imag + b.imag);
    }
    void print() { cout << real << " + i" << imag << endl; }
};
int main() {
    Complex c1(10, 5), c2(2, 4);
    Complex c3 = c1 + c2;   // calls operator+
    c3.print();             // 12 + i9
}
```

---

**Q44. What is Function Overloading? What causes ambiguity?**

**Answer:** Function overloading = multiple functions with the **same name** but **different parameters** (number, type, or order) in the same scope. Compiler picks the right one based on arguments.

**Causes of Ambiguity:**

**1. Type Conversion:**
```cpp
void fun(int i) { }
void fun(float j) { }
int main() { fun(1.2); }   // ERROR: ambiguous (1.2 is double)
```
Floating point constants are treated as `double`, not `float` — can convert to both int and float.

**2. Default Arguments:**
```cpp
void fun(int i) { }
void fun(int a, int b = 9) { }
int main() { fun(12); }   // ERROR: ambiguous
```

**3. Pass by Reference vs Value:**
```cpp
void fun(int) { }
void fun(int &) { }
int main() { int a = 10; fun(a); }   // ERROR: ambiguous
```

---

**Q45. What is a Template? Why use Templates?**

**Answer:** Templates allow **generic programming** — writing code that works with any data type. It follows the **DRY (Don't Repeat Yourself)** principle.

**Why use templates?**
- To avoid writing the same function/class for different data types.
- To follow DRY principle.
- Generic programming.

**Types:**
1. **Function Templates**
2. **Class Templates**

**Function Template:**
```cpp
template <class T>
T max(T a, T b) { return (a > b) ? a : b; }

int main() {
    cout << max(3, 7);       // T = int
    cout << max(3.5, 2.1);   // T = double
}
```

**Class Template:**
```cpp
template <class T>
class Vector {
    T* arr; int size;
public:
    Vector(int m) { size = m; arr = new T[size]; }
    T dotProd(Vector& v) {
        T d = 0;
        for (int i = 0; i < size; i++) d += arr[i] * v.arr[i];
        return d;
    }
};
```

---

**Q46. What are Class Templates with Multiple Parameters?**

**Answer:** You can use more than one generic data type:

```cpp
template <class T1, class T2>
class Test {
    T1 a; T2 b;
public:
    Test(T1 x, T2 y) { a = x; b = y; }
    void show() { cout << a << " " << b; }
};

int main() {
    Test<float, int> t1(1.23, 123);
    Test<int, char> t2(100, 'w');
    t1.show(); t2.show();
}
```

---

**Q47. What are Templates with Default Parameters?**

**Answer:** Data types can be initialized with default values:

```cpp
template <class T1 = int, class T2 = float, class T3 = char>
class MyClass {
public:
    T1 a; T2 b; T3 c;
    MyClass(T1 x, T2 y, T3 z) : a(x), b(y), c(z) {}
    void display() { cout << a << " " << b << " " << c << endl; }
};

int main() {
    MyClass<> obj1(4, 6.4, 'l');        // uses defaults
    MyClass<float, char, char> obj2(4.3, 'r', 'c');  // overrides
}
```

---

**Q48. What is the difference between Function Template and Function Overloading?**

**Answer:**

| Feature | Function Template | Function Overloading |
|---------|-------------------|----------------------|
| Definition | One generic function for all types | Multiple functions with same name, different params |
| Code | Single definition | Multiple definitions |
| Resolution | Compiler instantiates for each type used | Compiler picks based on arguments |
| DRY | Follows DRY | Repetitive code |
| Example | `template<class T> T max(T a, T b)` | `int max(int, int)`, `double max(double, double)` |

**Note:** Exact match takes highest priority. If a non-template function exactly matches, it's called; otherwise the template is instantiated.

---

## Section 7: Abstract Classes, Interfaces, Keywords (Q49–Q54)

---

**Q49. Difference between Abstract Class and Interface?**

**Answer:**

| Feature | Abstract Class | Interface |
|---------|----------------|-----------|
| Methods | Abstract **and** concrete | Only abstract (Java 8+: default/static too) |
| Data members | Can have | Only static and final (Java) |
| Multiple inheritance | Not supported | Supported |
| Constructor | Can have | No constructor |
| Keyword | `abstract` | `interface` |
| Extends/Implements | `extends` | `implements` |
| Abstraction level | 0–100% | 100% |
| Access | private/protected allowed | public by default |

**C++:** There is no separate `interface` keyword. An interface is an abstract class with only pure virtual functions and no data members.

```cpp
// C++ interface
class Drawable {
public:
    virtual void draw() = 0;
    virtual ~Drawable() {}
};
```

---

**Q50. What is the `final` keyword?**

**Answer:** `final` is used to prevent inheritance or overriding.

- **Final variable:** Value cannot be changed (constant).
- **Final method:** Cannot be overridden.
- **Final class:** Cannot be extended.

```cpp
class Base final { };           // cannot be inherited
class A {
public:
    virtual void show() final { }   // cannot be overridden
};
```

**Q: Is a final method inherited?** Yes, inherited, but cannot be overridden.
**Q: Can a constructor be final?** No — a constructor is never inherited.

---

**Q51. What is the `explicit` keyword?**

**Answer:** `explicit` marks constructors so they do **NOT** implicitly convert types. Used for constructors taking exactly one argument (only single-argument constructors are usable for typecasting).

```cpp
// WITHOUT explicit
class Complex {
    double real, imag;
public:
    Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}
    bool operator==(Complex rhs) { return (real == rhs.real && imag == rhs.imag); }
};
int main() {
    Complex com1(3.0, 0.0);
    if (com1 == 3.0) cout << "Same";   // 3.0 implicitly converted
}

// WITH explicit
class Complex {
    double real, imag;
public:
    explicit Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}
    bool operator==(Complex rhs) { return (real == rhs.real && imag == rhs.imag); }
};
int main() {
    Complex com1(3.0, 0.0);
    // if (com1 == 3.0)              // ERROR: no implicit conversion
    if (com1 == (Complex)3.0) cout << "Same";  // OK: explicit cast
}
```

---

**Q52. What is the `const` keyword?**

**Answer:** `const` prevents modification of variables, pointers, and member functions.

**Rules for const variables:**
- Cannot be left uninitialized at declaration.
- Cannot be assigned a value anywhere else.
- Must be given an explicit value at declaration.

```cpp
const int var;         // ✗ Invalid — no value
const int var; var=5;  // ✗ Invalid — assigned separately
const int var = 5;     // ✓ Valid
```

**Const with pointers:**
1. **Pointer to const value:** `const int* ptr;` — can't modify value, can change pointer.
2. **Const pointer:** `int* const ptr;` — can modify value, can't change pointer.
3. **Const pointer to const value:** `const int* const ptr;` — can't modify either.

**Const member function:**
```cpp
void fun() const { }   // cannot modify object's data members
```


**Q54. What is a Namespace?**

**Answer:** A namespace provides a solution for preventing **name conflicts** in large projects. Each entity needs a unique name. A namespace allows for identically named entities as long as the namespaces are different.

```cpp
namespace first { int x = 1; }
namespace second { int x = 2; }

int main() {
    int x = 3;
    cout << x;              // 3 (local)
    cout << second::x;      // 2
    cout << first::x;       // 1
}
```

**`using namespace std;`** — brings all names from `std` into current scope. Used to avoid writing `std::` repeatedly.

---

## Section 8: Exception Handling, Modern Topics (Q55–Q60)

---

**Q55. What is Exception Handling? Types?**

**Answer:** Exceptions are **runtime anomalies** (division by zero, out-of-bounds access, memory exhaustion) that disrupt normal program flow. Exception handling provides a way to detect, report, and handle these gracefully.

**Three keywords:** `try`, `catch`, `throw`.

**Types:**
1. **Synchronous exceptions** — Errors like "out-of-range index", "overflow" — caused by the program.
2. **Asynchronous exceptions** — Errors generated by events beyond program control (disk failure, network issues).

**Mechanism:**
```cpp
try {
    // code that might throw
    if (b == 0) throw b;
    c = a / b;
}
catch (int e) {
    cout << "Division by " << e << endl;
}
```

**Multiple catch blocks:**
```cpp
try { /* ... */ }
catch (int e) { }
catch (char c) { }
catch (double d) { }
catch (...) { }   // catch-all
```

**Rethrowing:**
```cpp
catch (const char*) {
    cout << "Caught inside\n";
    throw;   // rethrow to outer handler
}
```

---

**Q56. What is the difference between Error and Exception?**

**Answer:**

| Error | Exception |
|-------|-----------|
| Serious problem, usually irrecoverable | Abnormal condition, usually recoverable |
| Caused by system/environment | Caused by program |
| Examples: OutOfMemory, StackOverflow | Examples: NullPointer, ArithmeticException |
| Not meant to be caught/handled | Meant to be caught/handled |
| Subclass of `Throwable` (Java) | Subclass of `Throwable` (Java) |

In C++, both are treated similarly via exceptions, but errors like `std::bad_alloc` are also exceptions.

---

**Q57. What is SOLID? Explain each principle.**

**Answer:**

| Principle | Meaning | One-liner |
|-----------|---------|-----------|
| **S** — Single Responsibility | A class should have only one reason to change. | One job per class. |
| **O** — Open/Closed | Open for extension, closed for modification. | Add new code, don't modify old. |
| **L** — Liskov Substitution | Subtypes must be usable in place of base types. | Derived must behave like base. |
| **I** — Interface Segregation | Many small interfaces > one large interface. | Don't force unnecessary methods. |
| **D** — Dependency Inversion | Depend on abstractions, not concrete implementations. | High-level modules shouldn't depend on low-level details. |

**Benefits:** Maintainable, flexible, testable code.

---

**Q58. What is Association, Aggregation, and Composition?**

**Answer:**

| Relationship | Type | Ownership | Lifetime |
|--------------|------|-----------|----------|
| **Association** | "uses-a" | No ownership | Independent |
| **Aggregation** | "has-a" (weak) | Weak ownership | Part can exist independently |
| **Composition** | "has-a" (strong) | Strong ownership | Part cannot exist without whole |

**Examples:**
- **Association:** Teacher — Student (both exist independently).
- **Aggregation:** Team — Player (players can exist without team).
- **Composition:** House — Room (rooms don't exist without house).

**Diagram:**
```
Association:  A ---> B
Aggregation:  A <>-- B   (hollow diamond)
Composition:  A <#>-- B  (filled diamond)
```

---

**Q59. What is a Design Pattern? Name a few.**

**Answer:** A design pattern is a **reusable solution to a common software design problem**. It's not code, but a template for solving a problem.

**Common patterns:**
- **Singleton:** Ensures one instance and global access.
- **Factory:** Creates objects without specifying exact class.
- **Observer:** Notifies dependents of state changes.
- **Strategy:** Defines a family of algorithms, makes them interchangeable.
- **Adapter:** Allows incompatible interfaces to work together.

**Singleton example:**
```cpp
class Singleton {
    static Singleton* instance;
    Singleton() {}
public:
    static Singleton* getInstance() {
        if (!instance) instance = new Singleton();
        return instance;
    }
};
```

---

**Q60. Design a Banking System using OOP principles.**

**Answer:**

```cpp
class Account {
protected:
    string accNo;
    double balance;
public:
    Account(string a, double b) : accNo(a), balance(b) {}
    virtual void deposit(double amt) { balance += amt; }
    virtual bool withdraw(double amt) = 0;   // pure virtual
    virtual ~Account() {}
};

class SavingsAccount : public Account {
    double rate;
public:
    SavingsAccount(string a, double b, double r) : Account(a, b), rate(r) {}
    bool withdraw(double amt) override {
        if (balance - amt < 1000) return false;   // min balance
        balance -= amt; return true;
    }
};

class CurrentAccount : public Account {
    double overdraft;
public:
    CurrentAccount(string a, double b, double o) : Account(a, b), overdraft(o) {}
    bool withdraw(double amt) override {
        if (balance - amt < -overdraft) return false;
        balance -= amt; return true;
    }
};
```

**OOP Principles Used:**
- **Encapsulation:** Private data + public methods.
- **Inheritance:** Base `Account` for common attributes.
- **Polymorphism:** Virtual `withdraw()` for different behavior.
- **Abstraction:** Abstract base class defines contract.
- **Composition:** "Has-a" relationships.

---

## Bonus: Output-Based Questions (Common in Interviews)

**Q. What is the output?**
```cpp
class Base {
public:
    virtual void show() { cout << "In Base\n"; }
};
class Derived : public Base {
public:
    void show() { cout << "In Derived\n"; }
};
int main() {
    Base *bp = new Derived;
    bp->show();
    bp->Base::show();
    return 0;
}
```
**Answer:**
```
In Derived
In Base
```
- `bp->show()` → virtual dispatch → `Derived::show()`.
- `bp->Base::show()` → scope resolution → `Base::show()`, bypasses virtual.

---

**Q. What is the output?**
```cpp
class Base {
public:
    Base() { cout << "Base Constructor\n"; }
    virtual ~Base() { cout << "Base Destructor\n"; }
};
class Derived : public Base {
public:
    Derived() { cout << "Derived Constructor\n"; }
    ~Derived() { cout << "Derived Destructor\n"; }
};
int main() {
    Base *bp = new Derived();
    delete bp;
    return 0;
}
```
**Answer:**
```
Base Constructor
Derived Constructor
Derived Destructor
Base Destructor
```
Since destructor is virtual, derived destructor called first, then base.

---

**Q. What is `sizeof(A)` vs `sizeof(B)`?**
```cpp
class A { public: virtual void fun(); };
class B { public: void fun(); };
```
**Answer:** `sizeof(A) > sizeof(B)` — Class A has a VPTR (typically 8 bytes on 64-bit), Class B doesn't.

---

**Q. Can static functions be virtual?**
```cpp
class Test { public: virtual static void fun() {} };
```
**Answer:** **No — compiler error.** Static functions are class-specific, not called on objects. Virtual functions are resolved per-object. Combining them is contradictory.

---

**Q. `Base *bp = new Derived; bp->fun();` where `B::fun()` overrides `A::fun()`, and `B *bp` (not `A*`) is used.**
```cpp
class A { public: virtual void fun() { cout << "A::fun "; } };
class B : public A { public: void fun() { cout << "B::fun "; } };
class C : public B { public: void fun() { cout << "C::fun "; } };
int main() { B *bp = new C; bp->fun(); }
```
**Answer:** `C::fun()` — `B::fun()` is virtual even without `virtual` keyword (it overrides a virtual base function). All descendant classes' same-signature functions are automatically virtual.

---