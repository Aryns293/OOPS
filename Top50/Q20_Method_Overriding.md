# Q20 Method Overriding

## 🎯 Interview Answer
**Method Overriding** is a feature in OOP where a derived class redefines a method of its base class with the **same function name and parameter list, with the same or a covariant return type**. It is used to achieve runtime polymorphism. When a method is called through a base class pointer or reference, the derived class version is executed based on the actual object type at runtime.

---

## 📜 Rules for Method Overriding in C++

1. **Inheritance required** — overriding occurs between a base and derived class.
2. **Same name and parameter list** — the return type must be the same or covariant.
3. **Base function must be virtual** for runtime overriding/dynamic dispatch. Without `virtual`, it’s just function hiding, not overriding.
4. **Access specifier can differ**; access control does not prevent overriding.
5. **Static functions cannot be overridden** because static functions cannot be virtual.
6. **Constructors cannot be overridden or virtual**.
7. **Destructors can be virtual**; a virtual base destructor is important when deleting derived objects through a base pointer.
8. **Use `override`** to let the compiler verify that you are actually overriding a virtual function.

---

## 💻 Code Example

```cpp
class Animal {
public:
    virtual void sound() {          // virtual function
        cout << "Animal makes a sound\n";
    }
    virtual ~Animal() {}            // virtual base destructor (important!)
};

class Dog : public Animal {
public:
    void sound() override {         // override keyword
        cout << "Dog barks\n";
    }
};

class Cat : public Animal {
public:
    void sound() override {
        cout << "Cat meows\n";
    }
};

int main() {
    Animal* a1 = new Dog();
    Animal* a2 = new Cat();

    a1->sound();   // Output: Dog barks
    a2->sound();   // Output: Cat meows

    delete a1;
    delete a2;
    return 0;
}
```
> **Note:** Here, `sound()` is called through `Animal*` pointers, but the derived versions execute because of runtime polymorphism (dynamic dispatch). 

*(Note on object slicing: If you call a virtual function through a base **object** rather than a pointer/reference—e.g., `Animal a = Dog(); a.sound();`—it will call `Animal::sound()` because the object was sliced down to an `Animal`.)*

---

## 📊 Diagram: Runtime Polymorphism via Overriding

```text
        Animal (base)
        virtual sound()
           ^
           |
   +-------+-------+
   |               |
  Dog             Cat
override sound()  override sound()

Animal* a = new Dog();
a->sound();  --> Dog::sound()  (resolved at runtime via VTABLE)
```

---

## ⚖️ Overriding vs Overloading (Quick Note)

| Feature | Overriding | Overloading |
|---------|------------|-------------|
| **Where** | Base + derived relationship | Multiple functions with same name but different parameter lists |
| **Binding** | Runtime | Compile-time |
| **Parameters** | Same | Different |
| **Virtual** | Required for runtime overriding | Not required |
| **Purpose** | Specialized derived behavior | Multiple ways to call same operation |

---

## 💡 Key Points to Impress
- Overriding = derived class provides a new implementation of a virtual base-class function.
- Enables runtime polymorphism/dynamic dispatch.
- Base function must be virtual for virtual dispatch.
- Use `override` to catch signature mistakes.
- Access modifiers do not determine whether overriding occurs.
- Static functions and constructors cannot be overridden.
- A virtual base destructor is important for polymorphic base classes.
- C++ implementations typically use mechanisms such as vtable/vptr for virtual dispatch.

---

## 🎯 Summary to Impress
- Method overriding lets derived classes provide specific behavior for a base class method.
- **Rules:** same signature, base method virtual, inheritance required.
- Achieves **dynamic dispatch** at runtime.
- Use `override` for safety.
- Essential for flexible, extensible OOP design.
