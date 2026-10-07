# Q07 Copy Constructor

## 🎯 Interview Answer
A **Copy Constructor** is a special constructor that creates a new object as a copy of an existing object of the same class. It takes a reference to an object of the same class as a parameter, usually a `const` reference.

### ⚙️ Syntax
```cpp
ClassName(const ClassName &obj);
```

### ⚡ When is it called?
It is called automatically when:
1. A new object is initialized from another existing object: `Student s2 = s1;`
2. An object is passed by value to a function.
3. An object is returned by value from a function.

---

## ❓ Why must its argument be passed by reference?
If the copy constructor took its argument by **value**, then calling the copy constructor would require making a copy of the argument. This would require calling the copy constructor again, leading to an **infinite recursion** (non-terminating chain of calls). The compiler would never be able to complete the call.

Therefore, it **must** take a reference. We use a `const` reference so that the original object cannot be modified, and to allow copying of `const` objects.

---

## 💻 Code Example

```cpp
class Student {
private:
    int rollNo;
    string name;

public:
    // Parameterized constructor
    Student(int r, string n) {
        rollNo = r;
        name = n;
    }

    // Copy constructor
    Student(const Student &s) {
        rollNo = s.rollNo;
        name = s.name;
        cout << "Copy constructor called" << endl;
    }

    void display() {
        cout << rollNo << " - " << name << endl;
    }
};

int main() {
    Student s1(101, "Alice");
    Student s2 = s1;   // Copy constructor called
    s2.display();
    return 0;
}
```

### 🖨️ Output:
```text
Copy constructor called
101 - Alice
```

---

## 📊 Diagram: Copy Constructor Call

```text
Existing Object s1
+-------------------+
| rollNo = 101      |
| name = "Alice"    |
+-------------------+
          |
          |  Student s2 = s1;
          v
   Copy Constructor
   Student(const Student &s)
          |
          v
New Object s2
+-------------------+
| rollNo = 101      |
| name = "Alice"    |
+-------------------+
```

---

## 💡 Important Points
- **Default Copy Constructor:** If you don’t define one, the compiler generates a default copy constructor that performs a shallow copy (copies member values as-is).
- **Shallow vs Deep Copy:** For classes with pointers/dynamic memory, the default shallow copy can cause problems (double-free, dangling pointers). You need a user-defined deep copy copy constructor.
- **Rule of Three:** If you need a custom destructor, copy constructor, or copy assignment operator, you likely need all three.

---

## 🎯 Summary to Impress
- **Copy constructor** creates a new object from an existing object.
- **Signature:** `ClassName(const ClassName &obj);`
- **Must take reference** to avoid infinite recursion.
- **Called on** initialization, pass-by-value, and return-by-value.
- **Default version** does a shallow copy; a deep copy needs custom implementation.
