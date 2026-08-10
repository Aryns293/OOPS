# TOPIC 5: Static Data Members & Member Functions

* Only one copy exists for the entire class, shared by all objects
* Initialized before any object is created — even before `main()` starts
* Visible only within the class, but lifetime = entire program
* `static data_type name_of_member;` — Declared inside the class body. Defined outside the class. Static member variables are not belonging to any objects, but its belongs to whole class so these are called class member variable.
* Belongs to the class, not any object

**Advantage:** memory efficient — no instance needed to access it.

## When declared static?

* To refer to a property common to all objects (e.g., `rateOfInterest`, `companyName`)
* To track data common to all — e.g., a static counter of objects created

```cpp
class Truck {
private:
   static int count = 0;
public:
   static int getCount() {
      return count;
   }
   Truck() {
      count++;
   }
};
```
