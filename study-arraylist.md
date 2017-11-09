# packages

It is in the package `java.util`

```java
import java.util.function.Consumer;
import java.ut
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


# Field
```java
/**
 * The array buffer into which the elements of the ArrayList are stored.
 * The capacity of the ArrayList is the length of this array buffer. Any
 * empty ArrayList with elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA
 * will be expanded to DEFAULT_CAPACITY when the first element is added.
 */
transient Object[] elementData;
```
* it is transient, it means not serializable. Learn transient [here](https://www.javaworld.com/article/2074911/learn-java/java-se-transience.html) or [in Chinese version](http://www.importnew.com/12611.html)
* it is defualt and **not private** to simplify nested class access.


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

### `public void trimToSize`

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


# commonly used method in array list

### public int indexOf(Object o)
```java
public int indexOf(Object o) {
    if (o == null) {
        for (int i = 0; i < size; i++)
            if (elementData[i]==null)
                return i;
    } else {
        for (int i = 0; i < size; i++)
            if (o.equals(elementData[i]))
                return i;
    }
    return -1;
}
```
* `indexOf(null)` returns the position of `null`
* `indexOf(object)` returns the position of object
* if not found return -1

Here consider the `ArrayList<Integer>`: `indexOf(5)` will first be converted as `indexOf(new Integer(5))`. Then Integer is Object, it overides the `equals` method. 

See the `equals` method in `Integer.class`:
```java
public boolean equals(Object obj) {
    if (obj instanceof Integer) {
        return value == ((Integer)obj).intValue();
    }
    return false;
}
```

`o.equals(elementData[i])` is equivalant to `5 == elementData[i]`

### `public E get(int index)`
```java
public E get(int index) {
    rangeCheck(index);

    return elementData(index);
}

private void rangeCheck(int index) {
    if (index >= size)
        throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
}

private String outOfBoundsMsg(int index) {
    return "Index: "+index+", Size: "+size;
}
```

the `get` method is one of the most commonly used method in list. There are two private method be designed to support the `get` method. If `throw new exception` appears many times in your program, you can also use this way to design.


### `public void sort(Comparator<? super E> c)`
```java
@Override
@SuppressWarnings("unchecked")
public void sort(Comparator<? super E> c) {
    final int expectedModCount = modCount;
    Arrays.sort((E[]) elementData, 0, size, c);
    if (modCount != expectedModCount) {
        throw new ConcurrentModificationException();
    }
    modCount++;
}
```

* `modCount` is used here to deal with concurrent problem.
* the way to sort is put into `Arrays.class`
* it override `sort` in `List<E>`    
```java
@SuppressWarnings({"unchecked", "rawtypes"})
default void sort(Comparator<? super E> c) {
    Object[] a = this.toArray();
    Arrays.sort(a, (Comparator) c);
    ListIterator<E> i = this.listIterator();
    for (Object e : a) {
        i.next();
        i.set((E) e);
    }
}
``` 

### public E remove(int index)

```java
public E remove(int index) {
    rangeCheck(index);

    modCount++;
    E oldValue = elementData(index);

    int numMoved = size - index - 1;
    if (numMoved > 0)
        System.arraycopy(elementData, index+1, elementData, index,
                         numMoved);
    elementData[--size] = null; // clear to let GC do its work

    return oldValue;
}

    ```

* in all kind of `remove` method, you can return void or ** return the removed value**.
* notice that `elementData[--size] = null` is to release memory. **Learn more in GC**



# private method

### grow
```java
private void grow(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}

```

* `newCapacity` is 3 times `oldCapacity`

> end



