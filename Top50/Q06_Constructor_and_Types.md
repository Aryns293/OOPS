# Q06 Constructor and Types

**Interview Answer:**
A Constructor is a special member function that is automatically called when an object is created. It has the same name as the class, no return type (not even void), and is used to initialize the data members of the new object. Constructors ensure that an object starts its life in a valid state.

Key Characteristics
Same name as the class.

No return type.

Called automatically at object creation.

Can be overloaded.

Cannot be virtual.

If you don’t define any constructor, the compiler generates a default constructor (which does nothing or leaves members with garbage values).

Types of Constructors
1. Default Constructor
Takes no arguments. If you don’t define any constructor, the compiler provides an empty one.

cpp
class Student {
    int rollNo;
public:
    Student() {          // Default constructor
        rollNo = 0;
    }
};
2. Parameterized Constructor
Takes arguments to initialize objects with specific values.

cpp
class Student {
    int rollNo;
    string name;
public:
    Student(int r, string n) {   // Parameterized constructor
        rollNo = r;
        name = n;
    }
};
Usage:

cpp
Student s1(101, "Alice");   // Calls parameterized constructor
3. Copy Constructor
Takes an object of the same class by reference as an argument and copies its data members into the new object.

cpp
class Student {
    int rollNo;
public:
    Student(int r) { rollNo = r; }
    Student(const Student &s) {   // Copy constructor
        rollNo = s.rollNo;
    }
};
Usage:

cpp
Student s1(101);
Student s2 = s1;    // Calls copy constructor
Diagram: Object Creation and Constructor Call
text
Class Student
+---------------------+
| - rollNo: int       |
| - name: string      |
+---------------------+
| + Student()         |  <-- Default constructor
| + Student(int,string)| <-- Parameterized
| + Student(Student&) |  <-- Copy constructor
+---------------------+
          |
          |  When object is created:
          v
Student s1(101, "Alice");   --> Parameterized constructor called
Student s2 = s1;            --> Copy constructor called
Student s3;                 --> Default constructor called
Constructor Overloading (Bonus)
Having multiple constructors with different parameters is called constructor overloading. The compiler chooses the right one based on the arguments passed.

cpp
class Complex {
    double real, imag;
public:
    Complex() { real = imag = 0; }                     // Default
    Complex(double r) { real = r; imag = 0; }          // Parameterized (1 arg)
    Complex(double r, double i) { real = r; imag = i; }// Parameterized (2 args)
};
Summary to impress:

Constructor = special member function, same name as class, no return type.

Called automatically when object is created.

Types: Default, Parameterized, Copy.

If no constructor is defined, compiler provides a default one.

Constructors can be overloaded.

They ensure objects are properly initialized.
