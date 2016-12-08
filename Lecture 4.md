### 4 fundamental OOP concepts
#### Encapsulation
		Bundling data and associated functionalities
		Hide internal details and restricting access
####	Inheritance
		Deriving a class from another, affording code reuse
####	Abstraction
		Hiding the complexity of the implementation
		Focusing on the specifications and not the implementation details
####	Polymorphism
		Behavior of functionality changes according to the actual type of data

### OOP language
The characteristic of OOP language is that it view the program as a collection of __Objects__ and each object has its own __Behavior(Methods / Functions)__ and __Attributes (Variables)__ These Attributes are hidden from the public.
For example: Bank Account is an object, it consists of two **attributes**: `bankAccountName` and `bankAccountBalance`, two **Behavior**: `withdrawMoney()` and `depositeMoney()`

### Design own class
The purpose of creating own class is to have a template to create objects. A class consist of Behavior and Attributes.  It is important to know that __All instances (objects) of the same class are independent entities that possess the same set of attributes and behaviours__. **__ Class is a temple for Objects__**
- Attributes are also called Member Data, or Fields (in Java API documentation)
	- Usually Private
- Behaviours (or Member Behaviours) are also called Methods (in Java API documentation)
	- Usually public

Public: Anyone can access  
Private: Accessed by the same method
Protected: Can be assessed by the classes in the same Java package
None: Only accessible to classes in the same Java package

``` Java
class BankAccount{

//Attributes
	private int bankAccountNumber;
	private double bankAccountBalance;

//Behaviours
	// 1. Constructors
	// 2. Methods
			//1. get methods   -----> Accessor: Access Data Only
			//2. set methods 	------> Mutator: Change Value
			//3. Other methods ------> such as Print

	//Default Constructor
	public BankAccount(){
		//Default set everything to 0
	}

	//Constructor with initialization
	public BankAccount(int aNUm, double bal){
		bankAccountNumber	= aNUm;
		bankAccountBalance = bal;
	}


	public int getAccountNumber(){
		return bankAccountNumber;
	}

	public double getAccountBalance(){
		return bankAccountBalance;
	}

	public boolean withdrawMoney(double amount){
		if(bankAccountBalance > amount){
			bankAccountBalance -= amount;
			return true;
		}else{
			return false;
		}
	}

	public void depositeMoney(double amount){
		bankAccountBalance += amount;
	}

	public void print(){
		System.out.println("Account Number =" + bankAccountNumber);
		System.out.println("Account Balance = " + bankAccountBalance);
	}

}
```

``` Java
//Test Account in main()
public class TestAccount{
	public static void main(String[]args){
		BankAccount account1 = new BankAccount();
		BankAccount account2 = new BankAccount(1234,500.0);

		System.out.println("Before Transaction");
		account1.print();
		account2.print();

		//Error 1: Unable to access data becasue bankAccountBalance is private
		//account1.bankAccountBalance += 1000;
		account1.depositeMoney(1000);
		account2.withdrawMoney(50);

		System.out.println("After Transaction");
		account1.print();
		account2.print();


	}
}
```
### Class and instance members
A class comprises 2 types of members:
1. Attributes (Data Members)
2. Methods(Behavior memebrs)
Java use `static to indicate if the member if a class member or an instance member`
1. static: class Attributes
2. Default: instance Attributes

when accessing __class attributes or class methods__, we use the name of the __class__, for example, in the last part of the code, we use `MyBall.getQuantity` to access the method. We can not access quantity because it is `private`

``` Java
class MyBall {
	/************** Data members **********************/
	private static int quantity = 0;	//Class Attributes, shared by all instances
	private String colour;		//Only accessed by individual instance memebr
	private double radius;		//Only accessed by individual instance memebr

	/************** Constructors **********************/
	// Default constructor creates a yellow, radius 10.0 ball
	//Before Simplification
	/*
	public MyBall() {
		setColour("yellow");
		setRadius(10.0);
		quantity++;
	}
	*/
	//After Simplification
	public MyBall() {	//It will call MyBall(String newColour, double newRadius) method
		this("yellow",10.0)
	}

	public MyBall(String newColour, double newRadius) {
		setColour(newColour);
		setRadius(newRadius);
		quantity++;
	}

/**************** Accessors ***********************/
	public static int getQuantity() {	//Class Method
		return quantity;
	}

	//Before Simplification
	/*
	public String getColour() {
		return colour;
	}

	public double getRadius() {
		return radius;
	}
	*/
	//After Simplification
	public String getColour() {
		return this.colour;
	}

	public double getRadius() {
		return this.radius;
	}

	/**************** Mutators ************************/
	//Before Simplification
	/*
	public void setColour(String newColour) {
		colour = newColour;
	}

	public void setRadius(double newRadius) {
		radius = newRadius;
	}
	*/
	//After Simplification
	public void setColour(String colour) {
		this.colour = colour;
	}

	public void setRadius(double radius) {
		this.radius = radius;
	}


}
```

``` Java
import java.util.*;
public class TestBallV1 {
	public static void main(String[] args) {
		String inputColour;
		double inputRadius;
		Scanner sc = new Scanner(System.in);

		// Read ball's input and create a ball object
		System.out.print("Enter colour: "); inputColour = sc.next();
		System.out.print("Enter radius: "); inputRadius = sc.nextDouble();
		MyBall myBall1 = new MyBall(inputColour, inputRadius);
		System.out.println();

		// Read another ball's input and create another ball object
		System.out.print("Enter colour: "); inputColour = sc.next();
		System.out.print("Enter radius: "); inputRadius = sc.nextDouble();
		MyBall myBall2 = new MyBall(inputColour, inputRadius);
		System.out.println();

		System.out.println(MyBall.getQuantity() + " balls are created.");
		System.out.println("1st ball's colour and radius: " + myBall1.getColour() + ", " + myBall1.getRadius());
		System.out.println("2nd ball's colour and radius: " + myBall2.getColour() + ", " + myBall2.getRadius());
	}
}

```

``` java
//Add overriding methods

class MyBall {
	// Other parts omitted

	// Overriding equals() method
	public boolean equals(Object obj) {
		if (obj instanceof MyBall) {
			MyBall ball = (MyBall) obj;
			return this.getColour().equals(ball.getColour())
			        && this.getRadius() == ball.getRadius();
		}
		else
			return false;
	}

	public String toString() {
		return "[" + getColour() + ", " + getRadius() + "]";
	}

}

```

``` Java
//After Modularising
import java.util.*;
public class TestBallV2 {
	// This method reads ball's input data from user, creates
	// a ball object, and returns it to the caller.
	public static MyBall readBall(Scanner sc) {
		System.out.print("Enter colour: ");
		String inputColour = sc.next();
		System.out.print("Enter radius: ");
		double inputRadius = sc.nextDouble();
		return new MyBall(inputColour, inputRadius);
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		MyBall myBall1 = readBall(sc); // Read input and create ball object
		System.out.println();

		MyBall myBall2 = readBall(sc); // Read input and create another ball object
		System.out.println();

		System.out.println(MyBall.getQuantity() + " balls are created.");
		System.out.println("1st ball's colour and radius: "
		     + myBall1.getColour() + ", " + myBall1.getRadius());
		System.out.println("2nd ball's colour and radius: "
		     + myBall2.getColour() + ", " + myBall2.getRadius());
	}
}


```

``` java
//Final Version

import java.util.*;
public class TestBallV4 {
	// readBall() method omitted for brevity

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		MyBall myBall1 = readBall(sc); // Read input and create ball object
		MyBall myBall2 = readBall(sc); // Read input and create another ball object

		// Testing toString() method
		// You may also write: System.out.println("1st ball: " + myBall1.toString());
		//                     System.out.println("2nd ball: " + myBall2.toString());
		System.out.println("1st ball: " + myBall1);
		System.out.println("2nd ball: " + myBall2);
		// Testing ==
		System.out.println("(myBall1 == myBall2) is " + (myBall1 == myBall2));
		// Testing equals() method
		System.out.println("myBall1.equals(myBall2) is "
		                    + myBall1.equals(myBall2));
	}
}

```
