# packages

It is in the package `java.util`

```java
import java.util.function.Consumer;
import java.util.function.Predicate;
import java.util.function.UnaryOperator;
import sun.misc.SharedSecrets;
```

> the packages in `java.util.function` is for functional programing in java8. All the 3 are `FunctionalInterface`. See also in java8 programming.
>
> `sun.misc.SharedSecrets`: in the method `private void readObject` a static method is used \(to improve performance\):
>
> ```java
>  SharedSecrets.getJavaOISAccess().checkArray(s, Object[].class, capacity);
> ```
>
> [Examples](https://www.programcreek.com/java-api-examples/index.php?api=sun.misc.SharedSecrets)

# class structure

```java
public class ArrayList<E> 
extends AbstractList<E> 
implements List<E>, 
RandomAccess, Cloneable, java.io.Serializable
```

* It is a generic type
* `implement Serializable` : [see the usage of serialVersionUID](http://swiftlet.net/archives/1268)
* `RandomAccess` is a marker interface.

# Constructor

```java
public ArrayList(int initialCapacity)
public ArrayList() -> ArrayList(10)
public ArrayList(Collection<? extends E> c)
```

### `public ArrayList(Collection<? extends E> c)`

```java
public ArrayList(Collection<? extends E> c) {
    elementData = c.toArray();
    if ((size = elementData.length) != 0) {
        // c.toArray might (incorrectly) not return Object[] (see 6260652)
        if (elementData.getClass() != Object[].class)
            elementData = Arrays.copyOf(elementData, size, Object[].class);
    } else {
        // replace with empty array.
        this.elementData = EMPTY_ELEMENTDATA;
    }
}
```

* `Collection<? extends E>` ? is in the subclass of E

# public method

## `public void trimToSize`

```java
public void trimToSize() {
    modCount++;
    if (size < elementData.length) {
        elementData = (size == 0)
          ? EMPTY_ELEMENTDATA
          : Arrays.copyOf(elementData, size);
    }
}
```

trim the `ArrayList` to its current size. When the length of list and the number of opperation are large, this method can be used to save space and improve efficiency. 

* `modCount` is the times that the list be modified.
* `EMPTY_ELEMENTDATA` is {}



> end



