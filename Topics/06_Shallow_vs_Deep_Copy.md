# TOPIC 6: Shallow Copy vs Deep Copy

## Shallow Copy

Copies data of all variables, but pointers are copied (not what they point to) — original and copy point to the same memory address. Changes via one reflect in the other (unpleasant side effect).

The compiler implicitly generates a copy constructor/assignment operator that does shallow copy by default.

```cpp
class students {
   int age; char * names;
public:
   students(int age, char * names) {
      this->age = age;      // shallow copy
      this->names = names;
   }
};
```

Shallow copy is faster — just copies the reference.

**Diagram (Bag1/Bag2 shallow copy):** both Bag1 and Bag2 arrays point to the same shared boxes (Shivam, Shyam, Aseem, Anmol) — arrows go both directions to the same objects.

## Deep Copy

Copies all fields AND allocates similar memory resources with the same value — requires explicitly defining the copy constructor.

```cpp
class student {
   int age; char * names;
public:
   student(int age, char * names) {
      this->age = age;    // deep copy
      this->names = new char[strlen(names)+1];
      strcpy(this->names, names);  // new array, copied data
   }
};
```

**Diagram (Bag1/Bag2 deep copy):** Bag1 and Bag2 each have their own separate copies of Shivam, Shyam, Aseem, Anmol — two independent sets of boxes.

**NOTE:** Shallow copy works fine if no variable of the object is in heap. If a variable is dynamically allocated in heap, the copied object's variable references the same memory location.

## Comparison Table

| Shallow Copy | Deep Copy |
| :--- | :--- |
| Stores references to the original memory address | Stores copies of the object's value |
| Changes to the copy reflect in the original | Changes to the copy don't reflect in the original |
| Points references to objects | Recursively copies objects too |
| Faster | Comparatively slower |
