# Q35 Pure Virtual Function

## 🎯 Interview Answer
A **pure virtual function** is a virtual function declared by assigning it `= 0` in its declaration. It typically has no implementation in the base class. 

Any class that contains at least one pure virtual function becomes an **abstract class**. An abstract class cannot be instantiated directly — it can only be inherited from.

---

## 💻 Code Example

```cpp
class Shape {
public:
    virtual double area() = 0;  // pure virtual function
    virtual ~Shape() {}
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    
    // Derived class must implement the pure virtual function
    double area() override { 
        return 3.14 * r * r; 
    }
};

int main() {
    // Shape s;                // ERROR: Cannot instantiate abstract class
    Shape* s = new Circle(5);  // OK: Pointer to base class holding derived object
}
```

---

## 🎯 Summary to Impress
Pure virtual functions define a **strict contract or interface**. Derived classes are forced to implement these functions; if they don't, they also become abstract classes and cannot be instantiated.
