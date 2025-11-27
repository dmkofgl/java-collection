# Annotations

Annotations are metadata added to Java code (classes, methods, fields, parameters, etc.) to provide additional information to the compiler
or runtime tools.

Common annotations:

- `@Override` — indicates overriding a superclass method.
- `@Deprecated` — marks deprecated API.
- `@SuppressWarnings` — suppress compiler warnings.
- `@FunctionalInterface` — ensures single abstract method.

Creating custom annotation example:

```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAnnotation {
    String value() default "default";
    int count() default 1;
}
```

Usage and runtime inspection via reflection:

```java
Method method = Test.class.getMethod("myMethod");
if (method.isAnnotationPresent(MyAnnotation.class)) {
    MyAnnotation ann = method.getAnnotation(MyAnnotation.class);
    System.out.println("Value: " + ann.value());
}
```

