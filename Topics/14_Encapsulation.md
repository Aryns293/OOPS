# TOPIC 14: Encapsulation

Binding code and data into a single unit. To restrict outside access, data members are made private.

* Bundles data and the methods that operate on it into a single unit
* A class is the primary example
* Restricts direct access to some components of an object
* Hides both data members and functions/methods
* Encapsulation = Data hiding + Abstraction
* Wraps data/methods into a class, protecting from outside intervention

We can create a fully encapsulated class by making all data members private, using setter/getter methods for access.

```cpp
class Student {
private:
   string studentName; 
   int studentRollno; 
   int studentAge;
public:
   string getStudentName() { return studentName; }
   void setStudentName(string studentName) { this->studentName = studentName; }
   int getStudentRollno() { return studentRollno; }
   void setStudentRollno(int studentRollno) { this->studentRollno = studentRollno; }
   int getStudentAge() { return studentAge; }
   void setStudentAge(int studentAge) { this->studentAge = studentAge; }
};

int main() {
   Student obj;
   obj.setStudentName("Avinash"); 
   obj.setStudentRollno(101); 
   obj.setStudentAge(22);
   
   cout << "Student Name: " << obj.getStudentName() << endl;
   cout << "Student Rollno: " << obj.getStudentRollno() << endl;
   cout << "Student Age: " << obj.getStudentAge();
}
// Output: Student Name: Avinash / Student Rollno: 101 / Student Age: 22
```

How is Encapsulation achieved? Using access modifiers.

## Advantages:

* Providing only a setter OR getter makes a class read-only or write-only
* Control over data — e.g., setter logic can reject id ≤ 100 or negative numbers
* Achieves data hiding — other classes can't access private data directly
* Encapsulated classes are easy to unit test

## How Encapsulation is achieved in a class:

* Make all data members private
* Create public setter/getter functions for each — set functions assign the value, get functions retrieve it

## Self-study questions posed (unanswered in source):
* Can we achieve encapsulation using the public access modifier?
* How is encapsulation achieved in a class, with example?
* Can we achieve encapsulation without data hiding?
