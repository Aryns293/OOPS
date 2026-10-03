# Q28 Static Member Function

**Interview Answer:**
A static member function is a function declared with static inside a class. It works for the class as a whole, not for a specific object.

Key points:

Called using class name: ClassName::func().

Can be called without creating an object.

Can access only static data members and static member functions.

Has no this pointer.

Cannot be virtual.

Code:

cpp
class Math {
    static int count;
public:
    static int add(int a, int b) { return a + b; }
    static void increment() { count++; }
};
int Math::count = 0;

int main() {
    cout << Math::add(2, 3);  // 5
}
Summary: Static member functions are class-level utilities; no object needed.
