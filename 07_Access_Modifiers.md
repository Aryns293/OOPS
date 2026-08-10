# TOPIC 7: Access Modifiers

## Access Modifiers in Java — Full Table

**Default:** when no access modifier is specified for a class, method, or data member — accessible only within the same package.

| | `default` | `private` | `protected` | `public` |
| :--- | :--- | :--- | :--- | :--- |
| **Same Class** | Yes | Yes | Yes | Yes |
| **Same package subclass** | Yes | No | Yes | Yes |
| **Same package non-subclass** | Yes | No | Yes | Yes |
| **Different package subclass** | No | No | Yes | Yes |
| **Different package non-subclass** | No | No | No | Yes |

Private members are not accessible directly by any object/function outside the class — only member functions or friend functions can access private members (C++).

## Types of Class Member Functions in C++

### 1. Simple Member Functions
No special prefix keyword.

### 2. Static Member Functions
Declared using `static`. Work for the class as a whole.

```cpp
class X {
public:
   static void f() { /* statement */ }
};

int main() { 
   X::f(); // typically called via class name + ::
}  
```

* Cannot access ordinary data members/member functions — only static ones
* No `this` keyword — that's why it can't access ordinary members

### 3. Const Member Functions
`const` prevents the function from modifying the object/its data members.

```cpp
void fun() const { /* statement */ }
```

### 4. Inline Functions
All member functions defined inside the class definition are, by default, Inline.

### 5. Friend Functions
NOT class member functions, but given private access.

```cpp
class WithFriend {
   int i;
public:
   friend void fun();
};

void fun(){
   WithFriend wf; 
   wf.i = 10; 
   cout << wf.i;
}

int main(){ 
   fun(); 
}
```

**Making an entire class a friend:**

```cpp
class Other{ 
   void fun(); 
};

class WithFriend{
private: 
   int i;
public:
   void getdata();
   friend void Other::fun();
   friend class Other;   // all member functions of Other become friend functions
};
```

**NOTE:** Friend Functions are why C++ is not called a "pure" Object Oriented language — they violate Encapsulation.

**Characteristics of Friend Function:**
* Not in the scope of the class it's friend of
* Cannot be called using the object of that class
* Invoked like a normal function, without any object
* Cannot use member names directly (unlike member functions)
* Can be declared in public or private sections without affecting meaning
* Usually has objects as arguments
* Can be a global function or a member of another class

**Note:** Private members are not allowed to be accessed directly by any object or function outside the class. Only the member functions or the friend functions are allowed to access the private data members of the class in C++.
