# TOPIC 1: Introduction to OOPs

The major purpose of C++ programming is to introduce object orientation to the C programming language. The main aim of OOP is to bind together data and the functions that operate on them so no other part of the code can access this data except that function.

OOP is a methodology to design a program using classes and objects. A programming paradigm where everything is represented as an object is a truly object-oriented language — Smalltalk is considered the first truly object-oriented language.

It simplifies software development and maintenance via: Object, Class, Inheritance, Polymorphism, Abstraction, Encapsulation.

## The 4 Pillars
* **Abstraction:** Hiding internal details, showing only functionality. Example: making a phone call — we don't see the internal processing.
* **Inheritance:** One object acquires properties/behaviors of a parent object — base class gives behavior/attributes to derived class. Provides code reusability; used to achieve runtime polymorphism.
* **Polymorphism:** Proper method executes based on the calling object's type — one task performed in different ways.
* **Encapsulation:** Binding (wrapping) code and data into a single unit. Example: a capsule wrapped with different medicines.

## Why OOP?
* Makes development/maintenance of projects more effortless
* Provides data hiding — good for security (procedural programming has global data accessible from anywhere)
* Solves real-world problems naturally
* Increases code reusability, understandability, maintainability
* Helps write generic code that works with a range of data
* Problems can be divided into subparts

**Example (Cars):** Rather than describing each of 100 cars from scratch, you use the same Car class to create 100 objects. Each object (Ferrari, BMW, Mercedes) has its own Year of Manufacture, model, Top Speed, color, Engine Power, efficiency, etc.

## Disadvantages of OOPs
* Requires pre-work and proper planning
* Programs can consume large amounts of memory in certain scenarios
* Not suitable for small problems
* Proper documentation required for later use

## Class vs Structure
| Class | Structure |
| :--- | :--- |
| User-defined blueprint from which objects are created | User-defined collection of variables of different data types |
| Consists of methods/instructions performed on objects | — |
| Default access modifier: private | Default access modifier: public |
| Normally used for data abstraction and further inheritance | Does not support inheritance; may have only a parameterized constructor |
| — | Used for grouping data — e.g., representing a student via name, gpa, age, uid |

## Class vs Object
| Class | Object |
| :--- | :--- |
| Blueprint of an object; used to create objects | Instance of a class |
| No memory allocated when declared | Memory allocated as soon as created |
| A group of similar objects | A real-world entity (book, car) |
| Logical entity | Physical entity |
| Declared only once | Created many times as needed |
| Example: car | Example: BMW, Mercedes, Ferrari |

**Memory allocation note:**

```cpp
class Animal{};        // size = 1 byte
class Animal{ int a; char ch; };   // size = 8 byte
```

When a class is defined, minimum/no memory is allocated — memory is allocated only when instantiated.

## Creating Objects

* **Statically:** `class_name objectName;`
* **Dynamically:** `class_name * objectName = new class_name();`

Here `objectName` is a pointer storing the heap address. The default constructor is called, memory is dynamically allocated for one object, and the address is assigned to the pointer. (Object memory is in heap; in stack, `objectName` becomes a pointer storing the heap address.)
