# packages

It is in the package `java.util`

```java
import java.util.function.Consumer;
import java.util.function.Predicate;
import java.util.function.UnaryOperator;
import sun.misc.SharedSecrets;
```

> the packages in `java.util.function` is for functional programing in java8. All the 3 are `FunctionalInterface`. See also in java8 programming.


> `sun.misc.SharedSecrets`: in the method `private void readObject` a static method is used (to improve performance):
>
> ```java
>  SharedSecrets.getJavaOISAccess().checkArray(s, Object[].class, capacity);
> ```

# class structure

```java
public class ArrayList<E> 
extends AbstractList<E> 
implements List<E>, 
RandomAccess, Cloneable, java.io.Serializable
```

> 知识点
>
> * It is a generic type
> * `implement Serializable` : [see the usage of serialVersionUID](http://swiftlet.net/archives/1268)
> * `RandomAccess` is a marker interface.

# Constructor

```java
public ArrayList(int initialCapacity)
public ArrayList(Collection<? extends E> c)
```



>end





