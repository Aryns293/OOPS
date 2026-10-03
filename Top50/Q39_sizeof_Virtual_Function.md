# Q39 sizeof Virtual Function

**Interview Answer:**
When a class has at least one virtual function, the compiler inserts a hidden VPTR (Virtual Pointer) into every object of that class. This increases the size of the object.

On a 64-bit system, VPTR is typically 8 bytes.

A class without virtual functions has no VPTR.

Code:

cpp
class A { int x; };            // sizeof(A) = 4 (int)
class B { int x; virtual void f() {} };  // sizeof(B) = 16 (int + padding + VPTR)
Summary: Virtual functions add a hidden VPTR, increasing object size.
