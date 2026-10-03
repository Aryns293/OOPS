# Q40 Output of Virtual Dispatch

**Interview Answer:**
Given:

cpp
class Base {
public:
    virtual void show() { cout << "In Base\n"; }
};
class Derived : public Base {
public:
    void show() { cout << "In Derived\n"; }
};
int main() {
    Base *bp = new Derived;
    bp->show();
    bp->Base::show();
    return 0;
}
Output:

text
In Derived
In Base
Explanation:

bp->show() uses virtual dispatch → calls Derived::show() because the object is Derived.

bp->Base::show() uses scope resolution → explicitly calls Base::show(), bypassing the virtual mechanism.

Summary: Virtual call uses actual object type; scope resolution forces base version.
