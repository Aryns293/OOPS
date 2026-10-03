# Q27 Static Data Member

**Interview Answer:**
A static data member is a class member that is shared by all objects of the class. Only one copy exists, regardless of how many objects are created.

Key points:

Declared inside class with static.

Defined outside class: int ClassName::count = 0;

Initialized before any object is created (even before main()).

Used for properties common to all objects (e.g., rateOfInterest, companyName) or as a counter.

Code:

cpp
class Student {
    static int count;  // declaration
public:
    Student() { count++; }
    static int getCount() { return count; }
};

int Student::count = 0;  // definition

int main() {
    Student s1, s2;
    cout << Student::getCount();  // 2
}
Summary: Static data members are class-level variables, shared across all instances.
