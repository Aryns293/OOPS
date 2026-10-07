# Q18 Function Overloading

## 🎯 Interview Answer
**Function overloading** is a C++ feature where multiple functions can have the same name but different **parameter lists**. The compiler performs **overload resolution** at compile time and selects the best matching function based on the arguments provided. It is a form of compile-time polymorphism.

### 📜 Rules for Overloading
1. Same function name.
2. Different parameter list (the lists can differ in the **number**, **types**, or **order** of parameters).
3. Return type alone **cannot** distinguish overloaded functions.

> **Note:** Parameters are the variables in the function declaration, while arguments are the actual values passed during the call.

### 💻 Example
```cpp
int add(int a, int b) { 
    return a + b; 
} 

double add(double a, double b) { 
    return a + b; 
} 

int add(int a, int b, int c) { 
    return a + b + c; 
} 
```
> **Note:** The compiler selects the best matching overload during overload resolution.

### ⚠️ Common Follow-Up: Can these overloads coexist?
```cpp
int fun(int x);
double fun(int x);
```
**Answer:** **No.** Their parameter lists are identical. The return type is not considered when selecting an overload.

---

## ❓ How Does Function Overloading Cause Ambiguity?
Ambiguity occurs when the compiler cannot decide which overloaded function to call. This leads to a **compile-time error**.

### 1️⃣ Type Conversion Ambiguity
When an argument can be converted to multiple parameter types, and no single conversion sequence is clearly better than the others.

```cpp
void fun(int x) { cout << "int"; } 
void fun(float x) { cout << "float"; }

int main() { 
    fun(1.2); 
    // 1.2 is a double. 
    // ERROR: ambiguous call 
} 
```
> **Explanation:** `1.2` is a double. Both `double → int` and `double → float` are valid conversions, but neither overload is preferred (neither provides a better conversion sequence), so the call is ambiguous.

### 2️⃣ Default Arguments Ambiguity
When a function with default arguments conflicts with another overload.

```cpp
void fun(int x) { cout << "one arg"; } 
void fun(int x, int y = 9) { cout << "two args"; }

int main() { 
    fun(12); 
    // Which one? fun(int) or fun(int, int=9)? 
    // ERROR: ambiguous call 
} 
```
> **Explanation:** Both are viable candidates that can accept one argument. Overload resolution cannot choose a unique best match.

### 3️⃣ Pass by Reference vs Pass by Value Ambiguity
When overloads differ only by reference vs value.

```cpp
void fun(int x) { cout << "value"; } 
void fun(int &x) { cout << "reference"; }

int main() { 
    int a = 10; 
    fun(a); 
    // ERROR: ambiguous call 
} 
```
> **Explanation:** Both overloads are viable for an lvalue `int`, but neither is a better match than the other, so overload resolution cannot select a unique best candidate.
>
> **Important:** This remains ambiguous even if you use `const int& x`. The underlying issue is equally viable candidates, not just the syntax at the call site.

---

## 📊 Diagram: Ambiguity Causes

```text
               Function Overloading Ambiguity
              /              |              \
   Type Conversion      Default Args      Ref vs Value
```

---

## 💡 Key Points to Impress
- **Function overloading** is compile-time polymorphism.
- Same name, different parameter list.
- Return type alone **cannot** overload.
- **Ambiguity** happens when the compiler cannot pick the best match.
- **Common causes:** type conversion, default arguments, reference vs value.
- Ambiguity is a **compile-time error** — the program won’t compile.
- **To fix:** avoid ambiguous overloads, use explicit casts, or rename functions.

---

## 🎯 Summary to Impress
- **Function overloading:** same name, different parameters, resolved at compile time.
- **Ambiguity:** compiler cannot choose between overloads.
- **Causes:** type conversion, default arguments, ref vs value.
- **Solution:** design overloads carefully, avoid overlapping viable candidates.
- It’s a powerful feature but must be used with precision.
