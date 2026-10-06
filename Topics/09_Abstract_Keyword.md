# TOPIC 9: Abstract Keyword / Abstract Class / Abstract Methods (Java)

* `abstract` keyword declares a method or class as abstract
* **Abstract Class:** contains the `abstract` keyword; may or may not have abstract methods
* If ANY method is abstract, the class MUST be declared abstract
* Cannot be instantiated
* Must be inherited, with implementations provided for its abstract methods
* If inheriting an abstract class, you must implement ALL its abstract methods

## Abstract Methods

Declared in a parent when the actual implementation is left to child classes.

* `abstract` keyword before the method name
* Signature only, NO body
* Ends with `;` instead of `{}`

```java
public abstract class Employee {
    private String name;
    private String address;
    private int number;
    public abstract double computePay();
}
```

### Consequences of an abstract method:

* Containing class must be abstract
* Any inheriting class must override it, or itself become abstract
* We cannot create objects of an abstract class, but can derive from them and use their (non-abstract) data members/functions
