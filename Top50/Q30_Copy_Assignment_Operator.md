# Q30 Copy Assignment Operator

**Interview Answer:**
The copy assignment operator (operator=) is called when assigning to an already existing object: obj1 = obj2;. It is different from the copy constructor, which creates a new object.

Rule of Three: If a class needs a custom destructor, copy constructor, or copy assignment operator, it likely needs all three. This is because they all manage the same resource (e.g., dynamic memory).

Code:

cpp
class Student {
    int* rollNo;
public:
    Student(int r) { rollNo = new int(r); }
    ~Student() { delete rollNo; }                     // destructor
    Student(const Student& s) {                       // copy constructor
        rollNo = new int(*(s.rollNo));
    }
    Student& operator=(const Student& s) {            // copy assignment
        if (this != &s) {                             // self-assignment check
            delete rollNo;
            rollNo = new int(*(s.rollNo));
        }
        return *this;
    }
};
Summary: Rule of Three ensures proper deep copying and resource management.
