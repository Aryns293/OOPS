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

* `Test t;` → compiler error (can't stack-construct)
* `Test* t;` → fine (just a pointer, nothing constructed)
* `Test* t = new Test;` → fine (dynamic allocation, programmer's responsibility to delete)
* Only dynamic objects can be created if the destructor is private
* A friend function, or a class method like `void destruct() { delete this; }`, can be used to trigger a private destructor

## Interview Q&A
* **Does the compiler create a default constructor when we write our own?** — No.
* **Explain constructor** — special member function, auto-called, initializes data members.
* **What is constructor overloading?** — multiple constructors, different parameters.
* **Explain destructor** — opposite of constructor, frees resources.
* **What is a copy constructor?** — copies one object's members into another.
* **How many types of constructors?** — 3 (Default, Parameterized, Copy).
* **When should destructor use delete?** — when the object used new.
* **Return type of constructor/destructor?** — none, not even void.
