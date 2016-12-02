## Arrays

### 1.1	Introduction
- Array is the simplest way to store a collection of data of the same type (homogeneous)
- It stores its elements in contiguous memory
  - Array index begins from zero
  - Example of a 5-element integer array A with elements filled

### 1.2	Array in Java
In java, Array is an __Object__, Every array has a __public length attribute__

Notes:
- Attribute is not a method
- Declaring an array:
  - `datatype[] array_name`
- Constructing an array:
  - `array_name = new datatype[size]`
- Construct and Initialize array
  - `datatype [] array_name = new {elements}`
- Accessing individual array elements
  - use for loop
  - use enhanced for loop
    - `for(datatype e: array_name)`
      - Go through all elements in the array, 'e' refers to the elements
- toString() method
  - In the Arrays class, there is a toString() method which can convert arr to string
  - `Arrays.toString(arr)`

``` Java
//For Loop
public class TestArray1{
  public static void main(String[] args){
    int [] arr; //arr is a reference(pointer)
    //Create a new integer array with 3 elements
    //arr now refers(points) to the new array
    arr = new int[3];

    //Using the length Attribute
    //Not method, a method will have brackets, eg length()
    System.out.println("Length = " + arr.length);

    arr[0] = 100;
    arr[1] = arr[0] - 37;
    arr[2] = arr[1] / 2;
    for(int i = 0; i < arr.length;i++){
      System.out.println("arr[" + i + "] = " + arr[i]);
    }
  }
}
```

``` Java
//Enhanced For loop
public class TestArray2{
  public static void main(String[] args){
    //Construct and initialize array
    double [] arr = {35.1,21,57/7,18.3};
    //Using the length attribute
    System.out.println("Length = " + arr.length);
  for(int i = 0; i < arr.length;i++){
    System.out.print(arr[i] + " ");
  }
  System.out.println();

  //Enhanced For loop
  for(double element:arr){
    System.out.print(element + " ");
  }
  System.out.println();
  System.out.println(Arrays.toString(arr));

  }
}
```

### 1.3	Array as a Parameter
- The reference to the array is passed into a method
  - Any modification of the elements in the method will affect the actual array
    - This is the same in C program, arr is a pointer

``` Java
public class TestArray3{
  public static void main(String[] args){
    int [] list = {22,55,33};
    swap(list,0,2);
    for(int element:list){
      System.out.print(element + " ");
    }
    System.out.println();
  }

  public static void swap(int[] arr, int i, int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
  }
}
```

### 1.4	Detour: String[] in main() method
- The main() method contains a parameter which is an array of String objects
- We can use this for command-line arguments

``` Java
public class TestCommandLineArgs{
  public static void main(String[] args){
    for(int i = 0; i<args.length;i++){
      System.out.println("args[" + i +"] = " + args[i]);
    }
  }
}
```

### 1.5	Returning an Array
- Array can be returned from a method

``` Java
public class TestArray4{
  public static void main(String[] args){
    double []values;
    values = makeArray(5,999.0);
    for(double value:values){
      System.out.println(value + " ");
    }
  }

  //To create an array and return it to caller
  public static double[] makeArray(int size, double limit){
    double []arr = new double[size];
    for(int i=0; i < arr.length;i++){
      arr[i] = limit / (i+1);
    }
    return arr;
  }
}
```
### 1.6	Common Mistakes
- 1.  Length vs length()
  - To obtain length of a __String object__ str, we use the length() method
    - str.length()
    - String is a special type of array(Different array Class), it does not have the attribute, hence, need to use length method
  - To obtain length(size) of an __array__ arr, we use the length attribute
    - arr.length
- 2.  Array index out of range
  - Beware of __ArrayIndexOutOfBoundsException__
- 3.  No instantiate array objects
  - Beware of __NullPointerException__

1. Length vs length()
>length --- arrays (int[], double[], String[]) ---- to know the length of the arrays.
>
>length() --- String related Object (String, StringBuilder etc)to know the length of the String
>
>size() --- Collection Object (ArrayList, Set etc)to know the size of the Collection

2. Array index out of range
``` Java
//Out of bound issue
public static void main(String[] args){
  int [] numbers = new int[10];
  for(int i=0;i<= numbers.length;i++) //length can not be 10
}
```

3. No instantiate array objects

``` Java
//Mistake
Point[] array = new Point[3]; //Only create array, but Never instantiate the objects. So inside each array element, there is no Point Object, only Null
for(int i =0; i< array.length; i++){
    array[i].setLocation(1,2);
}    

//Correction
Point[] array = new Point[3];
for(int i=0;i<array.length;i++){
  array[i] = new Point();
  array[i] = setLocation(1,2);
}
```

### 1.7	2D Array
- A two-dimensional (2D) array is an array of array
- This allows for rows of different lengths.
  - `int [][]array2D = {{4,5,2},{1,3},{7,1,5,6}}`

``` Java
public class Test2DArray{
  public static void main(String[] args){
    int [][]array2D = {{4,5,2},{1,3},{7,1,5,6}};
    System.out.println("array2D.length = " + array2D.length);
    for(int i=0; i< array2D.length;i++){
      System.out.println("array2D[" + i + "].length = " + array2D[i].length);
    }
    for(int row = 0;row<array2D.length;row++){
      for(int col = 0;col<array2D[row].length;col++){
        System.out.print(array2D[row][col] + " ");
      }
      System.out.println();
    }
  }
}
```

### 1.8	Drawback
- Array has one major drawback:
  - Once initialized, the array size is fixed
  - Reconstruction is required if the array size changes
  - To overcome such limitation, we can use some classes related to array
