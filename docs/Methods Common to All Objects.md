## Methods Common to All Objects

### Obey the general contract when overriding equals

To avoid problems is not to override the equals method if any of the following conditions apply:

- Each instance of the class is inherently unique. 
- There is no need for the class to provide a “logical equality” test. 
- A superclass has already overridden equals, and the superclass behavior is appropriate for this class.
- The class is private or package-private, and you are certain that its equals method will never be invoked. 

It is appropriate to override `equals` when a class has a notion of logical equality that differs from mere object identity and a superclass has not already overridden equals
When you override the equals method, you must adhere to its general contract. 

- `Reflexive`: For any non-null reference value x, x.equals(x) must return true.
- `Symmetric`: For any non-null reference values x and y, x.equals(y) must return true if and only if y.equals(x) returns true.
- `Transitive`: For any non-null reference values x, y, z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) must return true.
- `Consistent`: For any non-null reference values x and y, multiple invocations of x.equals(y) must consistently return true or consistently return false, provided no information used in equals comparisons is modified.
- For any non-null reference value x, x.equals(null) must return false.

A recipe for a high-quality equals method.

- Use the == operator to check if the argument is a reference to this object.
- Use the instanceof operator to check if the argument has the correct type.
- Cast the argument to the correct type. 
- For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object.

> When you are finished writing your equals method, ask yourself three questions: Is it symmetric? Is it transitive? Is it consistent?

```java
// Class with a typical equals method

public final class PhoneNumber {

    private final short areaCode, prefix, lineNum;

    public PhoneNumber(int areaCode, int prefix, int lineNum) {
        this.areaCode = rangeCheck(areaCode,  999, "area code");
        this.prefix   = rangeCheck(prefix,    999, "prefix");
        this.lineNum  = rangeCheck(lineNum,  9999, "line num");
    }

    private static short rangeCheck(int val, int max, String arg) {
        if (val < 0 || val > max)
           throw new IllegalArgumentException(arg + ": " + val);
        return (short) val;
    }

    @Override public boolean equals(Object o) {
        if (o == this)
            return true;
        if (!(o instanceof PhoneNumber))
            return false;
        PhoneNumber pn = (PhoneNumber)o;
        return pn.lineNum == lineNum && pn.prefix == prefix
                && pn.areaCode == areaCode;
    }

    // Remainder omitted
}
```

Here are a few final caveats:

- Always override hashCode when you override equals
- Don’t try to be too clever.
- Don’t substitute another type for Object in the equals declaration. 

### Always override hashcode when you override equals

You must override hashCode in every class that overrides equals. 
Here is the contract, adapted from the Object specification :

- When the `hashCode` method is invoked on an object repeatedly during an execution of an application, it must consistently return the same value, provided no information used in equals comparisons is modified. This value need not remain consistent from one execution of an application to another.
- If two objects are equal according to the equals(Object) method, then calling hashCode on the two objects must produce the same integer result.
- If two objects are unequal according to the equals(Object) method, it is not required that calling hashCode on each of the objects must produce distinct results. However, the programmer should be aware that producing distinct results for unequal objects may improve the performance of hash tables.

> The key provision that is violated when you fail to override hashCode is the second one: equal objects must have equal hash codes.

### Always override toString

The toString contract goes on to say, “It is recommended that all subclasses override this method.” Good advice, indeed!

### Override clone judiciously

