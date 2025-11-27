# Core Libraries

## Object
- `toString()`, `equals(Object)`, `hashCode()`, `clone()`, `finalize()`.

## Objects
- Utility: `Objects.requireNonNull`, `Objects.equals`, `Objects.hash`.

## System
- `System.out`, `System.err`, `System.in`, `System.currentTimeMillis()`, `System.gc()`, `System.exit()`.

## Optional
- `Optional<T>` to avoid null checks: `Optional.ofNullable`, `orElse`, `ifPresent`.

## Random, UUID, Base64
- `Random` for PRNG, `UUID.randomUUID()` for IDs, `Base64` encoder/decoder.

Examples

```java
String encoded = Base64.getEncoder().encodeToString("hello".getBytes());
String decoded = new String(Base64.getDecoder().decode(encoded));

UUID uuid = UUID.randomUUID();
```

