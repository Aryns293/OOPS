# Q32 Destructor Overloading & Static Constructors

## 🎯 Interview Answer

### Can you overload a destructor?
**No.** A destructor takes no arguments (parameters) and has no return type. Since function overloading requires a difference in the parameter list, a destructor simply cannot be overloaded. A class can have **only one** destructor.

### Can a constructor be static?
**No.** Constructors are invoked automatically to initialize a specific instance (object) of a class. The `static` keyword means the member belongs to the class itself, not to any specific object. Therefore, it makes no sense for a constructor to be static. Additionally, constructors cannot be virtual either.

---

## 🎯 Summary to Impress
- **Destructors:** Only one per class. Cannot be overloaded because they take no parameters.
- **Constructors:** Cannot be static or virtual because they are intrinsically tied to the creation of a specific object instance.
