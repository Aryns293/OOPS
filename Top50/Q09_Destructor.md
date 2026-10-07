# Q09 Destructor

## 🎯 Interview Answer
A **Destructor** is a special member function that is automatically called when an object is destroyed. It is the exact opposite of a constructor. Its main job is to release any resources (especially dynamically allocated memory, file handles, or network sockets) that the object acquired during its lifetime.

### ⚙️ Key Characteristics
- **Same name** as the class, preceded by a tilde (`~`).
- Takes **no parameters**.
- Has **no return type** (not even `void`).
- **Cannot be overloaded** — a class can have only one destructor.
- **Called automatically**, never explicitly (though you *can* call it explicitly, it’s rarely needed and often dangerous).
- If you don’t define one, the compiler generates a **default destructor** (which does nothing for simple primitive members).

---

## ⚡ When is a Destructor Called?
A destructor is called automatically in these situations:
1. When a local object **goes out of scope** (e.g., function execution ends).
2. When the **program ends** (for global or static objects).
3. When `delete` is called on a dynamically allocated object (`delete obj;` or `delete[] arr;`).
4. When a **temporary object** is destroyed (e.g., after the expression it was created in finishes).

---

## 💻 Code Example

```cpp
class Student {
    int* rollNo;
public:
    Student(int r) {
        rollNo = new int(r);
        cout << "Constructor called for roll " << *rollNo << endl;
    }

    ~Student() {
        cout << "Destructor called for roll " << *rollNo << endl;
        delete rollNo;   // Free dynamically allocated memory
    }
};

int main() {
    Student s1(101);        // Constructor called
    
    {
        Student s2(102);    // Constructor called
    }                       // s2 goes out of scope -> Destructor called for 102

    Student* s3 = new Student(103);  // Constructor called
    delete s3;                       // Destructor called for 103

    return 0;
}   // s1 goes out of scope -> Destructor called for 101
```

### 🖨️ Output:
```text
Constructor called for roll 101
Constructor called for roll 102
Destructor called for roll 102
Constructor called for roll 103
Destructor called for roll 103
Destructor called for roll 101
```

---

## 📊 Diagram: Object Lifecycle

### General Flow
```text
Object Created  --->  Constructor called
      |
      |  (object used)
      v
Object Destroyed --->  Destructor called
```

### Local Object Scope
```text
{                   // Scope begins
    Student s;      // Constructor called
    // ... use s
}                   // Scope ends -> Destructor called
```

### Dynamic Object Lifetime
```text
Student* s = new Student();  // Constructor called
// ... use s
delete s;                    // Destructor called
```

---

## 🎯 Summary to Impress
- **Destructor** = `~ClassName()`, no parameters, no return type.
- **Automatically called** when the object’s lifetime ends.
- **Purpose:** Used to free resources (dynamic memory, file handles, locks, etc.).
- **Uniqueness:** Cannot be overloaded (only one per class).
- **Rule of Three:** If you need a custom destructor, you likely also need a custom copy constructor and copy assignment operator.
- **Polymorphism Note:** For polymorphic base classes, you must make the destructor `virtual` so derived destructors are called correctly.
