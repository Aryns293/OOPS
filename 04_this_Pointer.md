# TOPIC 4: this Pointer

Holds the address of the current object.

## Three main usages:
* Refer to the current class instance variable
* Pass the current object as a parameter to another method
* Declare indexers

```cpp
class mobile {
   string model; 
   int year_of_manufacture;
public:
   void set_details(string model, int year_of_manufacture){
      this->model = model;
      this->year_of_manufacture = year_of_manufacture;
   }
   void print(){ 
      cout << this->model << endl; 
      cout << this->year_of_manufacture << endl; 
   }
};
// Output: Note 7 Pro / 2019
```

## Why needed? 
Each object has its own data members, but all objects share ONE copy of member functions. The compiler passes an implicit `this` pointer with function calls so the correct object's data is used. Only available in non-static member functions — static functions are common to all objects, so can't refer to a specific one via `this`.

## Interview Q&A
* **What is this?** — accessible only inside member functions, points to the calling object.
* **When is it necessary?** — when local variable names match data member names.
* **Similarity between deep and shallow copy?** — both used to copy data between objects.
