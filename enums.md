# Enums

In Java, an enum (short for enumeration) is a special data type that represents a fixed set of constants — for example, days of the week,
directions, colors, etc.

```java
enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}
```

Features of Enums

- Type-Safe Constants — compile-time type safety.
- Implicit static and final — enum constants are public static final.
- Enums can have fields, constructors and methods.

Notes:
- Enums implicitly extend `java.lang.Enum` and cannot be subclassed.
- Enums can implement interfaces.
- Each enum constant is a singleton instance.

Example with methods and fields:

```java
public enum Status {
    NEW(0), IN_PROGRESS(1), DONE(2);

    private final int code;

    Status(int code) { this.code = code; }

    public int getCode() { return code; }
}
```

