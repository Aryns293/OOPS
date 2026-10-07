# Q27 Static Data Member

## 🎯 Interview Answer
A **static data member** is a class-level member that is shared by all objects of the class. Only one single copy exists in memory, regardless of how many objects of that class are created.

### ⚙️ Key Points:
- **Declaration**: Declared inside the class with the `static` keyword.
- **Definition**: Defined outside the class (e.g., `int ClassName::count = 0;`).
- **Initialization**: Initialized before any object is created (even before `main()` executes).
- **Usage**: Used for properties that are common to all objects (e.g., `rateOfInterest`, `companyName`) or as an object instance counter.

---

## 💻 Code Example

```cpp
class Student {
    static int count;  // declaration inside class
public:
    Student() { 
        count++; 
    }
    
    static int getCount() { 
        return count; 
    }
};

// definition outside class
int Student::count = 0;  

int main() {
    Student s1, s2;
    cout << Student::getCount();  // Output: 2
}
```

---

## 🎯 Summary to Impress
Static data members are **class-level variables** that are shared across all instances of a class. They belong to the class itself rather than to any specific object.
