# TOPIC 12: Super Keyword (Java)

A reference variable referring to the immediate parent class object.

## Usage of Super Keyword — 3 numbered uses

1. `super` can be used to refer to the immediate parent class's instance variable
2. `super` can be used to invoke the immediate parent class's method
3. `super()` can be used to invoke the immediate parent class's constructor

**Note:** `super()` is added automatically by the compiler in each class constructor if there's no explicit `super()` or `this()`.

**Real use:** If `Emp` inherits `Person`, all `Person` properties are inherited by default. To initialize all properties, use the parent class constructor from the child via `super()` — reusing the parent's constructor.
