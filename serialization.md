# Serialization Support

Serialization in Java is the process of converting an object into a byte stream so it can be:

- saved to disk,
- transmitted over a network,
- or otherwise stored/transported.

Deserialization is the reverse: turning the byte stream back into a live object.

Java provides automatic serialization via the `java.io.Serializable` marker interface.

## Key points
- No methods to implement.
- Fields are serialized automatically unless marked `transient`.
- Java uses `ObjectOutputStream` / `ObjectInputStream`.

## Example

```java
class Person implements java.io.Serializable {
    private String name;
    private int age;
    private transient String password; // not serialized
}
```

## Serialization + UUID — why and when

Including a UUID is useful when serialized objects need a stable, globally unique identity across systems. UUIDs help with deduplication,
referential integrity, tracing, and merging data from multiple sources.

Minimal pattern:

```text
public final class Person implements java.io.Serializable {
    private static final long serialVersionUID = 1L;
    private final java.util.UUID id = java.util.UUID.randomUUID();
    private final String name;
    // ... equals/hashCode by id if identity semantics desired
}
```

## Practical guidance
- Add `serialVersionUID` explicitly.
- Use `final` for UUID fields when id should never change.
- Consider external ids (DB PKs) instead of generated UUID if available.

### `serialVersionUID` — details and best practices

`serialVersionUID` is a `private static final long` field that Java's serialization runtime uses to verify that a loaded class and the serialized
object are compatible. If the `serialVersionUID` of the class does not match the `serialVersionUID` embedded in the serialized stream,
`InvalidClassException` is thrown during deserialization.

Why it's important

- By default, if you don't declare `serialVersionUID`, the JVM computes one at runtime from the class signature (fields, methods, interfaces,
  etc.). That generated value can change when you recompile or when the class structure changes subtly, which can break compatibility
  unexpectedly.
- Declaring `serialVersionUID` explicitly lets you control binary compatibility across versions of a class.

How to choose a value

- Any `long` constant works (commonly `1L` for the initial version). Many projects use a random large long or the output of the
  `serialver` tool as the value.
- Example:

```java
private static final long serialVersionUID = 1L;
```

Generating/inspecting the value with `serialver`

- The JDK provides the `serialver` tool to compute the default value the runtime would generate for the current class.

Example (run in terminal from classpath where the class is available):

```bash
serialver -show com.example.Person
# or for a compiled class file
serialver -classpath out com.example.Person
```

Compatibility rules (simplified)

- Compatible changes (do not require changing `serialVersionUID` if you want old streams to remain readable):
  - Adding new fields (you should handle missing fields during read)
  - Adding `private` methods
  - Changing method bodies
- Incompatible changes (typically require a new `serialVersionUID` or careful migration):
  - Removing fields
  - Changing the type of a field
  - Changing class hierarchy (superclass changes)
  - Changing non-private static final constants used in serialization logic

When to change the `serialVersionUID`

- If you make incompatible structural changes and you want deserialization to fail fast (rather than attempting to read a mismatched stream), change
  the `serialVersionUID` to a new value.
- If you maintain compatibility (for example, you add fields and provide defaults), keep the same `serialVersionUID`.

Handling version differences in code

- Use `defaultReadObject()` inside `readObject` and then fix up any missing/new fields. Provide sensible defaults so older streams can be read.

Example:

```java
private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
    in.defaultReadObject(); // reads fields present in the stream

    // Compatibility fixup for older streams that don't have 'email'
    if (this.email == null) {
        this.email = ""; // or compute a default
    }
}
```

Advanced hooks

- `writeObject` / `readObject` — control precisely what and how you serialize.
- `writeReplace` / `readResolve` — substitute different objects during serialization/deserialization.
- `serialPersistentFields` — list which fields should be serialized when you want a stable serialized form independent of class fields.

Pitfalls & reminders

- Don't rely on the compiler-generated `serialVersionUID` across builds if you need stable compatibility.
- Declaring `serialVersionUID` does not magically make incompatible changes safe — it only controls whether the runtime will attempt to deserialize.
- Test deserialization between versions (e.g., keep sample streams and verify newer code can read older streams if compatibility is required).
