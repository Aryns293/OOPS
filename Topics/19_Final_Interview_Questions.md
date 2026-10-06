# TOPIC 19: Final Compiled Interview Questions

*(Note: source numbers these 1,2,4,5,7,8 — questions 3 and 6 are absent from the original notes, not omitted by me.)*

**1. What is Encapsulation? Why "Data hiding"?**
Binding data and corresponding methods (behavior) into a single unit. Binds class members together, prevents access by other classes — keeps them safe from outside interference/misuse. If a field is private, it cannot be accessed from outside the class — hence "data hiding."

**2. Abstraction vs Encapsulation?**

| Abstraction | Encapsulation |
| :--- | :--- |
| Hides unnecessary details, shows necessary ones | Binds data members and methods together to do a job without revealing unnecessary details |
| Achieved through encapsulation | Implemented using Access Modifiers (Public, Protected, Private) |
| Focus on WHAT the object does, not HOW | Hides code/data into a single unit to secure it |
| Problems solved at design/interface level | Problems solved at implementation level |

**4. Limitations of Inheritance?**
Yes — needs more time to process (navigating multiple classes). Base and child classes are tightly coupled — changes may need nested changes in both. Can be complex to implement; incorrect implementation → unexpected errors.

**5. Overloading vs Overriding?**
* **Overloading** = compile-time polymorphism, same name, multiple implementations (method/operator overloading). 
* **Overriding** = runtime polymorphism, same name, implementation changes during execution (method overriding).

**7. Advantages of Polymorphism?**
* Achieves flexibility — perform various operations using same-named methods per requirement
* Main benefit: providing implementation to an abstract base class or interface

**8. Polymorphism vs Inheritance?**
* Inheritance = parent-child relationship between classes; polymorphism leverages that relationship for dynamism
* Inheritance helps reusability by inheriting behavior; polymorphism enables the child to redefine already-defined behavior — without it, a child can't execute its own behavior

## Friend Function (extended coverage)

```cpp
class class_name {
   friend data_type function_name(argument);
};
```

Defined outside the class scope but has rights to access private/protected members — definition doesn't use `friend` keyword or scope resolution operator.

```cpp
class Rectangle {
private: int length;
public:
   Rectangle() { length = 10; }
   friend int printLength(Rectangle);
};

int printLength(Rectangle b) { 
   b.length += 10; 
   return b.length; 
}

int main() { 
   Rectangle b; 
   cout << "Length of Rectangle: " << printLength(b) << endl; 
}
// Output: Length of Rectangle: 20
```

## Final Interview Questions Set

* **Does every virtual function need to be overridden?** No — can be used as-is from base.
* **What is an abstract class?** Class with ≥1 pure virtual function. Cannot instantiate. Can only be inherited; methods can be overridden.
* **Can a constructor be Virtual?** No — must be defined before the object (and its VTABLE) exists.
* **What is a pure virtual function?** A virtual function with no implementation — declared by assigning `0`.
* **Characteristics of Friend Function?** (see list in Topic 7)

**Sample output — Box with friend printWidth:**
```cpp
class Box {
   double width;
public:
   friend void printWidth(Box box);
   void setWidth(double wid) { width = wid; }
};
void printWidth(Box box) { 
   box.width = box.width * 2; 
   cout << "Width of box: " << box.width << endl; 
}
int main() { 
   Box box; 
   box.setWidth(10.0); 
   printWidth(box); 
}
```
**Answer:** 20 (10.0 × 2).

## Closing Analogy on Polymorphism

* Saving 2 numbers under the same phone contact name is like method overloading in Java — a method `number()` can have multiple definitions (`number(int p1, int p2)` and `number(int p1)`), and which executes depends on parameters passed.
* Ice cream parlour analogy: class `Icecream` has `dinshaws()` with only vanilla in one branch; `Branch` extends `Icecream` overrides it to include vanilla + chocolate. Which version runs depends on the object's actual class — Method Overriding in action.

*(Final line in source notes: references an external Whimsical OOP cheatsheet by Love Babbar for a visual summary — not reproduced here as it's an external resource link, not content of this PDF.)*
