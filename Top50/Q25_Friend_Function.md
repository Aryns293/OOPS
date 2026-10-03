# Q25 Friend Function

**Interview Answer:**
A friend function is a non-member function that is granted access to the private and protected members of a class. It is declared inside the class with the friend keyword, but defined outside.

Characteristics:

Not in the scope of the class.

Cannot be called using an object (obj.friendFunc() is invalid).

Invoked like a normal function.

Can be a global function or a member of another class.

Violates encapsulation (C++ is not pure OOP because of this).

Code:

cpp
class Box {
private:
    int length;
public:
    Box(int l) : length(l) {}
    friend void printLength(Box b);  // friend declaration
};

void printLength(Box b) {
    cout << b.length;  // can access private
}
Summary: Friend functions are useful for operator overloading (like <<) and when two classes need to share internals.
