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

```java
public final class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private final UUID id = UUID.randomUUID();
    private final String name;
    // ... equals/hashCode by id if identity semantics desired
}
```

## Practical guidance
- Add `serialVersionUID` explicitly.
- Use `final` for UUID fields when id should never change.
- Consider external ids (DB PKs) instead of generated UUID if available.

## Pitfalls & privacy
- UUID increases payload size (~16 bytes + overhead).
- `UUID.randomUUID()` is not a cryptographic token; for secure tokens use dedicated crypto.
- Stable ids can leak linkability across systems; consider privacy implications.

## Advanced
- Implement `writeObject`/`readObject` for controlled compatibility.
- Serialize references by id for large graphs instead of embedding full objects.

