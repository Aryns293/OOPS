# Q43 Design Patterns

**Interview Answer:**
A design pattern is a reusable solution to a common software design problem.

Common patterns:

Singleton: Ensures one instance and global access.

Factory: Creates objects without specifying exact class.

Observer: Notifies dependents of state changes.

Strategy: Defines a family of algorithms, makes them interchangeable.

Code (Singleton):

cpp
class Singleton {
    static Singleton* instance;
    Singleton() {}
public:
    static Singleton* getInstance() {
        if (!instance) instance = new Singleton();
        return instance;
    }
};
Summary: Patterns provide proven solutions; know the common ones.
