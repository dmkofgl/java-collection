# Generics

Java Generics let you parameterize types — you can write code that handles any object type while keeping strong compile-time type checking.
They were introduced in Java 5 (JDK 1.5) to eliminate unsafe type casts and provide cleaner, type-safe APIs (especially for collections).

## Basic generics usage

You can define classes with type parameters that are specified when an instance is created.

```java
class Box<T> {

    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}

Box<Integer> intBox = new Box<>();
intBox.set(10);
System.out.println(intBox.get()); // 10

Box<String> strBox = new Box<>();
strBox.set("Hello");
System.out.println(strBox.get()); // Hello
```

## Wildcards, super/extends bound

Wildcards (?) allow you to specify flexible generic type relationships — especially useful in methods that accept collections of various element types.

| Wildcard      | Meaning                             | Example                  |
|---------------|-------------------------------------|--------------------------|
| `?`           | Unknown type                        | `List<?> list`           |
| `? extends T` | Any type that *is a subtype of* T   | `List<? extends Number>` |
| `? super T`   | Any type that *is a supertype of* T | `List<? super Integer>`  |

- Use `? extends` when you only need to read values.
- Use `? super` when you need to write values.

## Type erasure

Java’s generics are implemented using type erasure. At compile time, generic types are erased and replaced by their upper bound (or Object if unbounded).

Example: `List<Integer>` and `List<String>` are the same at runtime.

## Reflection and Generics

Reflection can inspect generic declarations at runtime (via `Field.getGenericType()` etc.), but runtime type parameters are not reified.

