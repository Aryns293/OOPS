# TOPIC 18: Virtual Base Class (Diamond Problem)

**Need:** Class A inherited by B and C, both B and C inherited into D (diamond shape). Data/functions of A get inherited twice into D — once via B, once via C. Accessing A's members from D's object causes ambiguity (which copy — via B or via C?). Confuses compiler, produces error.

**Diagram:** Class A → (labeled edges "A", "A") → Class B and Class C → each carries "B and B's A" / "C and C's A" → both → Class D → "D has now 2 A: B's A and C's A — This leads to ambiguity."

**Solution** — declare A as virtual base class: only ONE copy of the data/function member is shared. `virtual` can be written before or after `public`. Saves space, avoids ambiguity — a single shared copy used by all base classes using the virtual base.

```cpp
class A { 
public: 
   int a; 
   A(){ a = 10; } 
};
class B : public virtual A {};
class C : public virtual A {};
class D : public B, public C {};
int main() { 
   D object; 
   cout << "a = " << object.a << endl; 
}
```
