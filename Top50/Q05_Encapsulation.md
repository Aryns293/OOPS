# Q05 Encapsulation

## 🎯 Interview Answer
**Encapsulation** is the process of binding data and the methods that operate on that data into a single unit (a class) and hiding the internal state from outside interference. 

In practice, we achieve this by making data members `private` and providing `public` getter and setter methods for controlled access. This protects the data from unintended modifications and allows us to enforce validation rules.

---

## ❓ Why Encapsulation?
- **Data Hiding:** The internal state is not directly accessible from the outside.
- **Security:** Only authorized methods can change the data.
- **Validation:** Setters can check values before assigning them (e.g., rejecting a negative age).
- **Maintainability:** Internal implementation can change without affecting external code.
- **Modularity:** Each class is a self-contained capsule.

---

## 💻 Code Example (C++)

```cpp
class Student {
private:
    string name;
    int rollNo;
    int age;

public:
    // Setter with validation
    void setAge(int a) {
        if (a > 0 && a < 100)
            age = a;
        else
            cout << "Invalid age!" << endl;
    }

    // Getter
    int getAge() { return age; }

    void setName(string n) { name = n; }
    string getName() { return name; }

    void setRollNo(int r) { rollNo = r; }
    int getRollNo() { return rollNo; }
};

int main() {
    Student s;
    s.setName("Alice");
    s.setRollNo(101);
    s.setAge(20);        // Valid
    s.setAge(-5);        // Invalid age! (rejected)
    
    cout << s.getName() << " is " << s.getAge() << " years old.";
    return 0;
}
```
> **Note:** Here, `name`, `rollNo`, and `age` are private. External code cannot do `s.age = -5;` directly. It must go through `setAge()`, which validates the input. This is encapsulation.

---

## 📊 Diagram: Encapsulation as a Capsule

```text
        Class Student (Capsule)
   +--------------------------------+
   |  Private Data:                 |
   |    - name                      |
   |    - rollNo                    |
   |    - age                       |
   +--------------------------------+
   |  Public Methods:               |
   |    + setName()                 |
   |    + getName()                 |
   |    + setAge()  -> validates    |
   |    + getAge()                  |
   +--------------------------------+
                |
                |  Controlled access
                v
        Outside code can only call public methods
```

---

## ⚖️ Encapsulation vs. Abstraction (Quick Note)
- **Encapsulation** is about *how we protect data* (bundling + access control).
- **Abstraction** is about *what we expose* (hiding complexity).
- They are complementary concepts.

---

## 🎯 Summary to Impress
- **Encapsulation** = Data + Methods in one unit + Private data + Public controlled access.
- Achieved via `private` members and `public` getters/setters.
- **Benefits:** Security, Validation, Maintainability, Modularity.
- Prevents unintended modifications and enforces invariants. It’s the foundation of robust class design.
