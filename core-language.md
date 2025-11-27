# Core Language

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

### Control Statements

- **Branching**: `if`, `else`, `switch` (supports String, enum, primitives).
- **Looping**: `for`, `while`, `do-while`, enhanced for-each loop (`for(Type var : array/collection)`).
- **Branching/Flow**: `break`, `continue`, `return`, exception handling with `try/catch/finally`.

### Object-Oriented Programming (OOP)

- **Four Main Principles**:
    - **Encapsulation**: Hiding internal state via access modifiers, providing methods for interaction.
    - **Abstraction**: Interfaces and abstract classes define contracts/behavior without implementation details.
    - **Inheritance**: Classes can extend one class, inheriting fields/methods (`extends`).
    - **Polymorphism**: Supports runtime (method overriding) and compile-time (method overloading) polymorphism; enables interface-based
      programming.
- **Classes & Members**: Classes contain fields (variables), methods, constructors, nested types. Members use modifiers.

(See the rest of the document for examples and deeper topics.)

