# Q14 Modes of Inheritance

## 🎯 Interview Answer
In C++, inheritance modes determine how the members of the base class are accessed in the derived class. There are three modes: `public`, `protected`, and `private`.

---

## 🏗️ The 3 Modes of Inheritance

### 1️⃣ Public Inheritance
- **Public members** of base → remain `public` in derived.
- **Protected members** of base → remain `protected` in derived.
- **Private members** of base → **never accessible directly** in derived (but can be accessed via public/protected base methods).
- **Represents:** An “is-a” relationship. This is the most common and intuitive form.

```cpp
class Base {
public:    int a;
protected: int b;
private:   int c;
};

class Derived : public Base {
    // a is public
    // b is protected
    // c is NOT accessible
};
```

### 2️⃣ Protected Inheritance
- **Public and protected members** of base → become `protected` in derived.
- **Private members** → still not accessible.
- **Used when:** You want to restrict access to derived classes only (outside world cannot access inherited members).

```cpp
class Derived : protected Base {
    // a is protected
    // b is protected
    // c is NOT accessible
};
```

### 3️⃣ Private Inheritance
- **Public and protected members** of base → become `private` in derived.
- **Private members** → still not accessible.
- **Represents:** An “implemented-in-terms-of” relationship. The derived class uses the base class internally but does not expose its interface. *Composition is usually preferred over private inheritance.*

```cpp
class Derived : private Base {
    // a is private
    // b is private
    // c is NOT accessible
};
```

---

## 📊 Summary Table: Base Member Access in Derived Class

| Base Member Access | `public` Inheritance | `protected` Inheritance | `private` Inheritance |
|--------------------|----------------------|-------------------------|-----------------------|
| **`public`**       | `public`             | `protected`             | `private`             |
| **`protected`**    | `protected`          | `protected`             | `private`             |
| **`private`**      | *Not accessible*     | *Not accessible*        | *Not accessible*      |

---

## 💡 Default Inheritance Mode
- For a `class`, default inheritance is **private**.
- For a `struct`, default inheritance is **public**.

```cpp
class Derived1 : Base { };        // private inheritance by default
struct Derived2 : Base { };       // public inheritance by default
```

---

## 💻 Code Example

```cpp
class Vehicle {
public:
    void fuel() { cout << "Fueling\n"; }
protected:
    int speed;
private:
    int vin;
};

// Public inheritance
class Car : public Vehicle {
public:
    void setSpeed(int s) { 
        speed = s;  // OK: protected is accessible in derived class
    }  
    // vin is NOT accessible
};

int main() {
    Car c;
    c.fuel();        // OK: public in base -> public in derived
    // c.speed = 10; // ERROR: speed is protected, cannot access from main()
    return 0;
}
```

---

## 🎯 Summary to Impress
- **Three modes:** `public`, `protected`, `private`. They change the access level of inherited base members in the derived class.
- **Private members** of the base class always remain **inaccessible** in the derived class, regardless of the inheritance mode.
- **Default mode:** `class` is `private`, `struct` is `public`.
- **Best Practices:** Use `public` for “is-a” relationships. Use **composition** instead of `private` inheritance for “has-a” / "implemented-in-terms-of" relationships.
