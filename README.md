# Java-Finish-Line

#CORE 

**1-1 Declare variable**

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

**1-2  String Concatenation** 

**String concatenation** means joining two or more strings together into one. In Java, there are several ways to do it:

**1. Using the `+` operator** (most common)
```java
String first = "Hello";
String second = "World";
String result = first + " " + second;  // "Hello World"
```

You can also mix strings with other types — Java automatically converts them:
```java
String message = "Age: " + 25;        // "Age: 25"
String info = "Score: " + 99.5;       // "Score: 99.5"
```

**2. Using `+=`** (append to an existing string)
```java
String greeting = "Hello";
greeting += " there!";   // greeting is now "Hello there!"
```

**3. Using `concat()` method**
```java
String first = "Hello";
String second = "World";
String result = first.concat(" ").concat(second);  // "Hello World"
```

**4. Using `StringBuilder`** (best for combining many strings, e.g. in a loop)
```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
String result = sb.toString();  // "Hello World"
```

Why does `StringBuilder` matter? In Java, **Strings are immutable** — every time you use `+` to combine strings, it actually creates a brand new String object behind the scenes rather than modifying the original. That's fine for a few concatenations, but if you're doing it hundreds or thousands of times (like inside a loop), it gets wasteful. `StringBuilder` avoids this by building the string in a mutable buffer, only converting to a final `String` at the end.

**Example: bad vs. good in a loop**
```java
// Inefficient — creates many intermediate String objects
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i + ", ";
}

// Efficient — modifies one buffer
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i).append(", ");
}
String result = sb.toString();
```
