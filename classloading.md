# Classloading

## Classloading

Classloading is the process by which the Java Virtual Machine (JVM) loads Java classes (.class files) into memory so they can be executed.

When you run a Java program, the JVM doesn’t load all classes at once — it loads them on demand, using special components called
ClassLoaders.

JVM loads classes dynamically from classpath using built-in or custom class loaders. Supports parent delegation model
for security and isolation.

A ClassLoader is a part of the JVM responsible for:

1. Locating class files (from disk, JARs, network, etc.)
2. Loading them into memory
3. Defining them in the JVM so code can use them

Each loaded class belongs to a specific namespace managed by a ClassLoader.

Java uses a hierarchical delegation model of classloaders:

```
Bootstrap ClassLoader
↓
Extension (Platform) ClassLoader
↓
Application (System) ClassLoader
↓
Custom ClassLoaders (optional)
```

- Bootstrap ClassLoader: loads core Java classes.
- Extension / Platform ClassLoader: loads platform APIs.
- Application / System ClassLoader: loads application classes from classpath.
- Custom ClassLoaders: for special loading policies (application servers, plugin systems).

When a classloader is asked to load a class:

1. It first delegates the request to its parent.
2. If the parent can’t find it, it tries to load it itself.

This ensures that core classes aren’t overridden by user code and duplicate classes aren’t loaded unnecessarily.

### Custom ClassLoader example (sketch)

```java
public class MyClassLoader extends ClassLoader {
    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        byte[] bytes = loadClassFromFile(name);
        return defineClass(name, bytes, 0, bytes.length);
    }

    private byte[] loadClassFromFile(String name) {
        // Custom logic (e.g. read .class bytes from disk or network)
        return ...;
    }
}

ClassLoader loader = new MyClassLoader();
Class<?> cls = loader.loadClass("com.example.MyClass");
```

