# TOPIC 10: Final Keyword (Java)

Applies to variables, methods, and classes.

**Mnemonic diagram:** Java Final Keyword → Stop Value Change / Stop Method Overriding / Stop Inheritance.

* **Final variable** — value cannot be changed (constant). `final int speedlimit = 90;`
* **Final method** — cannot be overridden.
* **Final class** — cannot be extended.

**Q: Is a final method inherited?** 
Yes, inherited, but cannot be overridden.

**Q: What is a blank/uninitialized final variable?** 
Not initialized at declaration — can only be set in the constructor. Useful for things like a PAN CARD number, set once at object creation.

**Q: Can we initialize a blank final variable?** 
Yes, but only in the constructor.
* **Static Blank Final Variable:** static final variable not initialized at declaration — only initializable in a static block.

**Q: What is a final parameter?** 
If a parameter is final, its value cannot be changed.

**Q: Can a constructor be final?** 
No — a constructor is never inherited.
