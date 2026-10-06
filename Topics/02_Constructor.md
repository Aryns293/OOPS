# TOPIC 2: Constructor

A constructor is a special member function automatically called when an object is created. No return type, same name as the class, used to initialize data members.

* Must be in the public section. The constructor must be placed in the public section of the class because we want the class to be instantiated anywhere.
* Called only once per object, at creation
* Can be overloaded
* Cannot be virtual — the virtual mechanism needs a VTABLE, which doesn't exist yet when the constructor runs (no object exists yet). Virtual destructor IS possible, though.
* Cannot be inherited
* Address of constructor cannot be referred
* Makes implicit calls to new/delete during memory allocation
* Usually public, though can be private

## 3 Types

### 1. Default Constructor
No arguments/parameters.

* If you don't define one, the compiler auto-generates an empty default constructor (garbage values for members).
* If you define a parameterized constructor, the compiler will NOT implicitly call/generate a default one — `Student s;` will error.
* **Note 1:** defining any constructor other than a copy constructor removes the compiler's default constructor (but the default copy constructor remains).
* **Note 2:** defining a copy constructor removes BOTH the default constructor and default copy constructor.

### 2. Parameterized Constructor
Takes arguments to initialize objects with different values.

### 3. Copy Constructor
Takes an object (by reference) as an argument, copies its data members into another object ("member-wise initialization" / "copy initialization"). If not user-defined, the compiler creates one that does a shallow, member-wise copy.

```cpp
class class_name{
   int data_member1; string data_member2;
public:
   class_name(class_name &obj){
     data_member1 = obj.data_member1;
     data_member2 = obj.data_member2;
   }
};
```

* User-defined copy constructor is needed only if an object has pointers or runtime-allocated resources (file handle, network connection, etc.).
* Default constructor only does shallow copy; deep copy is only possible with a user-defined copy constructor.

### Copy Constructor vs Assignment Operator:

```cpp
MyClass t1, t2;
MyClass t3 = t1;  // (1) copy constructor
t2 = t1;          // (2) assignment operator
```

* Copy constructor makes new memory storage every time; assignment operator does not.

### Frequently Asked Questions

**Can copy constructor be private?**
Yes — makes the class non-copyable, useful when the class holds pointers/dynamic resources, catching mistakes at compile time.

**Why must the argument be passed by reference?**
If passed by value, calling the copy constructor would itself require calling the copy constructor — infinite non-terminating chain.

**Why should the argument be const?**
So objects aren't accidentally modified — general good practice.

## Constructor Overloading
Multiple constructors, same class name, different parameters — differ by number/type of arguments.
