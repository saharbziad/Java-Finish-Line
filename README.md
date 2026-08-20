# Java-Finish-Line
all about java 

In Java, you declare a variable by specifying its **type**, then a **name**, and optionally assigning a value:

```java
type variableName = value;
```

**Examples by type:**

```java
int age = 25;                 // integer
double price = 19.99;         // decimal number
boolean isActive = true;      // true/false
char grade = 'A';             // single character
String name = "Alex";         // text (technically an object, not primitive)
long population = 8000000000L; // large integer (note the L suffix)
float temperature = 98.6f;    // decimal, less precise than double (note the f suffix)
```

**Declaring without initializing:**
```java
int score;       // declared, no value yet
score = 100;      // assigned later
```

**Multiple variables at once:**
```java
int x = 1, y = 2, z = 3;
```

**Constants** (can't be reassigned after set):
```java
final double PI = 3.14159;
```

**Naming rules:**
- Must start with a letter, `$`, or `_` (not a number)
- Case-sensitive (`age` and `Age` are different)
- Convention: use camelCase for variables (`firstName`, not `first_name`)
- Can't use reserved keywords (`class`, `public`, `int`, etc.)

**A note on scope** — where you declare it matters:
```java
public class Example {
    int instanceVar = 10;      // instance variable (belongs to object)
    static int classVar = 20;  // static/class variable (shared across all objects)

    void someMethod() {
        int localVar = 30;      // local variable (only exists inside this method)
    }
}
```
