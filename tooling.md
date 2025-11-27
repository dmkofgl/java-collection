# Tooling & Running Java Programs

## Tooling

`javac` for compilation, `java` for running. IDEs (IntelliJ IDEA, Eclipse) provide richer tools. Build tools (Maven, Gradle) automate compiling, testing, packaging.

- Quick commands / examples

```bash
# Compile single file
javac -d out src/com/example/Main.java

# Compile whole module/source tree (with classpath)
javac -d out -cp "lib/*" $(find src -name "*.java")

# Run (with classpath)
java -cp out:lib/* com.example.Main

# Run with JVM options (memory, system properties)
java -Xms256m -Xmx2g -Dconfig.file=prod.properties -cp out:lib/* com.example.Main

# Enable assertions
java -ea -cp out com.example.Main

# Inspect bytecode / API
javap -c -p com.example.Main
```

### Useful JDK tools
- `jshell` — REPL for quick experiments (Java 9+).
- `jlink` — create a custom runtime image (modular apps).
- `jpackage` — native installers for desktop apps (since JDK 14+ / incubating earlier).
- `jcmd`, `jstack`, `jmap`, `jinfo` — diagnostics (thread dumps, heap, JVM flags).
- `jstat` — GC and JVM statistics.
- `jdeps` — dependency analysis for JARs / modules.
- `jconsole`, `jvisualvm` — profiling and monitoring GUI tools.

### JVM common runtime flags
- Memory: `-Xms<size>` (initial), `-Xmx<size>` (max).
- GC tuning: `-XX:+UseG1GC`, `-XX:+UseZGC` (JDK versions permitting), `-XX:MaxGCPauseMillis=200`.
- Diagnostics: `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/heap.hprof`.
- System properties: `-Dname=value`.
- Debugging: `-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005`.

### Creating and running JARs

```bash
# Create a simple JAR
jar cfm app.jar MANIFEST.MF -C out/ .

# Run an executable JAR
java -jar app.jar

# Create 'fat' or 'uber' JAR (example using Gradle/Maven/plugins)
# For manual assembly, extract deps and jar together (not recommended long term)
```

### Maven

```bash
mvn clean install        # compile, test, package, install to local repo
mvn -DskipTests package  # package without running tests
mvn test                 # run unit tests (Surefire/Failsafe)
mvn dependency:tree     # view dependency graph
```

### Gradle (wrapper recommended)

```bash
./gradlew build          # compile, test, assemble
./gradlew test           # run tests
./gradlew clean build
./gradlew bootJar        # Spring Boot: build executable jar
./gradlew dependencies  # view dependency graph
```

### IDE tips
- Set `JAVA_HOME` to the JDK installation used by the IDE and CI.
- Use IDE run configs to pass JVM args, system properties, and env vars.
- Use built-in debuggers (breakpoints, evaluate expressions) instead of `jdb` for faster workflow.

### Testing & quality
- JUnit (5+) is the standard for unit tests; use Surefire (Maven) or the Gradle test task.
- Static analysis: `spotbugs`, `checkstyle`, `pmd`.
- Formatting: `google-java-format`, `spotless` (Gradle/Maven plugins).

### CI / reproducibility
- Pin JDK version in CI (GitHub Actions, GitLab CI) and use build tool wrapper (`./gradlew`) or `mvn -B`.
- Cache dependency directories (Maven `.m2`, Gradle `.gradle`) for faster builds.

### Troubleshooting
- Classpath errors: check `-cp` ordering and module-path vs classpath (modules reduce ambiguity).
- Version mismatch: ensure runtime JRE >= compiled target (javac `--release` or `-target`/`-source`).
- OutOfMemory: inspect heap with `jmap -dump:live,format=b,file=heap.hprof <pid>` and analyze with VisualVM or Eclipse MAT.

### Where to get the JDK
- AdoptOpenJDK / Temurin, Oracle JDK, Amazon Corretto, Azul Zulu. Choose a distribution and version supported by your project.

