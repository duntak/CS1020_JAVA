Chapter 1

Section 1.1 (Excludes Arrays) to Section 1.5: Pages 27 to 45

Section 1.7 (Excludes Console class): pages 73 to 77

### Java: Brief History and background
James Gosling found Java in 1995 when he was working in Sun Microsystems. He use C/C++ as foundation, created a "Cleaner" in syntax, less low-level machine interaction language which is Java.
Advantages:
1. Write Once, Run Everywhere
2. Extensive and Well documented Standard library
Disadvantage:
1. Less Efficient

### Run cycle
#### In C Programs
1. Writing / Editing Program: Use vim Editor and source code must have a .c extension
2. Compiling Program: Use gcc Compiler to create a default executable file: a.out
3. Executing Binary: Type a.out, But **a.out file unable to execute on different platforms** becuase __Executable files are directly dependent on the OS/Hardware__

#### In Java Program
**Java run executable file on an _uniform hardware environment_** also known as **_Java Virtual Machine_**, So __Compile once and run anywhere.__
1. Writing/Editing program: Use vim Editor and source code must have .java extension
2. Compiling program: use javac compiler and create .class extension
3. Run on Java Virtual Machine, eg. java Helloworld __NO Need to type extension__

### Basic Program Structure
- __Common Mistakes__
  - Public class name not identical to program's file name. eg `public class HelloWorld` and the file name must be 'HelloWorld.java'
- Import package
  - use `import xxxx` statements
  - use `*` to import all packages under a group
- class
  - Only one main() method in a class
  - A source code file may contain more than one classes

### Basic Java elements
#### Arithmetic Expressions
1. Identifier
  - Letters ('a' - 'z', 'A' - 'Z')
  - Digit('0' - '9')
  - Underscore (' _ ')
  - Dollar sign ('$')
  - Can not begin with digit character
  - __Rules for Naming
    - __UpperCamelCase__
    - eg HelloWorld
2. Variable
  - Declared with a specific data type
  - eg. int length
  - __Rules for Naming
    - __lowerCamelCase__
    - eg countDays
3. Constant
  - Represent a fixed value
  - eg public static __final__ int PEOPLE = 65;
  - keyword **final** indicate the value can not change
  - __Rules for Naming__
    - __ALLUPPERCASE__
    - eg. PI

#### Data Type Conversion
Common Mistake
```
double d;
int i;
i = 31415;
d = i / 10000;
```
Correction: use type casting
```
double d;
int i;
i = 31415;
d = (double) i / 10000;
```

__type casting__
syntax: `(datatype) value`

Effect: value is converted explicitly to the data type

**_Exercise_** Fahrenheit to Celsius
``` java
public class Temperature{
  public static void main (String[] args){
    double fahrenheit, celsius;
    fahrenheit = 123.5;
    celsius = (5.0/9) * (fahrenheit - 32);
    System.out.println("Celsius: " + celsius);
  }
}
```
Notes:
- 5.0/9 is necessary to get the correct result (what will 5/9 give? Answer: 0)
- “+” in the printing statement
  - Concatenate operator, to combine strings into a single string
  - Variable **values** will be converted to **string** automatically
- There is another printing statement, System.out.print(), which does not include newline at the end of line

#### Control Flow statements and Logical Expressions

Boolean Data Type: store **true** or **false**, take note that **true** and  **false** are __Keywords__ in java

In C Program, `0` means false and any other values means true. <br>
In Java, there is `true` and `false`

Boolean operator

| Operators | Description           |
| --------- | :----------           |
| <         | Less than             |
| >         | larger than           |
| <=        | Less than or equal    |
| >=        | greater than or equal |
| ==        | Esqual                |
| !=        | Not Equal             |
| &&        | And                   |
|           | or                    |
| !         | Not                   |
| ^         | Exclusive - or        |

Selection statements
- if-Else statement
  - Must be a boolean Expressions
  - integer values not valid
- Switch statement
  - Expression in switch() must evaluate to a value of char, byte, short or int type
  - break: stop the fall-through execution
  - default: catch all unmatched cases; may be optional
- while and do-while statement
  - Must be a boolean Expression
- for loop
  - initialization ; condition ; update
  - Order
    - A, B, body, C, B, body, C,

Repetition statement
- for loop
  - In ANSI C, the loop variable must be declared before it is used in a ‘for’ loop
    - Declare outside for loop
  ```
  int i;
  for(i=0;i<10;i++);
  ```
  - In Java, the loop variable may be declared in the initialisation part of the ‘for’ loop
    - eg `for (int i = 0; i < 10; i++)`

#### Basic Input and Output

##### Input
- Package: `import java.util.Scanner;`
- Syntak:
  ``` java
  Scanner scVar = new Scanner(System.in);
  scVar.nextInt();
  scVar.nextDouble();
  ```

**_Exercise_** Reading Input
``` java
import java.util.Scanner; // or import java.util.*
public class Temperature{
  public static void main(String[] args){
    double fahrenheit, celsius;
    Scanner sc = new Scanner(System.in);
    System.out.print("Enter Temperature in fahrenheit: ");
    fahrenheit = sc.nextDouble();
    celsius = (5.0 / 9) * (fahrenheit - 32);
    System.out.println("celsius: " + celsius);
  }
}
```
Notes
- The statement `Scanner sc = new Scanner(System.in);` declare a variable `sc` of Scanner Type
- The initialization `new Scanner(System.in)`
  - Construct a Scanner object
  - Attach it to the standard input `System.in`
    - Receive input from this device
  - Scanner can attach to other inputs
- Functions to read input
  - `nextDouble()` is a method that return a double value
- Typically only **one Scanner Object** is required

##### Output
- System.out is the predefined output device refers to the screen of your computer
- System.out.print(out_put)
  - `System.out.print("ABC");`  
- System.out.println(out_put)  
  - `System.out.println("GHI"); //Print new line`
- System.out.printf(format_string, [items])
    - `System.out.printf("Very C-like %.3f\n", 3.14159);`

Format Specificers and Modifiers

| Name   |   Description      |
|--------|--------------------|
| %d     | Integer Type       |
| %f     | Double Floating    |
| %s     | String             |
| %b     | Boolean Type       |
| %c     | Character Type     |

**_Exercise_** Approximating PI
``` java
import java.util.*;
public class ApproximatePI{
  public static void main(String[] args){
    int nTerms, sign = 1, denom = 1;
    double pi = 0.0;

    Scanner sc = new Scanner(System.in);
    System.out.print("Enter number of terms: ");
    nTerm = sc.nextInt();

    for(int i=0; i<nTerms; i++){
      pi += 4.0 / denom * sign;
      sign *= -1;
      denom += 2;
    }
    System.out.printf("PI = %6f\n", pi);
  }
}

```

#### API
- API: an interface for other programs to interact with a program without having direct access to the internal data of the program
- For Java programmers, it is very important to refer to the API documentation regularly!
- The API consists of many classes
    - You do not need to know all the classes (there are easily a few thousand classes altogether!)
    - Read up __Scanner__ class in the API documentation

#### Math class, Class Attributes
- Package: java.lang(default)
  - useful Math methods
    - abs()
    - ceil()
    - floor()
    - max()
    - min()
    - pow()
    - random()
    - sqrt()

#### User-defined Functions
- In Java, C-like function is known as static/class method
  - Denoted by the “static” keyword before return data type
``` java
public class Factorial{
  public static int factorial (int n){
    if(n == 0) return 1;
    else return n * factorial(n-1);
  }
  public static void main(String[] args){
    int n = 5;
    System.out.printf("Factorial(%d) = %d ", n , factorial(n));
  }
}
```

Method Parameter Passing
- All parameters in Java are passed by value

**_Summary_**

Data Types:
  - Numeric Data Types:
      - byte, short, int, float, double
  - Boolean Data Type:
	boolean
Expressions:
  - Arithmetic Expression
  - Boolean Expression
Control Flow Statements:
  - Selection Statements: if-else, switch-case
  - Repetition Statements: while, do-while, for
Classes:
  - Scanner
  - Math
