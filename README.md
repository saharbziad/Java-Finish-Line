# Java-Finish-Line

##CORE##

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


**1-3 Reading inputs from the console **


In Java, the most common way to read input from the console is using the **`Scanner`** class.

**1. Basic setup**
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();
        
        System.out.println("Hello, " + name + "!");
        
        scanner.close();  // good practice to close when done
    }
}
```

**2. Reading different data types**

`Scanner` has different methods depending on what type of input you expect:

```java
Scanner scanner = new Scanner(System.in);

System.out.print("Enter your age: ");
int age = scanner.nextInt();

System.out.print("Enter your height (in meters): ");
double height = scanner.nextDouble();

System.out.print("Are you a student? (true/false): ");
boolean isStudent = scanner.nextBoolean();

System.out.print("Enter your name: ");
scanner.nextLine();  // ⚠️ needed to consume leftover newline — see below
String name = scanner.nextLine();
```

| Method | Reads |
|---|---|
| `nextLine()` | a full line of text (String) |
| `next()` | a single word (stops at whitespace) |
| `nextInt()` | an integer |
| `nextDouble()` | a decimal number |
| `nextBoolean()` | true/false |
| `nextLong()` | a long integer |

**3. The classic "leftover newline" gotcha**

This trips up almost everyone at some point. When you call `nextInt()`, `nextDouble()`, etc., it reads the *value* but leaves the newline character (`\n`) in the input buffer. If you then call `nextLine()`, it immediately grabs that leftover newline instead of waiting for new input — so it looks like it "skipped" your input.

```java
Scanner scanner = new Scanner(System.in);

System.out.print("Enter your age: ");
int age = scanner.nextInt();  // leaves "\n" in the buffer

System.out.print("Enter your name: ");
String name = scanner.nextLine();  // grabs the leftover "\n" — name ends up empty!
```

**Fix:** add an extra `scanner.nextLine()` to consume the leftover newline before reading the next line:
```java
int age = scanner.nextInt();
scanner.nextLine();  // consume leftover newline
String name = scanner.nextLine();  // now works correctly
```

**4. Reading multiple values on one line**
```java
System.out.print("Enter three numbers separated by spaces: ");
int a = scanner.nextInt();
int b = scanner.nextInt();
int c = scanner.nextInt();
```

**5. Handling bad input (optional but useful)**
```java
System.out.print("Enter a number: ");
if (scanner.hasNextInt()) {
    int num = scanner.nextInt();
    System.out.println("You entered: " + num);
} else {
    System.out.println("That's not a valid number!");
}
```
**1-4 print vs. println **


Both are used to display output to the console, but they differ in one key way:

**`print()`** — outputs text **without** moving to a new line afterward
```java
System.out.print("Hello");
System.out.print("World");
```
Output:
```
HelloWorld
```
(Both stay on the same line, right next to each other.)

**`println()`** — outputs text **and then moves to a new line** afterward
```java
System.out.println("Hello");
System.out.println("World");
```
Output:
```
Hello
World
```
(Each call starts a fresh line.)

**Side-by-side comparison**
```java
System.out.print("A");
System.out.print("B");
System.out.print("C");
// Output: ABC

System.out.println("A");
System.out.println("B");
System.out.println("C");
// Output:
// A
// B
// C
```

**Mixing them**
```java
System.out.print("Name: ");
String name = "Alex";
System.out.println(name);
// Output: Name: Alex   (on one line, because print() didn't break the line)
```

This is actually a really common pattern — using `print()` for a label/prompt so the next thing appears right after it, then `println()` to finish the line.

**Quick tip:** `println()` with no arguments just prints an empty line (like pressing Enter):
```java
System.out.println("First line");
System.out.println();  // blank line
System.out.println("Second line");
```

**1-5 specific vs. wildcard imports **


In Java, `import` statements let you use classes from other packages without typing the full package path every time. There are two ways to do it:

**1. Specific import** — imports exactly one class
```java
import java.util.Scanner;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<String> list = new ArrayList<>();
    }
}
```

**2. Wildcard import** — imports *all* classes from a package using `*`
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ArrayList<String> list = new ArrayList<>();
        HashMap<String, Integer> map = new HashMap<>();
        // all available without individual imports
    }
}
```

**Without either, you'd have to write the full path every time:**
```java
java.util.Scanner scanner = new java.util.Scanner(System.in);
```
That's why imports exist — they save you from typing this repeatedly.

**Comparison**

| | Specific import | Wildcard import |
|---|---|---|
| Syntax | `import java.util.Scanner;` | `import java.util.*;` |
| Imports | One class | All classes in that package |
| Clarity | Clear exactly what's used | Less clear which classes come from where |
| Compile time | Slightly faster (technically) | Negligible difference in practice |
| Name conflicts | Rare | More likely if two packages have same class name |

**A gotcha with wildcards: naming conflicts**
```java
import java.util.*;
import java.sql.*;

Date d = new Date();  // ❌ Error! Both java.util and java.sql have a "Date" class
                        // Java doesn't know which one you mean
```
In this case, you'd need to specify the full path anyway:
```java
java.util.Date d = new java.util.Date();
```

**Important: wildcard doesn't include subpackages**
```java
import java.util.*;  // gets Scanner, ArrayList, HashMap, etc.
// but does NOT get java.util.concurrent.* — that's a separate subpackage
```

**Which should you use?**

Most style guides and teams (and tools like IDEs by default) prefer **specific imports**, because:
- It's clear exactly which classes your code depends on
- Avoids naming conflicts
- Easier for others to read your code and know what's being used

Wildcard imports are more common in quick scripts, examples, or when you're importing many classes from the same package and don't want a long list at the top.

**One more thing — you don't need to import everything.** Classes in `java.lang` (like `String`, `System`, `Math`) are available automatically, no import needed:
```java
public class Main {
    public static void main(String[] args) {
        String s = "Hello";     // no import needed
        System.out.println(s);  // no import needed
        Math.sqrt(16);           // no import needed
    }
}
```

**1-6 identifiers **


In Java, an **identifier** is simply the name you give to things in your code — variables, methods, classes, interfaces, packages, etc. Anytime you're naming something, you're creating an identifier.

```java
int age = 25;              // "age" is an identifier
String firstName = "Alex"; // "firstName" is an identifier
class Employee { }          // "Employee" is an identifier
void calculateTotal() { }   // "calculateTotal" is an identifier
```

**Rules for valid identifiers** (the compiler enforces these — break them and your code won't compile)

1. **Can contain:** letters (a-z, A-Z), digits (0-9), underscore (`_`), and dollar sign (`$`)
2. **Cannot start with a digit**
3. **Cannot contain spaces**
4. **Cannot be a reserved keyword** (like `int`, `class`, `public`, `if`, `while`, etc.)
5. **Case-sensitive** — `age`, `Age`, and `AGE` are three different identifiers

```java
// ✅ Valid identifiers
int age;
int _count;
int $price;
int total1;
int firstName;

// ❌ Invalid identifiers
int 1total;      // can't start with a digit
int first name;  // can't contain a space
int class;       // "class" is a reserved keyword
int total-1;     // hyphen isn't allowed
```

**Naming conventions** (not enforced by the compiler, but expected by convention — breaking these won't cause errors, but it makes your code look unprofessional or confusing to other Java developers)

| Type | Convention | Example |
|---|---|---|
| Variables & methods | camelCase | `firstName`, `calculateTotal()` |
| Classes & interfaces | PascalCase | `Employee`, `BankAccount` |
| Constants | ALL_CAPS with underscores | `MAX_SIZE`, `PI` |
| Packages | all lowercase | `java.util`, `com.mycompany.app` |

```java
// Following convention
int studentAge = 20;
class StudentRecord { }
final double INTEREST_RATE = 0.05;
package com.myapp.utils;

// Technically legal, but bad practice
int StudentAge = 20;      // should be camelCase
class studentrecord { }    // should be PascalCase
```

**Reserved keywords you can't use as identifiers**

Java has around 50 reserved words. Some common ones you'll run into:
```
class    public   private   static   void   int
double   boolean  if       else     for    while
return   new      import   package  final  try
catch    this     super    null     true   false
```

If you try to use one as a variable name, you'll get a compile error:
```java
int class = 5;  // ❌ Compile error — "class" is reserved
```

**A note on `$` and `_`**

Technically legal, but rarely used in normal code:
```java
int $total = 100;   // legal, but unconventional
int _flag = true;   // legal, but unconventional
```
You'll mostly see `$` in auto-generated code (like from compilers or frameworks) and `_` sometimes as a placeholder — Java actually reserves a single underscore (`_`) as a special "unused variable" marker in newer versions, so avoid using just `_` alone as a name.

**Quick self-check example**

```java
int 2ndPlace = 10;     // ❌ invalid — starts with digit
String user-name = "x"; // ❌ invalid — hyphen not allowed
double $balance = 5.5;  // ✅ valid, but unconventional
boolean isReady = true; // ✅ valid and follows convention
```
