# Q26 this Pointer

**Interview Answer:**
The this pointer is an implicit pointer available only inside non-static member functions. It points to the current object that invoked the member function.

Uses:

Resolve name conflicts: this->x = x;

Return the current object: return *this;

Pass the current object as a parameter.

Not available in:

Static member functions (no object).

Friend functions (not members).

Code:

cpp
class Student {
    string name;
public:
    void setName(string name) {
        this->name = name;  // this distinguishes member from parameter
    }
};
Summary: this is a hidden pointer to the invoking object; essential for chaining and disambiguation.
