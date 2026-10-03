# Q09 Destructor

**Interview Answer:**
A Destructor is a special member function that is automatically called when an object is destroyed. It is the opposite of a constructor. Its main job is to release any resources (especially dynamically allocated memory) that the object acquired during its lifetime.

Key Characteristics
Same name as the class, preceded by a tilde (~).

Takes no parameters.

Has no return type (not even void).

Cannot be overloaded — a class can have only one destructor.

Called automatically, never explicitly (though you can call it explicitly, but it’s rarely needed).

If you don’t define one, the compiler generates a default destructor (which does nothing for simple members).

When is a Destructor Called?
A destructor is called automatically in these situations:

When the object goes out of scope (e.g., local variable in a function ends).

When the program ends (for global or static objects).

When delete is called on a dynamically allocated object (delete obj; or delete[] arr;).

When a temporary object is destroyed (e.g., after an expression).

Code Example
cpp
class Student {
    int* rollNo;
public:
    Student(int r) {
        rollNo = new int(r);
        cout << "Constructor called for roll " << *rollNo << endl;
    }

    ~Student() {
        cout << "Destructor called for roll " << *rollNo << endl;
        delete rollNo;   // Free dynamically allocated memory
    }
};

int main() {
    Student s1(101);        // Constructor
    {
        Student s2(102);    // Constructor
    }                       // s2 goes out of scope -> Destructor called for 102

    Student* s3 = new Student(103);  // Constructor
    delete s3;                       // Destructor called for 103

    return 0;
}   // s1 goes out of scope -> Destructor called for 101
Output:

text
Constructor called for roll 101
Constructor called for roll 102
Destructor called for roll 102
Constructor called for roll 103
Destructor called for roll 103
Destructor called for roll 101
Diagram: Object Lifecycle
text
Object Created  --->  Constructor called
      |
      |  (object used)
      v
Object Destroyed --->  Destructor called
For a local object:

text
{                   // Scope begins
    Student s;      // Constructor
    // ... use s
}                   // Scope ends -> Destructor
For dynamic object:

text
Student* s = new Student();  // Constructor
// ... use s
delete s;                     // Destructor
Summary to Impress
Destructor = ~ClassName(), no parameters, no return type.

Called automatically when object’s lifetime ends.

Used to free resources (dynamic memory, file handles, locks, etc.).

Cannot be overloaded.

Rule of Three: If you need a custom destructor, you likely also need a custom copy constructor and copy assignment operator.

For polymorphic base classes, make the destructor virtual so derived destructors are called correctly.
