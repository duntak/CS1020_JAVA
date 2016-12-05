### Recapitulation
- Compiling and running Java programs
- Java program structure
- Basic Java elements
- API: Scanner class, Math class

### API: Where you find service classes
__Aplication Programming Interface - Where you find service classes__

####	2.1  Scanner class (revisit)
- For reading input, `import java.util.Scanner`
- Important methods
  - next(): Finds and returns the next complete token from this scanner.
  - nextDouble(): Scans the next token of the input as a double.
  - nextInt():Scans the next token of the input as an int.
  - nextLine():Advances this scanner past the current line and returns the input that was skipped.
  - hasNext(): Returns true if this scanner has another token in its input
  - hasNextDouble(): Returns true if the next token is Double
  - hasNextInt(): Returns true if the next token is Int
  - hasNextLine(): Returns true if there is another line in the input of this scanner.

``` Java
import java.util.*;
public class TestScanner{
  public static void main(String[] args){
    Scanner sc = new Scanner(System.in);
    //Comparing nextLine() and next()
    System.out.print("Enter name1: ");
    String name1 = sc.nextLine();
    System.out.println("name1 entered is '"+name1+"'.");

    System.out.print("Enter name2: ");
    String name2 = sc.next();
    System.out.println("name2 entered is '"+name2+"'.");
    sc.nextLine();   //Important: to skip the rest of the line after the next() method captured the first word of the second name

    //Using nextInt() and hasNextInt()
    int num,sum = 0;
    System.out.println("Enter integers, terminate with control-d");
    while(sc.hasNextInt()){
      num = sc.nextInt();
      System.out.println("Integer read: " + num);
      sum += num;
    }
    System.out.println("Sum = "+ sum);
  }
}
```

#### 2.2  String class (revisit)
- Representation in Text, `import java.lang.String`
- Important methods
  - charAt(): Returns the char value at the specified index.
  - concat(): Concatenates the specified string to the end of this string.
  - equals(): Compares this string to the specified object.
  - indexOf(): Returns the index within this string of the first occurrence of the specified character.
  - lastIndexOf(): Returns the index within this string of the last occurrence of the specified character.
  - length(): Returns the length of this string.
  - toLowerCase(): Converts all of the characters in this String to lower case using the rules of the default locale.
  - toUpperCase(): Converts all of the characters in this String to upper case using the rules of the default locale.
  - substring(): Returns a new string that is a substring of this string.
  - trim(): Returns a copy of the string, with leading and trailing whitespace omitted.
- Notes
  - Strings are objects, __do not use ==__ to check if two strings contains the same text, must use equals() method

``` java
import java.lang.String; //Optional
public class TestString{
  public static void main(String[] args){
    String text = new String("I am studying CS1020");
    String text2 = "I am Studying CS1020 Again";

    System.out.println("text: "+ text);
    System.out.println("text.length() = " + text.length());
    System.out.println("text.charAt(5) = " + text.charAt(5));
    System.out.println("text.substring(5,8) = " + text.substring(5,8));
    System.out.println("text.indexOf(\"in\") = " + text.indexOf("in"));

    String newText = text + "How are you";
    newText = newText.toUpperCase();
    System.out.println("newText: " + newText);
    if(text.equals(newText)){
      System.out.println("text and newText are equal");
    }else{
      System.out.println("text and newText are not equal");
    }
  }
}

```

#### 2.3  Math class (revisit)
- Maths Demo

``` java
import java.util.*;     

public class TestMath2 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		System.out.print("Enter 3 values: ");
		double num1 = sc.nextDouble();
		double num2 = sc.nextDouble();
		double num3 = sc.nextDouble();

		System.out.printf("pow(%.2f,%.2f) = %.3f\n", num1, num2, Math.pow(num1,num2));
		System.out.println("Largest = " + Math.max(Math.max(num1,num2), num3));
		System.out.println("Generating 5 random values:");
		for (int i=0; i<5; i++)
			System.out.println(Math.random());
	}
}


```

### OOP concepts (basic)
#### 3.1 Modifiers
- modifiers are keywords that added to specify the way a class/attribute/method works
- Access-Control modifiers
  - public
  - private
- Non-Access modifiers
  - static

#### 3.2 Class vs Instance methods
- static method also known as class method
  - It means that no object(instance) of the class is needed to use the method
  - Eg. String Class, Math Class
  - All methods in the Math class are class methods
    - `double answer = Math.pow(3.5,2.2)`
    - Calling class method by using the class name
  - String class comprises a mix of class and instance methods
- non-Static method also known as instance method
  - It means that the method must be applied to an object(instance) of that class
  - eg. Scanner class
    - All methods in the Scanner class are instance methods
    - `Scanner sc = new Scanner(System.in)`
    - Calling instance method using object
    - `double answer = sc.nextDouble()`

#### 3.3 Constructors
- Instance methods Require constructor to create instance
  - key word is `new`
  - `String str1 = new String()`
  - `String str2 = new String("To be or not to be?")`
- Important Notes
  - `String str1 = "To be "` and `String str2 = new String("To be");` are not equal
  - __String objects are Immutable__

#### 3.4 Overloading
- Overloading: Some methods have identical name but different parameter
- Example: `abs(double a); abs(int a);` and `absDouble(double a); absInt(int a)`

### More classes (new)
#### 4.1 DecimalFormat class
- We have used the System.out.printf() statement to format the output of real number
  -`System.out.printf("Math.PI = %.3f\n", Math.PI);`
- We also can use the DecimalFormat class in the `import java.text.DecimalFormat` package  

``` java
import java.text.DecimalFormat;
public class TestDecimalFormat{
  public static void main(Stirng[] args){
    DecimalFormat df1 = new DecimalFormat("0.000");  //3 Decimal
    DecimalFormat df2 = new DecimalFormat("#.###");  //3 Decimal, 0 will not show
    DecimalFormat df3 = new DecimalFormat("0.00%");  //2 Decimal, with percent sign

    System.out.println("PI = " + df1.format(Math.PI));
		System.out.println("12.3 formatted with \"0.000\" = " + df1.format(12.3));
		System.out.println("12.3 formatted with \"#.###\" = " + df2.format(12.3));
		System.out.println("12.3 formatted with \"0.00%\" = " + df3.format(12.3));

  /*
PI = 3.142
12.3 formatted with "0.000" = 12.300
12.3 formatted with "#.###" = 12.3
12.3 formatted with "0.00%" = 1230.00%
  */

  }
}

```

#### 4.2 Random class
- Generate Random number
- The Math class provides a random() method
- Alternatively, you may use the Random class in the `Import java.util.Random` package
  - Constructors
    - Random(): random numbers generated are different each time program is run
    - Random(long seed): random numbers generated are taken from a pre-determined fixed sequence based on the seed

``` java
import java.util.Random;

public class TestRandom {
	public static void main(String[] args) {
		// To generate a random integer in [51,70]
		// using Math.random() and Random's nextInt()
		int num1 = (int) (Math.random() * 20) + 51;
		System.out.println("num1 = " + num1);
		Random rnd = new Random();
		int num2 = rnd.nextInt(20) + 51;
		System.out.println("num2 = " + num2);
	}
}

```

####	4.3 Wrapper classes
- __Primitive Data Types such as Int, Double, Char, Boolean, Float are not objects__
- Sometimes we need object equivalent of these primitive data types
- These are called wrapper classes – one wrapper class corresponding to each primitive data type
  - int -> Integer
  - long -> Long
  - float -> Float
  - double -> Double
  - char -> Character
  - boolean -> Boolean
- We may convert a primitive type value to its corresponding object.
- Wrapper classes offer methods to perform conversion between types

``` java
//Convert primitive type to Object
int x = 9;
Integer y = new Integer(x);
System.out.println("Value in y = " + y.intValue());

//Convert between string and intger
int num = Integer.valueOf("28");
String str = Integer.toString(567);

```


####	4.4 Point class
- Point is another class, need to `import java.awt.Point`
- The Point class contains 2 attributes
  - Attrubutes also known as data members
    - It can be class attributes (With Static modifier)
    - It can be instance attributes (No Static modifier)
  - The two attributes are instance attributes which means __Must create Object__
- Three Constructors
  - Point()
  - Point(int x, int y)
  - Point(Point P)
- Important methods
  - getLocation(): return the location of this Point
  - getX(): return X coordinate, Double
  - getY(): return Y coordinate, Double
  - move(int x, int y): Moves this point to the specified location
  - toString(): Returns a string representation of this point
- Common Mistakes
  - Accessing an object before it is created
    - `Point pt`; `pt.setLocation(12,10)`
      - Wrong because never create Object
      - Correction: `Point pt = new Point()`


``` java
// To test out Point class
import java.util.*;
import java.awt.*;

public class TestPoint {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		System.out.print("Enter x and y: ");
		int xCoord = sc.nextInt();
		int yCoord = sc.nextInt();

		Point pt = new Point(xCoord, yCoord);

		System.out.println("x-coordinate is " + pt.getX());
		System.out.println("y-coordinate is " + pt.y);

		System.out.println("The point created is " + pt);
		// or: System.out.println("The ... is " + pt.toString());
	}
}

```

### Abstraction and Information Hiding
- One OOP design issue is abstraction
  - Procedural abstraction: Specify what to do, not how to do it, separates the purpose of a method from its implementation
  - Data abstraction: Specify what you will do to data, not how to do it, focuses on what operations on the data are to be provided instead of their implementation
- Procedural abstraction
  - It provides an interface with the user
  - **How** the method is implemented is hidden from the user
