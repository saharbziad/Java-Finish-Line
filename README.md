# Java-Finish-Line

### CORE




### **1. Identifiers**


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
### **1.2 Declare variable**


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

**1.3 Type casting — converting between types**

Sometimes you need to convert one type to another:

```java
// Widening (automatic) — smaller type to bigger type, no data loss
int i = 100;
double d = i;  // 100.0, happens automatically

// Narrowing (manual/explicit) — bigger type to smaller type, possible data loss
double price = 19.99;
int wholeNumber = (int) price;  // 19 — you must explicitly cast, decimal is truncated
```

**1.4 `final` variables — constants**

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

**2.1 Reading different data types**

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

**2.2 "leftover newline"**

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

**2.3 Reading multiple values on one line**
```java
System.out.print("Enter three numbers separated by spaces: ");
int a = scanner.nextInt();
int b = scanner.nextInt();
int c = scanner.nextInt();
```

### **3.  String Concatenation** 


**String concatenation** means joining two or more strings together into one. In Java, there are several ways to do it:

**1.1 Using the `+` operator** (most common)
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
### **6. Numeric Operations**


| Category | Operators |
|---|---|
| Arithmetic | `+` `-` `*` `/` `%` |
| Increment/Decrement | `++` `--` |
| Compound assignment | `+=` `-=` `*=` `/=` `%=` |
| Comparison | `==` `!=` `>` `<` `>=` `<=` |
| Logical | `&&` `\|\|` `!` |

 **6.1 Arithmetic**

 
**The 5 basic operators**

```java
int a = 10;
int b = 3;

a + b   // 13  → addition
a - b   // 7   → subtraction
a * b   // 30  → multiplication
a / b   // 3   → division
a % b   // 1   → remainder (what's left over)
```

**The one thing to watch out for**

If both numbers are `int`, division drops the decimal part:
```java
int result = 7 / 2;   // 3, not 3.5
```

To get the decimal, make at least one number a `double`:
```java
double result = 7.0 / 2;   // 3.5
```

 **6.2 Increment/Decrement**


**1. Basic usage**

```java
int x = 5;
x++;   // x is now 6
x--;   // x is now 5 again
```


**2. Pre-increment vs. post-increment — the important distinction**

```java
int a = 5;
int b = a++;   // POST-increment: use a's CURRENT value first, THEN increment

System.out.println(a);   // 6
System.out.println(b);   // 5  ← got the OLD value of a
```

```java
int c = 5;
int d = ++c;   // PRE-increment: increment FIRST, THEN use the new value

System.out.println(c);   // 6
System.out.println(d);   // 6  ← got the NEW value of c
```

**Side-by-side comparison**

| Expression | What happens | Value used |
|---|---|---|
| `x++` | increments *after* the value is used | old value |
| `++x` | increments *before* the value is used | new value |
| `x--` | decrements *after* the value is used | old value |
| `--x` | decrements *before* the value is used | new value |

**3. Same logic applies to decrement**

```java
int a = 10;
int b = a--;   // b = 10 (old value), a becomes 9

int c = 10;
int d = --c;   // c becomes 9 first, d = 9 (new value)
```
### **6.3 Compound assignment**


Compound assignment operators are shortcuts that combine an operation with assignment in one step.

**The basic idea**

Instead of writing this:
```java
x = x + 5;
```

You can write this:
```java
x += 5;
```

Both do exactly the same thing — just shorter.

**The 5 compound operators**

```java
int x = 10;

x += 5;   // same as x = x + 5   → 15
x -= 3;   // same as x = x - 3   → 12
x *= 2;   // same as x = x * 2   → 24
x /= 4;   // same as x = x / 4   → 6
x %= 4;   // same as x = x % 4   → 2
```

**Simple example**

```java
int score = 0;
score += 10;   // score is now 10
score += 10;   // score is now 20
score -= 5;    // score is now 15
```

**6.4 Comparison**


Comparison operators compare two values and give back `true` or `false`.

**The 6 comparison operators**

```java
5 == 5   // true   → equal to
5 != 3   // true   → not equal to
5 > 3    // true   → greater than
5 < 3    // false  → less than
5 >= 5   // true   → greater than or equal to
5 <= 4   // false  → less than or equal to
```

**Example**

```java
int age = 20;

boolean isAdult = age >= 18;   // true
boolean isChild = age < 13;     // false
```

**Watch out for**

`==` (comparison) is easy to mix up with `=` (assignment):
```java
if (age == 18) { }   // ✅ checks if age equals 18
if (age = 18) { }     // ❌ compile error for booleans — this assigns 18 to age instead
```


**6.5Logical**


Logical operators combine multiple `true`/`false` conditions into one result.

**The 3 logical operators**


| Operator | Name | True when... |
|---|---|---|
| `&&` | AND | both sides are true |
| `\|\|` | OR | at least one side is true |
| `!` | NOT | flips true ↔ false |


```java
true && false   // false  → AND (both must be true)
true || false   // true   → OR (at least one must be true)
!true            // false  → NOT (flips the value)
```

**Example**

```java
int age = 20;
boolean hasLicense = true;

boolean canDrive = age >= 18 && hasLicense;   // true (both conditions true)
```

```java
boolean isWeekend = true;
boolean isHoliday = false;

boolean isDayOff = isWeekend || isHoliday;     // true (at least one is true)
```

```java
boolean isRaining = false;

boolean goOutside = !isRaining;   // true (flips false to true)
```

**6.6 Casting**


**Casting** = converting one data type into another.

**Two types**

```java
int i = 100;
double d = i;   // ✅ automatic — small type to big type
```

```java
double price = 19.99;
int whole = (int) price;   // ✅ manual — big type to small type, needs (type)
```

**The rule**

- Small → big: automatic, no cast needed
- Big → small: you must write `(type)` in front



**6.7 BODMAS**

BODMAS = the order Java follows when evaluating an expression with multiple operators.
Brackets → Orders (powers/roots) → Division → Multiplication → Addition → Subtraction.



```java
2 + 3 * 4   // multiply first: 3*4=12, then 2+12 = 14
```

```java
(2 + 3) * 4   // brackets first: 2+3=5, then 5*4 = 20
```
