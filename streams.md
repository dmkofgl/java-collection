# Stream API

The Java Stream API (introduced in Java 8) is a framework for processing sequences of data in a declarative, functional style.

## Concepts
- Source (collection, array, I/O channel)
- Intermediate operations (lazy)
- Terminal operations (trigger execution)

Example

```java
numbers.stream()
    .filter(n -> n % 2 == 0)
    .sorted()
    .forEach(System.out::println);
```

## Common operations
- Intermediate: `filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`, `limit`, `skip`.
- Terminal: `forEach`, `collect`, `reduce`, `count`, `findFirst`, `findAny`, `anyMatch`, `allMatch`.

## Collect examples
- `collect(Collectors.toList())`
- `collect(Collectors.toSet())`
- `collect(Collectors.groupingBy(...))`

## Reduce examples
- `reduce(0, Integer::sum)`
- `reduce(Integer::max)`

Notes: prefer `collect` for building mutable containers; be careful with side-effects in parallel streams.

