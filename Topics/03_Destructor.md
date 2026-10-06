# TOPIC 3: Destructor

Opposite of constructor — destroys the object, freeing acquired resources.

```cpp
~class_name() { }
```

Name matches class exactly, begins with `~`.

## When called automatically:

* Object goes out of scope
* Program ends
* A scope `{}` containing a local variable ends
* `delete` operator called

**Note:** heap-allocated (`new`) objects need `delete` to trigger the destructor; statically created objects get it automatically.

## Rules
* Name begins with `~`, matches class name
* Only ONE destructor per class (no overloading)
* Takes NO parameters
* No return type, not even `void`
* Should be public
* Address cannot be accessed
* Compiler generates a default one if not specified
* Cannot be static or const
* Default works fine unless the class has dynamically allocated memory/pointers — then a custom destructor must release that memory to avoid leaks

## Private Destructor

Used to control destruction of objects — e.g., preventing dangling references when a pointer is passed to a function that deletes the object.

In the case where the destructor is declared private, an instance of the class can also be created using the `malloc()` function.

### Examples of Private Destructors

**1. Class with private destructor and pointer only (no instance)**

```cpp
// Private Destructor
#include <iostream>
using namespace std;
class Test {
private:
    ~Test() {}
};
int main() { Test* t; }
```
*The above program works fine. There is no object being constructed, the program just creates a pointer of type `Test`, so nothing is destructed.*

**2. Dynamic allocation with private destructor**

```cpp
// Private Destructor
#include <iostream>
using namespace std;
class Test {
private:
    ~Test() {}
};
int main() { Test* t = new Test; }
```
*The above program also works fine. When something is created using dynamic memory allocation, it is the programmer's responsibility to delete it. So, compiler doesn't bother.*

**3. Friend function deletes private destructor**

```cpp
// Private Destructor
#include <iostream>

// A class with private destructor
class Test {
private:
    ~Test() {}
public:
    friend void destructTest(Test*);
};

// Only this function can destruct objects of Test
void destructTest(Test* ptr) { delete ptr; }

int main()
{
    // create an object
    Test* ptr = new Test;
    // destruct the object
    destructTest(ptr);
    return 0;
}
```

**4. Class instance method private destructor**

```cpp
#include <iostream>
using namespace std;

class parent {
    // private destructor
    ~parent() { cout << "destructor called" << endl; }
public:
    parent() { cout << "constructor called" << endl; }
    void destruct() { delete this; }
};

int main()
{
    parent* p;
    p = new parent;
    // destructor called
    p->destruct();
    return 0;
}
```
## Interview Q&A
* **Does the compiler create a default constructor when we write our own?** — No.
* **Explain constructor** — special member function, auto-called, initializes data members.
* **What is constructor overloading?** — multiple constructors, different parameters.
* **Explain destructor** — opposite of constructor, frees resources.
* **What is a copy constructor?** — copies one object's members into another.
* **How many types of constructors?** — 3 (Default, Parameterized, Copy).
* **When should destructor use delete?** — when the object used new.
* **Return type of constructor/destructor?** — none, not even void.
