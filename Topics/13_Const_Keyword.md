# TOPIC 13: Const Keyword (C++)

Whenever `const` keyword is attached with any method(), variable, pointer variable, and with the object of a class it prevents that specific object/method()/variable to modify its data items value.

## Declaring constants — 3 forms:

```cpp
const int var;              // ✗ Invalid — no value
const int var; var = 5;     // ✗ Invalid — assigned separately
const int var = 5;          // ✓ Valid — declared and initialized together
```

## Rules for const variables:

* Cannot be left uninitialized at declaration
* Cannot be assigned a value anywhere else in the program
* Must be given an explicit value at declaration

## Const with Pointer Variables: 

Three possible ways to use const with a pointer:
1. Pointer to const value
2. Const pointer
3. Const pointer to const value

*(Notes defer to GeeksforGeeks documentation for full detail rather than covering all three inline).*
