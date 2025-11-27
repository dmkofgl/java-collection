# Exception Handling

An exception is an event that disrupts the normal flow of the program. Exception handling in Java allows a program to gracefully handle
runtime errors without crashing.

## try/catch

```java
try {
    int result = 10 / 0; // throws ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Division by zero");
} finally {
    System.out.println("always runs");
}
```

## try-with-resources (Java 7+)

Resources implementing `AutoCloseable` can be used in try-with-resources to ensure automatic close.

```java
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    System.out.println(br.readLine());
}
```

## Exception hierarchy

```
Throwable
 ├── Error
 └── Exception
      ├── RuntimeException (unchecked)
      └── Checked Exceptions
```

- Checked exceptions must be declared or caught.
- Runtime exceptions are unchecked; usually programming errors.

