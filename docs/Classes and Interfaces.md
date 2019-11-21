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
