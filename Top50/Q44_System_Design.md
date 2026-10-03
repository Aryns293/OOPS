# Q44 System Design

**Interview Answer:**
Use OOP principles:

Encapsulation: Private data + public methods.

Inheritance: Base class for common attributes.

Polymorphism: Virtual functions for different behavior.

Abstraction: Abstract base class defines contract.

Composition: “Has-a” relationships.

Example: Banking System

cpp
class Account {
protected:
    string accNo;
    double balance;
public:
    Account(string a, double b) : accNo(a), balance(b) {}
    virtual void deposit(double amt) { balance += amt; }
    virtual bool withdraw(double amt) = 0;
    virtual ~Account() {}
};

class SavingsAccount : public Account {
    double rate;
public:
    SavingsAccount(string a, double b, double r) : Account(a, b), rate(r) {}
    bool withdraw(double amt) override {
        if (balance - amt < 1000) return false;
        balance -= amt; return true;
    }
};

class CurrentAccount : public Account {
    double overdraft;
public:
    CurrentAccount(string a, double b, double o) : Account(a, b), overdraft(o) {}
    bool withdraw(double amt) override {
        if (balance - amt < -overdraft) return false;
        balance -= amt; return true;
    }
};
Summary: Use inheritance for “is-a”, composition for “has-a”, virtual functions for polymorphic behavior. Design abstractions that are stable and extensible.
