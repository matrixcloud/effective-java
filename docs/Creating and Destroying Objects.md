## Builder Pattern

### Why we need builder pattern

- `The telescoping constructor pattern`: It is hard to write client code when a constructor have many parameters, and harder still to read it.
- `The Java Beans pattern`
    - Because construction is split across multiple calls, a JavaBean may be in an inconsistent state partway through its construction.
    - It precludes the possibility of making a class immutable and requires added effort on the part of the programmer to ensure thread safety.
    
### The advantages of builder pattern

- The built object is immutable
- All parameter default values are in one place
- Provide a fluent API
- Validity checks were omitted for brevity.

