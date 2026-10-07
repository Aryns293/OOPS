# Q30 Copy Assignment Operator

## 🎯 Interview Answer
The **copy assignment operator** (`operator=`) is called when assigning the value of one object to another **already existing** object (e.g., `obj1 = obj2;`). It is different from the copy constructor, which creates a *new* object from an existing one.

### 📜 Rule of Three
If a class needs a custom **destructor**, **copy constructor**, or **copy assignment operator**, it likely needs all three. This is because all three are typically required to correctly manage a shared resource (such as dynamically allocated memory).

---

## 💻 Code Example

```cpp
class Student {
    int* rollNo;
public:
    Student(int r) { 
        rollNo = new int(r); 
    }
    
    // Destructor
    ~Student() { 
        delete rollNo; 
    }                     
    
    // Copy Constructor
    Student(const Student& s) {                       
        rollNo = new int(*(s.rollNo));
    }
    
    // Copy Assignment Operator
    Student& operator=(const Student& s) {            
        if (this != &s) {                             // Self-assignment check
            delete rollNo;                            // Clean up existing resource
            rollNo = new int(*(s.rollNo));            // Allocate and copy new resource
        }
        return *this;                                 // Return reference for chaining (a = b = c)
    }
};
```

---

## 🎯 Summary to Impress
The **Rule of Three** ensures proper deep copying and resource management. The copy assignment operator handles assignment to an already existing object, and must always check for self-assignment (`this != &s`) before modifying internal resources.
