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
// Output: 
// Note 7 Pro 
// 2019

Here you can see that we have two data members `model` and `year_of_manufacture`. In member function `set_details()`, we have two local variables with the same name as the data members' names. Suppose you want to assign the local variable value to the data members. In that case, you won't be able to do until unless you use this pointer because the compiler won't know that you are referring to the object's data members unless you use this pointer. This is one of example where you must use this pointer.
```

## Why needed? 

Explain the situation where this pointer is used: As we know each object gets its own copy of data members and all objects shares a single copy of member functions. Then now, question is that if only one copy of each member function exist which is used by multiple objects, how are the proper data members are accessed and updated. Ans: The complier supplies an implicit pointer along with the names of the functions as 'this'. Where 'this' refers the address of current object. The 'this' pointer is available only within the non-static member functions of a class. If the member function is static, it will be common to all the objects, and hence a single object can't refer to those functions independently.

## Interview Q&A
* **What is this?** — accessible only inside member functions, points to the calling object.
* **When is it necessary?** — when local variable names match data member names.
* **Similarity between deep and shallow copy?** — both used to copy data between objects.
