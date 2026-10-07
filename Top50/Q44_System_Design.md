# Q44 System Design using OOP

## 🎯 Interview Answer
When designing a system, use core OOP principles to structure the code logically and make it extensible.

### ⚙️ How to apply OOP Principles:
- **Encapsulation**: Use private data members and expose behavior via public methods.
- **Inheritance**: Create a base class to share common attributes and avoid code duplication.
- **Polymorphism**: Use virtual functions to allow different behaviors through a common interface.
- **Abstraction**: Use an abstract base class to define a strict contract for derived classes.
- **Composition**: Use "has-a" relationships to build complex objects out of simpler ones.

---

## 💻 Code Example: Banking System

```cpp
// Abstract Base Class
class Account {
protected:
    string accNo;
    double balance;
public:
    Account(string a, double b) : accNo(a), balance(b) {}
    
    // Concrete method
    virtual void deposit(double amt) { 
        balance += amt; 
    }
    
    // Pure virtual method (forces implementation in derived classes)
    virtual bool withdraw(double amt) = 0;
    
    virtual ~Account() {}
};

// Derived Class 1
class SavingsAccount : public Account {
    double rate;
public:
    SavingsAccount(string a, double b, double r) : Account(a, b), rate(r) {}
    
    bool withdraw(double amt) override {
        if (balance - amt < 1000) return false; // Minimum balance check
        balance -= amt; 
        return true;
    }
};

// Derived Class 2
class CurrentAccount : public Account {
    double overdraft;
public:
    CurrentAccount(string a, double b, double o) : Account(a, b), overdraft(o) {}
    
    bool withdraw(double amt) override {
        if (balance - amt < -overdraft) return false; // Overdraft limit check
        balance -= amt; 
        return true;
    }
};
```

---

## 🎯 Summary to Impress
Use **inheritance** for "is-a" relationships, **composition** for "has-a" relationships, and **virtual functions** for polymorphic behavior. The goal of system design is to create abstractions that are stable, testable, and extensible.
