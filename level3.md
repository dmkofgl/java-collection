# Java level 3

## Details

### Core Language

#### Data Types (incl. Arrays)

- **Primitives**: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.
  Java has **8 primitive data types**, which are the basic building blocks for data manipulation. Unlike objects, primitives hold their
  values directly in memory.

| Type      | Size (bits)   | Default Value | Range / Description | Example                |
|-----------|---------------|---------------|---------------------|------------------------|
| `byte`    | 8             | `0`           | -128 to 127         | `byte b = 100;`        |
| `short`   | 16            | `0`           | -32,768 to 32,767   | `short s = 30000;`     |
| `int`     | 32            | `0`           | -2³¹ to 2³¹-1       | `int i = 42;`          |
| `long`    | 64            | `0L`          | -2⁶³ to 2⁶³-1       | `long l = 123456789L;` |
| `float`   | 32            | `0.0f`        | ±3.4e³⁸ (approx)    | `float f = 3.14f;`     |
| `double`  | 64            | `0.0d`        | ±1.7e³⁰⁸ (approx)   | `double d = 3.14159;`  |
| `char`    | 16            | `''`          | Unicode 0 to 65,535 | `char c = 'A';`        |
| `boolean` | JVM-dependent | `false`       | `true` or `false`   | `boolean flag = true;` |

- **Reference Types**: `String`, Arrays, Classes, Enums.

Unlike **primitives** (`int`, `boolean`, etc.), **reference types** store a **reference (memory address)** to the actual object, not the
value itself.

### Main Reference Types

| Type            | Description                        | Example                 |
|-----------------|------------------------------------|-------------------------|
| **Classes**     | Custom or built-in objects         | `String s = "hello";`   |
| **Interfaces**  | Implemented by classes             | `List<String> list;`    |
| **Arrays**      | Fixed-size collection of same type | `int[] nums = {1,2,3};` |
| **Enums**       | Set of named constants             | `enum Day {MON, TUE}`   |
| **Annotations** | Metadata                           | `@Override`             |

- **Arrays**: Zero-based, mutable, fixed-length; supports multidimensional arrays.

Common manipulations include

- iteration,
- copying (`Arrays.copyOf`),
- sorting (`Arrays.sort`),
- searching (`Arrays.binarySearch`),
- and streams (`Arrays.stream`).

### Declaration & Initialization

```java
// Declaration
int[] numbers;
String[] names;

// Initialization
numbers =new int[5];  // [0, 0, 0, 0, 0]
names =new String[3]; // [null, null, null]

// Declaration + Initialization
int[] primes = {2, 3, 5, 7, 11};
String[] colors = new String[]{"red", "green", "blue"};

// Multi-dimensional arrays
int[][] matrix = {
	{1, 2, 3},
	{4, 5, 6},
	{7, 8, 9}
};

int[] arr = {10, 20, 30, 40, 50};

// Access elements
int first = arr[0];        // 10
int last = arr[arr.length - 1]; // 50

// Modify elements
arr[2]=99; // [10, 20, 99, 40, 50]

// Length
int size = arr.length; // 5
```

Copying

```java
int[] source = {1, 2, 3, 4, 5};

// Method 1: Arrays.copyOf
int[] copy1 = Arrays.copyOf(source, source.length);

// Method 2: Arrays.copyOfRange
int[] partial = Arrays.copyOfRange(source, 1, 4); // [2, 3, 4]

// Method 3: System.arraycopy
int[] copy2 = new int[source.length];
System.

arraycopy(source, 0,copy2, 0,source.length);

// Method 4: clone() - shallow copy
int[] copy3 = source.clone();
```

Sorting

```java
int[] numbers = {5, 2, 8, 1, 9};
Arrays.

sort(numbers); // [1, 2, 5, 8, 9]

// Sort substring
String[] words = {"banana", "cherry", "apple"};
Arrays.

sort(words, 1,3); // ["banana", "apple", "cherry"]

// Custom sorting with Comparator
Arrays.

sort(words, String.CASE_INSENSITIVE_ORDER);
```

Searching

```java
int[] sorted = {1, 3, 5, 7, 9};
int index = Arrays.binarySearch(sorted, 5); // 2
int notFound = Arrays.binarySearch(sorted, 4); // -3 (insertion point)
```

Filling

```java
int[] arr = new int[10];
Arrays.fill(arr, 7); // All elements = 7

// Fill range
Arrays.fill(arr, 2,6,-1); // Elements 2-5 = -1
```

To string

```java
int[] arr = {1, 2, 3};
System.out.println(Arrays.toString(arr)); // [1, 2, 3]
System.out.println(Arrays.deepToString(matrix)); // For 2D arrays
```

Notes:

- Array should be sorted.
- Insertion point - index at which this value expected ( where to insert, to keep ordering)
- If has multiple suitable value, there is no guarantee which one will be found

#### Control Statements

- **Branching**: `if`, `else`, `switch` (supports String, enum, primitives).
- **Looping**: `for`, `while`, `do-while`, enhanced for-each loop (`for(Type var : array/collection)`).
- **Branching/Flow**: `break`, `continue`, `return`, exception handling with `try/catch/finally`.

#### Object-Oriented Programming (OOP)

- **Four Main Principles**:
    - **Encapsulation**: Hiding internal state via access modifiers, providing methods for interaction.
    - **Abstraction**: Interfaces and abstract classes define contracts/behavior without implementation details.
    - **Inheritance**: Classes can extend one class, inheriting fields/methods (`extends`).
    - **Polymorphism**: Supports runtime (method overriding) and compile-time (method overloading) polymorphism; enables interface-based
      programming.
- **Classes & Members**: Classes contain fields (variables), methods, constructors, nested types. Members use modifiers:

- **Common modifiers (classes, methods, fields)**:
  - `static` — belongs to the class, not instances.
  - `final` — (field) cannot be modified; (method) cannot be overridden; (class) cannot be subclassed.
  - `abstract` — must be implemented by subclasses; cannot be instantiated.
  - `synchronized` — method locked for thread safety.
  - `native` — implemented in native (non-Java) code. ( methods only)
  - `strictfp` — enforces strict floating-point behavior.

- **For classes and interfaces**:
  - `static` — only for nested types (defines a static nested class).
  - `sealed` — (Java 17+) restricts which classes can extend or implement it.
  - `non-sealed` — explicitly allows extension when inside a sealed hierarchy.

- **Field-specific modifiers**:
  - `volatile` — value is always read from main memory (ensures visibility across threads).
  - `transient` — skipped during serialization.

- **Abstract Classes & Interfaces**: Abstract classes allow partial abstraction; interfaces are 100% abstract (default/static methods
  allowed since Java 8). Multiple interfaces can be implemented.
- **Nested/Inner Classes**: Static and non-static inner classes, local/anonymous classes for encapsulation and event handling.
    - Static class can see only static fields\methods of outer.
- **Lambdas**: Java 8+, enabling functional-style programming and concise implementation of single-method interfaces (functional interfaces,
  e.g., `Runnable`, `Comparator`).
- **Inheritance & Polymorphism Details**: Ability to extend/override methods, use `@Override` for safety, upcasting/downcasting, dynamic
  binding.

### Running Java Programs

#### Tooling

`javac` for compilation, `java` for running. IDEs (IntelliJ IDEA, Eclipse) provide richer tools. Build tools (Maven, Gradle)
automate compiling, testing, packaging.

- cmd\bash commands
    - javac
    - java
    - jar
- Build Tools
    - maven
    - gradle
    - ant

#### Classpath

Set of locations the JVM uses to find compiled classes/resources. Managed using `-cp` or `CLASSPATH` env variable. Supports
directories, jars, wildcards.

#### JAR Deployment

A JAR (Java ARchive) is a package file format that aggregates many Java class files, associated metadata, and resources (text, images,
etc.) into a single file. It is the standard way to distribute and deploy Java applications, libraries, and components.

JAR Deployment refers to the process of packaging a Java application into a JAR (Java ARchive) file and then deploying it so it can be run
or distributed easily.

#### Classloading

Classloading is the process by which the Java Virtual Machine (JVM) loads Java classes (.class files) into memory so they can be executed.

When you run a Java program, the JVM doesn’t load all classes at once — it loads them on demand, using special components called
ClassLoaders.

JVM loads classes dynamically from classpath using built-in or custom class loaders. Supports parent delegation model
for security and isolation.

A ClassLoader is a part of the JVM responsible for:

1. Locating class files (from disk, JARs, network, etc.)

1. Loading them into memory

1. Defining them in the JVM so code can use them

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

- Bootstrap ClassLoader

  The root loader, part of the JVM itself (written in native code).
  Loads core Java classes from the JAVA_HOME/lib directory (like java.lang.*, java.util.*).
- Extension / Platform ClassLoader

  Loads classes from the JRE extensions (JAVA_HOME/lib/ext) or module path.
  Loads platform APIs like javax.* or newer jdk.* modules.
- Application / System ClassLoader

  Loads classes from your application’s classpath (e.g. /bin, /target/classes, or JARs in /lib).
  Used for your main application code.
- Custom ClassLoaders

  You can create your own by extending ClassLoader.
  Often used in application servers (Tomcat, JBoss, OSGi) or plugin systems to isolate different modules or reload classes dynamically.

When a classloader is asked to load a class:

1. It first delegates the request to its parent.
2. If the parent can’t find it, it tries to load it itself.

This ensures that:

- Core classes aren’t overridden by user code.
- Duplicate classes aren’t loaded unnecessarily.

  Example:

When you write: `Class.forName("java.util.HashMap");` The Application ClassLoader will delegate up:

- → Platform ClassLoader
- → Bootstrap ClassLoader (finds it in rt.jar)
- Class is loaded.

You can define your own ClassLoader to load classes from a specific location:

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
...

ClassLoader loader = new MyClassLoader();
Class<?> cls = loader.loadClass("com.example.MyClass");

```

### Generics

Java Generics let you parameterize types — you can write code that handles any object type while keeping strong compile-time type checking.
They were introduced in Java 5 (JDK 1.5) to eliminate unsafe type casts and provide cleaner, type-safe APIs (especially for collections).

#### Basic generics usage

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
...

Box<Integer> intBox = new Box<>();
intBox.

set(10);
System.out.

println(intBox.get()); // 10

Box<String> strBox = new Box<>();
strBox.

set("Hello");
System.out.

println(strBox.get()); // Hello

```

Methods themselves can be generic — independent of whether the class is generic.

```java
public class Util {

	public static <T> void printArray(T[] array) {
		for (T elem : array) {
			System.out.print(elem + " ");
		}
		System.out.println();
	}

	public static void main(String[] args) {
		printArray(new Integer[]{1, 2, 3});
		printArray(new String[]{"A", "B", "C"});
	}
}

```

#### Wildcards, super/extends bound

Wildcards (?) allow you to specify flexible generic type relationships — especially useful in methods that accept collections of various
element types.

| Wildcard      | Meaning                             | Example                  |
|---------------|-------------------------------------|--------------------------|
| `?`           | Unknown type                        | `List<?> list`           |
| `? extends T` | Any type that *is a subtype of* T   | `List<? extends Number>` |
| `? super T`   | Any type that *is a supertype of* T | `List<? super Integer>`  |

- ? (Unbounded Wildcard)

Used when you only need to work with an object generically:

```java
public void printList(List<?> list) {
	for (Object obj : list)
		System.out.println(obj);
}
```

- ? extends (Upper Bound)

Used when you read data from a structure but don’t modify it.

```java
public void printNumbers(List<? extends Number> list) {
	for (Number n : list)
		System.out.println(n);
}
```

- ? super (Lower Bound)

Used when you write data (add elements) but don’t care about the exact supertype.

```java
public void addNumbers(List<? super Integer> list) {
	list.add(10);
	list.add(20);
}
```

#### Type erasure & reification

Java’s generics are implemented using type erasure to maintain backward compatibility with older, non-generic code.
At compile time, generic types are erased and replaced by their upper bound (or Object if unbounded).

For example: `Box<Integer> intBox = new Box<>();` is compiled roughly as: `Box box = new Box();`

```java
List<Integer> a = new ArrayList<>();
List<String> b = new ArrayList<>();
System.out.

println(a.getClass() ==b.

getClass()); // true
```

Reification (Contrast)

Some languages like Kotlin or C# support reified generics, where type parameters are available at runtime (Java does not).
Java’s generics are non-reified — the type parameters are lost after compilation.

#### Reflection and Generics

Even though runtime type information is erased, reflection allows access to the declarations of generic parameters in class files (via
metadata).
Java Reflection API can be used to inspect generic types at runtime (though with some limits due to erasure).

```java
import java.lang.reflect.*;

class Sample<E> {

	List<E> list;

	public <T> void process(T item) {
	}
}

public class Main {

	public static void main(String[] args) throws Exception {
		Field field = Sample.class.getDeclaredField("list");
		Type type = field.getGenericType();

		if (type instanceof ParameterizedType pType) {
			Type[] typeArgs = pType.getActualTypeArguments();
			System.out.println("Type argument: " + typeArgs[0]);
		}

		Method method = Sample.class.getMethod("process", Object.class);
		TypeVariable<Method>[] typeParams = method.getTypeParameters();
		System.out.println("Type parameter: " + typeParams[0].getName()); // T
	}
}
```

### Enums

In Java, an enum (short for enumeration) is a special data type that represents a fixed set of constants — for example, days of the week,
directions, colors, etc.

```java
enum Day {
	SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}
```

Features of Enums

- Type-Safe Constants
    - Unlike final static variables, enums provide compile-time type safety.

- Implicit static and final
    - Enum constants are implicitly public static final.

- Enums Can Have Methods and Fields
    - You can add fields, constructors, and methods.

Notes:

- Enums cannot be extended (they implicitly extend java.lang.Enum).
- You can implement interfaces with enums.
- Enums are singleton-like for each constant — only one instance of each exists.

### Annotations

Annotations are metadata added to Java code (classes, methods, fields, parameters, etc.) to provide additional information to the compiler
or runtime tools.

They do not directly affect the code execution, but tools and frameworks can use them to generate code, perform validations, or configure
behavior.

`@AnnotationName`

| Annotation             | Purpose                                                      | Example                                                             |
|------------------------|--------------------------------------------------------------|---------------------------------------------------------------------|
| `@Override`            | Indicates that a method overrides a method from a superclass | `java @Override public String toString() { return "Example"; } `    |
| `@Deprecated`          | Marks a method/class as deprecated                           | `java @Deprecated public void oldMethod() {} `                      |
| `@SuppressWarnings`    | Suppresses compiler warnings                                 | `java @SuppressWarnings("unchecked") List list = new ArrayList(); ` |
| `@FunctionalInterface` | Ensures interface has exactly one abstract method            | `java @FunctionalInterface interface MyFunc { void run(); } `       |
| `@SafeVarargs`         | Suppresses unchecked warnings for varargs                    | `java @SafeVarargs final void printAll(T... args) {} `              |

```java
class Parent {

	void display() {
		System.out.println("Parent display");
	}
}

class Child extends Parent {

	@Override
		// ensures method overrides correctly
	void display() {
		System.out.println("Child display");
	}

	@Deprecated
	void oldMethod() {
		System.out.println("Old method");
	}

	@SuppressWarnings("unchecked")
	void uncheckedMethod() {
		List list = new ArrayList();
		list.add("Hello");
	}
}
```

#### Creating Your Own Custom Annotation

```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAnnotation {

	String value() default "default";

	int count() default 1;
}
```

Notes:

- `@Retention`: Specifies when the annotation is available (SOURCE, CLASS, or RUNTIME).
- `@Target`: Specifies where the annotation can be applied (METHOD, FIELD, TYPE, etc.).
- Annotation members are defined like methods (String value();).

```java
class Test {

	@MyAnnotation(value = "Hello", count = 5)
	void myMethod() {
		System.out.println("Annotated method");
	}
}
...

public class Main {

	public static void main(String[] args) throws Exception {
		Method method = Test.class.getMethod("myMethod");

		if (method.isAnnotationPresent(MyAnnotation.class)) {
			MyAnnotation ann = method.getAnnotation(MyAnnotation.class);
			System.out.println("Value: " + ann.value());
			System.out.println("Count: " + ann.count());
		}
	}
}


```

### Exception Handling

An exception is an event that disrupts the normal flow of the program.Exception handling in Java allows a program to gracefully handle
runtime errors without crashing.

#### try/catch mechanism

The most basic form of exception handling:

```java
public class TryCatchExample {

	public static void main(String[] args) {
		try {
			int result = 10 / 0; // this will throw ArithmeticException
			System.out.println(result);
		} catch (ArithmeticException e) {
			System.out.println("Error: Division by zero is not allowed!");
			e.printStackTrace(); // optional: print detailed error
		} catch (ArrayIndexOutOfBoundsException e) {
			System.out.println("Array index error");
		} finally {
			System.out.println("This will always execute.");
		}
	}
}
```

If exception happens in catch block finally runs, then new exception propagates

#### try with resources (Java 7+)

When working with resources like files, sockets, or database connections, you must close them to avoid resource leaks. Java 7 introduced
try-with-resources, which automatically closes resources. Resources must implement `AutoCloseable` interface.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class TryWithResourcesExample {

	public static void main(String[] args) {
		try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
			String line;
			while ((line = br.readLine()) != null) {
				System.out.println(line);
			}
		} catch (IOException e) {
			System.out.println("File reading error: " + e.getMessage());
		}
	}
}

```

#### exception class & exceptions hierarchy (standard exceptions)

```
Throwable
 ├── Error
 └── Exception
      ├── RuntimeException (unchecked exceptions)
      │    ├── NullPointerException
      │    ├── ArithmeticException
      │    ├── ArrayIndexOutOfBoundsException
      │    └── IllegalArgumentException
      └── Checked Exceptions
           ├── IOException
           ├── SQLException
           └── ClassNotFoundException

```

Types of Exceptions:

- Checked Exceptions:

    - Checked at compile-time.

    - Must be either caught or declared using throws.

  Example: IOException, SQLException

- Unchecked Exceptions (Runtime Exceptions):

    - Checked at runtime.

    - Usually caused by programming errors.

  Example: ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException

- Errors:

  Serious problems not meant to be caught.

  Example: OutOfMemoryError, StackOverflowError

### Core Libraries

#### Object

The root of the Java class hierarchy.Every class in Java implicitly extends Object.

Key methods:

- toString(): Returns string representation.

- equals(Object obj): Checks object equality.

- hashCode(): Returns hash code for hashing collections.

- clone(): Creates a shallow copy.

- finalize(): Called by garbage collector before destruction.

#### Objects

Utility class to operate on objects (null-safe operations).

Key methods:

- Objects.requireNonNull(obj): Throws NPE if null.
- Objects.equals(a, b): Null-safe equality check.
- Objects.hash(a, b, ...): Generates hash code.

#### System

Provides access to system resources and operations.

Key fields/methods:

- System.out, System.err, System.in
- System.currentTimeMillis(); Returns the current time in milliseconds since January 1, 1970 UTC (Unix epoch).
- System.gc(); Request the garbage collector in the Java Virtual Machine. This is only a request, not a command. JVM may ignore it.
- System.exit(status); Terminates the JVM immediately.

#### Cloneable

Marker interface indicating a class allows field-for-field copying.
Works with Object.clone().

```java
class MyClass implements Cloneable {

	int value;

	public Object clone() throws CloneNotSupportedException {
		return super.clone();
	}
}

```

#### Math

Provides mathematical functions.

Key methods:

- abs(),
- sqrt(),
- pow(),
- random(),
- sin(),
- cos().

#### AutoCloseable

Classes implementing it can be used in try-with-resources.

Ensures automatic resource cleanup (like streams, DB connections).

```java
try(BufferedReader br = new BufferedReader(new FileReader("file.txt"))){
	System.out.

println(br.readLine());
	}

```

#### Optional

Container object that may or may not contain a value.

Helps avoid null checks and NullPointerException.

```java
Optional<String> name = Optional.ofNullable(null);
System.out.

println(name.orElse("Default Name")); // Default Name

```

#### Random

Generates pseudo-random numbers.

Methods: nextInt(), nextDouble(), nextBoolean().

```java
Random rand = new Random();
int n = rand.nextInt(100); // random number between 0-99

```

#### Timer + TimerTask

Timer schedules a task for future execution.

TimerTask represents the task to run.

```java
Timer timer = new Timer();
timer.

schedule(new TimerTask() {
	public void run () {
		System.out.println("Task executed");
	}
},1000); // delay 1 second

```

#### Formatter + formatting dates

Provides formatting support for strings, numbers, dates, etc.

Can be used via String.format() or Formatter class.

Dates:

```java
  public static void main(String[] args) {
	LocalDate date = LocalDate.now();
	LocalDateTime dateTime = LocalDateTime.now();

	// Custom format
	DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
	DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("dd-MMM-yyyy HH:mm:ss");

	System.out.println("Formatted Date: " + date.format(dateFormatter));
	System.out.println("Formatted DateTime: " + dateTime.format(dateTimeFormatter));

	// ISO format (default)
	System.out.println("ISO Date: " + date);
	System.out.println("ISO DateTime: " + dateTime);

	double pi = 3.14159;
	System.out.println(String.format("%.2f", pi));  // 2 decimal places
	System.out.println(String.format("%,d", 1000000)); // 1,000,000
	System.out.println(String.format("%,d", 1000000)); // 1,000,000

	// Currency
	double amount = 12345.67;

	NumberFormat currencyFormatter = NumberFormat.getCurrencyInstance(Locale.US);
	System.out.println("US: " + currencyFormatter.format(amount));

	currencyFormatter = NumberFormat.getCurrencyInstance(Locale.JAPAN);
	System.out.println("Japan: " + currencyFormatter.format(amount));
}
```

Numbers:

```java
 public static void main(String[] args) {
	double number = 1234567.89123;

	DecimalFormat df = new DecimalFormat("#,###.00");  // thousands separator + 2 decimals
	System.out.println("Formatted Number: " + df.format(number));

	DecimalFormat df2 = new DecimalFormat("000000");  // leading zeros
	System.out.println("Padded Number: " + df2.format(123));
}
```

#### Base64

Encode/decode binary data into/from Base64 strings.

Useful for encoding images, credentials, etc.

```java
String encoded = Base64.getEncoder().encodeToString("hello".getBytes());
String decoded = new String(Base64.getDecoder().decode(encoded));

```

#### UUID (what is uuid, support for uuid generation)

Universally Unique Identifier.

Used to generate unique identifiers for objects, transactions, etc.

``` java
UUID uuid = UUID.randomUUID();
System.out.println(uuid); // e.g., 123e4567-e89b-12d3-a456-426614174000
```

#### String Manipulation Classes

##### String

Immutable sequence of characters.

Common methods: length(), charAt(), substring(), concat(), equals(), replace(), split().

##### StringBuilder

Mutable sequence of characters.

Faster than String for frequent modifications.

Methods: append(), insert(), delete(), reverse().

##### StringBuffer

Like StringBuilder, but thread-safe (synchronized).

Slightly slower than StringBuilder.

StringJoiner

Used to join strings with a delimiter.

Can include prefix/suffix.

### Internationalization (i18n)

Java provides a robust Internationalization (i18n) framework through the java.util and java.text packages, enabling applications to support
multiple languages, regions, and cultural conventions without code changes

- Locale – Represents language + region (e.g., en_US, fr_FR, zh_CN)
- ResourceBundle – Stores localized strings, messages, etc.
- MessageFormat – Formats messages with placeholders
- NumberFormat, DateFormat – Format numbers, currencies, dates
- Collator – Locale-sensitive string comparison

```java
import java.util.Locale;

// Create Locale
Locale us = new Locale("en", "US");
	Locale france = new Locale("fr", "FR");
	Locale china = Locale.CHINA; // built-in constant
	Locale defaultLocale = Locale.getDefault();

	// Language tags (RFC 4646)
	Locale germany = Locale.forLanguageTag("de-DE");
```

Example File Structure (in src/main/resources)

- messages.properties          (default)
- messages_en.properties
- messages_en_US.properties
- messages_fr.properties
- messages_fr_FR.properties

```java
import java.util.ResourceBundle;
import java.util.Locale;

Locale locale = new Locale("fr", "FR");
ResourceBundle bundle = ResourceBundle.getBundle("messages", locale);

System.out.

println(bundle.getString("greeting")); // Bonjour, {0} !
```

Hierarchy: messages_fr_FR → messages_fr → messages_en (default\system locale) → messages

Formatting:

```java
String name = "Alice";
String pattern = bundle.getString("greeting");
MessageFormat formatter = new MessageFormat(pattern, locale);
String message = formatter.format(new Object[]{name});

System.out.

println(message); // Bonjour, Alice !

double amount = 1234567.89;

Locale locale = Locale.GERMANY;
NumberFormat currencyFmt = NumberFormat.getCurrencyInstance(locale);
NumberFormat numberFmt = NumberFormat.getNumberInstance(locale);

System.out.

println(currencyFmt.format(amount)); // 1.234.567,89 €
	System.out.

println(numberFmt.format(amount));  // 1.234.567,89


Date now = new Date();

DateFormat df = DateFormat.getDateInstance(DateFormat.FULL, Locale.FRANCE);
System.out.

println(df.format(now)); // vendredi 14 novembre 2025
// or java 8+
DateTimeFormatter dtf = DateTimeFormatter.ofPattern("EEEE, MMMM d, yyyy", Locale.FRANCE);
System.out.

println(dtf.format(LocalDateTime.now()));

```

String comparison:

```java
Collator collator = Collator.getInstance(Locale.GERMANY);
collator.

setStrength(Collator.PRIMARY);

int result = collator.compare("Äpfel", "apfel"); // considers Ä = A
System.out.

println(result); // 0 (equal at PRIMARY strength)
```

### Serialization Support

Serialization in Java is the process of converting an object into a byte stream so it can be:

- saved to disk,
- transmitted over a network,
- or otherwise stored/transported.

Deserialization is the reverse: turning the byte stream back into a live object.

Java provides automatic serialization via the java.io.Serializable marker interface.
Key points:

- No methods to implement.
- Fields are serialized automatically unless marked transient.
- Java uses ObjectOutputStream / ObjectInputStream.

```java 
class Person implements java.io.Serializable {

	private String name;
	private int age;
	// transient fields are skipped
	private transient String password;
}
...
	try(
ObjectOutputStream oos = new ObjectOutputStream(
	new FileOutputStream("person.ser"))){
	oos.

writeObject(new Person("Alice", 30));
	}

	try(
ObjectInputStream ois = new ObjectInputStream(
	new FileInputStream("person.ser"))){
Person p = (Person) ois.readObject();
}
```

### Stream API

The Java Stream API (introduced in Java 8) is a framework for processing sequences of data in a declarative, functional style. It allows
operations such as filtering, mapping, reducing, and collecting without modifying the underlying data source.

- **Concepts**: Streams represent sequences of elements, enabling functional-style operations on collections (map/filter/reduce).
  Distinction: Collections store data, streams process data.

A Stream operation is usually a pipeline of:

- Source (collection, array, I/O channel, generator)
- Intermediate operations (return a new stream)
    - Intermediate operations are not executed immediately. They run only when a terminal operation is invoked.
- Terminal operation (produces a result)

Example:

```
numbers.stream()
.filter(n -> n % 2 == 0)   // intermediate
.sorted()                 // intermediate
.forEach(System.out::println); // terminal
```

Streams do not change the original collection.

For easy multicore processing can be sequential or parallel:

```
list.parallelStream()
.filter(x -> x > 100)
.count();
```

//TODO how works under the hood

##### Types of Stream Operations:

Intermediate operations (return Stream)

- filter()
- map()
- flatMap()
- distinct()
- sorted()
- peek()
- takeWhile()
- dropWhile()
- limit() / skip()

Terminal operations (return result)

- forEach()
- collect()
- reduce()
- count()
- findFirst(), findAny()
- anyMatch(), allMatch(), noneMatch()

- **Lazy vs Terminal Ops**: Lazily compute results and optimize chains; terminal ops trigger processing (e.g., `collect`, `forEach`).

##### Gatherer
