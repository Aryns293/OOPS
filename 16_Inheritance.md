# TOPIC 16: Inheritance

Mechanism where one object acquires all properties/behaviors of a parent object — reuses existing class methods/fields, can add new ones.

**Terms:** Class, Sub Class/Child Class (derived/extended class), Super Class/Parent Class (base class), Reusability.

```java
class Subclass-name extends Superclass-name { }
```

## Types of Inheritance in Java (class-based): Single, Multilevel, Hierarchical

**Diagram:**
* **Single:** ClassA ← ClassB
* **Multilevel:** ClassA ← ClassB ← ClassC
* **Hierarchical:** ClassA ← ClassB, ClassA ← ClassC
* **Multiple:** ClassC ← ClassA, ClassC ← ClassB
* **Hybrid:** ClassA ← ClassB, ClassA ← ClassC, then ClassD ← ClassB, ClassD ← ClassC

**Note:** Multiple inheritance is NOT supported in Java through classes — only via interfaces.
**Note:** multiple and hybrid inheritance in Java are supported only through interfaces, not classes.

Hybrid (Virtual) Inheritance in C++ = combination of Hierarchical and Multilevel Inheritance.

### Q: Why isn't multiple inheritance supported via classes in Java?
To reduce complexity and simplify the language. If C inherits both A and B, and A/B have the same method, calling it from C creates ambiguity (which method?). Since compile-time errors are better than runtime errors, Java gives a compile-time error for inheriting 2 classes — regardless of whether methods differ.

```cpp
class parent_class { /* Body of parent class */ };
class child_class: access_modifier parent_class { /* Body of child class */ };
```

## Modes of Inheritance
* **Public mode:** public members of base stay public in derived; protected stay protected
* **Protected mode:** both public and protected members of base become protected in derived
* **Private mode:** both public and protected members of base become private in derived

## Need for Inheritance: 
Implements reusability — code written once (e.g., in `Person`) reused repeatedly. Saves time/resources, creates better connections between classes, achieves method overriding. Used to add new features to an existing class — like a child inheriting parent properties with some of their own new features.
