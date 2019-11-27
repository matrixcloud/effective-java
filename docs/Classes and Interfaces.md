## Classes and Interfaces

### Minimize the accessibility of classes and members

A well-designed component hides all its implementation details, cleanly separating its API from its implementation.
This concept, known as `information hiding or encapsulation`, is a fundamental tenet of software design

Note that a nonzero-length array is always mutable, so it is wrong for a class to have a public static final array field, or an accessor that returns such a field.

```java
// Potential security hole!

public static final Thing[] VALUES = { ... };
```

### In public classes, use accessor methods, not public fields

Public classes should never expose mutable fields.

### Minimize mutability

To make a class immutable, follow these five rules:

- Don’t provide methods that modify the object’s state (known as mutators).
- Ensure that the class can’t be extended.
- Make all fields final. 
- Make all fields private. 
- Ensure exclusive access to any mutable components. 

### Favor composition over inheritance

### Design and document for inheritance or else prohibit it

### Prefer interfaces to abstract classes

### Design interfaces for posterity

### Use interfaces only to define types

### Prefer class hierarchies to tagged classes

### Favor static member classes over nonstatic

There are four kinds of nested classes: `static member classes`, `nonstatic member classes`, `anonymous classes`, and `local classes`. All but the first kind are known as inner classes. 

Syntactically, the only difference between static and nonstatic member classes is that static member classes have the modifier static in their declarations. Despite the syntactic similarity, these two kinds of nested classes are very different. 
- Each instance of a nonstatic member class is implicitly associated with an enclosing instance of its containing class. 

> If you declare a member class that does not require access to an enclosing instance, always put the static modifier in its declaration

### Limit source files to a single top-level class