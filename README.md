# Java-Finish-Line

### CORE




### **1.1 Identifiers**


An **identifier** is simply the name you give to things in your code — variables, methods, classes, interfaces, packages, etc. Anytime you're naming something, you're creating an identifier.

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



### **1.1 Variables**



**1. Two categories of variables: primitive vs. reference**

**Primitive types** — store the actual value directly, built into Java (8 total):

| Type | Size | Example | Default value |
|---|---|---|---|
| `byte` | 1 byte | `byte b = 100;` | `0` |
| `short` | 2 bytes | `short s = 30000;` | `0` |
| `int` | 4 bytes | `int i = 100000;` | `0` |
| `long` | 8 bytes | `long l = 100000L;` | `0L` |
| `float` | 4 bytes | `float f = 3.14f;` | `0.0f` |
| `double` | 8 bytes | `double d = 3.14159;` | `0.0` |
| `char` | 2 bytes | `char c = 'A';` | `'\u0000'` |
| `boolean` | 1 bit | `boolean flag = true;` | `false` |

**Reference types** — store a reference (like an address) pointing to an object in memory, not the object itself:
```java
String name = "Alex";        // String is a reference type
int[] numbers = {1, 2, 3};    // arrays are reference types
Scanner scanner = new Scanner(System.in);  // objects in general
```

The practical difference matters most when you assign one variable to another:
```java
// Primitive — copies the actual value
int a = 5;
int b = a;
b = 10;
System.out.println(a);  // 5 (unaffected)

// Reference — copies the reference, both point to same object
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1;
arr2[0] = 99;
System.out.println(arr1[0]);  // 99 (changed! same underlying array)
```
### **1.1.2 Declare variable**


Declare a variable by specifying its **type**, then a **name**, and optionally assigning a value:

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

**2. Three kinds of variables, based on where they're declared**
```java
public class Example {
    int instanceVar = 10;      // instance variable (belongs to object)
    static int classVar = 20;  // static/class variable (shared across all objects)

    void someMethod() {
        int localVar = 30;      // local variable (only exists inside this method)
    }
}
```


| Kind | Declared where | Belongs to | Default value? |
|---|---|---|---|
| Local | inside a method | that method call only | ❌ must initialize before use |
| Instance | inside a class, outside methods | each object individually | ✅ gets default value |
| Static | inside a class, with `static` keyword | the class itself, shared | ✅ gets default value |

**Important:** local variables do NOT get default values — you must initialize them yourself, or the compiler throws an error:
```java
void method() {
    int x;
    System.out.println(x);  // ❌ compile error: "variable x might not have been initialized"
}
```
But instance/static variables are automatically initialized:
```java
public class Example {
    int count;  // automatically becomes 0, no error
}
```

**1.1.3 Type casting — converting between types**

Sometimes you need to convert one type to another:

```java
// Widening (automatic) — smaller type to bigger type, no data loss
int i = 100;
double d = i;  // 100.0, happens automatically

// Narrowing (manual/explicit) — bigger type to smaller type, possible data loss
double price = 19.99;
int wholeNumber = (int) price;  // 19 — you must explicitly cast, decimal is truncated
```

**1.1.4 `final` variables — constants**

Once assigned, a `final` variable can't be reassigned:
```java
final double PI = 3.14159;
PI = 3.14;  // ❌ compile error — cannot assign a value to final variable
```




### **2. Reading inputs from the console**


The most common way to read input from the console is using the **`Scanner`** class.

**2.1.1 Basic setup**
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

**2.1.2 Reading different data types**

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

**2.1.3"leftover newline"**

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

**2.1.4 Reading multiple values on one line**
```java
System.out.print("Enter three numbers separated by spaces: ");
int a = scanner.nextInt();
int b = scanner.nextInt();
int c = scanner.nextInt();
```

### **3.  String Concatenation** 


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



### **4. print vs. println**


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



**Mixing them**
```java
System.out.print("Name: ");
String name = "Alex";
System.out.println(name);
// Output: Name: Alex   (on one line, because print() didn't break the line)
```

**Quick tip:** `println()` with no arguments just prints an empty line (like pressing Enter):
```java
System.out.println("First line");
System.out.println();  // blank line
System.out.println("Second line");
```

### **5. specific vs. wildcard imports**


**`import`** statements let you use classes from other packages without typing the full package path every time. There are two ways to do it:

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

**wildcards: naming conflicts**
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

