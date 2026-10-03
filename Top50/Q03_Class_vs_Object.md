# Q03 Class vs Object

**Interview Answer:**
A Class is a user-defined blueprint or template from which objects are created. It is a logical entity — it defines the structure (data members) and behavior (member functions), but no memory is allocated when a class is declared. It’s like an architectural drawing of a house.

An Object is an instance of a class. It is a real-world entity with physical existence — memory is allocated when an object is created. It has its own state (values of data members) and behavior (methods). It’s like the actual house built from the drawing.

Key Differences
Feature	Class	Object
Definition	Blueprint / Template	Instance of a class
Existence	Logical entity	Physical entity
Memory	Not allocated when declared	Allocated when created
Quantity	Declared once	Many objects can be created
Data values	No specific values (non-static)	Holds specific values
Example	class Student { ... };	Student s1, s2;
Code Example (C++)
cpp
class Student {
public:
    string name;
    int rollNo;

    void display() {
        cout << name << " - " << rollNo << endl;
    }
};

int main() {
    Student s1;          // Object created → memory allocated
    s1.name = "Alice";
    s1.rollNo = 101;
    s1.display();

    Student s2;          // Another object
    s2.name = "Bob";
    s2.rollNo = 102;
    s2.display();

    return 0;
}
Here, Student is the class (blueprint).
s1 and s2 are objects (instances) — each has its own copy of name and rollNo.

Simple Diagram
text
Class Student (Blueprint)
+----------------+
| name: string   |
| rollNo: int    |
+----------------+
| display()      |
+----------------+
        |
        |  creates
        v
Object s1 (Instance)        Object s2 (Instance)
+----------------+          +----------------+
| name = "Alice" |          | name = "Bob"   |
| rollNo = 101   |          | rollNo = 102   |
+----------------+          +----------------+
Summary to impress:

Class = Design / Blueprint / Logical.

Object = Realization / Instance / Physical.

Class defines what and how; Object holds actual values and performs actions.

One class → many objects. Memory is allocated only when objects are created.
