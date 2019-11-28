## Generics

### Don’t use raw types

```java
// Use of raw type for unknown element type - don't do this!

static int numElementsInCommon(Set s1, Set s2) {
    int result = 0;
    for (Object o1 : s1)
        if (s2.contains(o1))
            result++;
    return result;
}
```

This code is dangerous, should use `unbonded wildcard type`

```java
// Uses unbounded wildcard type - typesafe and flexible

static int numElementsInCommon(Set<?> s1, Set<?> s2) { ... }
```

wildcard type is safe and the raw type isn’t. You can put any element into a collection with a raw type, easily corrupting the collection’s type invariant;
you can’t put any element (other than null) into a `Collection<?>`. Attempting to do so will generate a compile-time error message like this:

### Eliminate unchecked warnings

### Prefer lists to arrays

First, arrays are `covariant`. This scary-sounding word means simply that if Sub is a subtype of Super, then the array type Sub[] is a subtype of the array type Super[]. 
Generics, by contrast, are `invariant`: for any two distinct types Type1 and Type2, List<Type1> is neither a subtype nor a supertype of List<Type2>

### Favor generic types

### Favor generic methods

Static utility methods that operate on parameterized types are usually generic. All of the “algorithm” methods in Collections (such as binarySearch and sort) are generic.

#### Recursive type bound. 

A common use of recursive type bounds is in connection with the Comparable interface, which defines a type’s natural ordering

```java
public interface Comparable<T> {
    int compareTo(T o);
}
```

The type parameter T defines the type to which elements of the type implementing Comparable<T> can be compared. In practice, nearly all types can be compared only to elements of their own type. So, for example, String implements Comparable<String>, Integer implements Comparable<Integer>, and so on.
Many methods take a collection of elements implementing Comparable to sort it, search within it, calculate its minimum or maximum, and the like. 

```java
// Using a recursive type bound to express mutual comparability
public static <E extends Comparable<E>> E max(Collection<E> c);
```

The type bound <E extends Comparable<E>> may be read as “any type E that can be compared to itself,” which corresponds more or less precisely to the notion of mutual comparability.

### Type Erase

When we define a generic class, java will not create a new type instead of erasing the specific type and replace it with Object.

```java
public class ObjectContainer<T> { 
    private T contained; 
    public ObjectContainer(T contained) { 
        this.contained = contained; 
    } 
    public T  getContained() { 
        return contained; 
    }
}
```

After complied, the code will be. (The type T was been erased and replace with Object)

```java
public class ObjectContainer {
    private Object contained; 
    public ObjectContainer(Object contained) { 
        this.contained = contained; 
    } 
    public Object getContained() { 
        return contained;
    }
}
```

### Heap Pollution

[Wiki](https://en.wikipedia.org/wiki/Heap_pollution)

```java
public class HeapPollutionDemo
{
   public static void main(String[] args)
   {
      Set s = new TreeSet<Integer>();
      Set<String> ss = s;            // unchecked warning
      s.add(new Integer(42));        // another unchecked warning
      Iterator<String> iter = ss.iterator();
      while (iter.hasNext())
      {
         String str = iter.next();   // ClassCastException thrown
         System.out.println(str);
      }
   }
}
```