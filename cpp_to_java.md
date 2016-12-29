## A Crash Course from C++ to Java Notes

### Introduction:

* Construct an object: `new`, `Greeter gt = new Greeter()`

* `public static void main(String args[]){}`

* `System.out.println('')`

* How to compile:

  * `javac GreeterTest.java`
  * `java GreeterTest`

* Documentation: 

  * Example :![](http://i.imgur.com/7eAStE6.png)
  * `javadoc *.java`

* Math and String classes are very useful

* In Java, an object value is always a reference to an object or in other words, a value that describes the location of the object. 

* Reference means:

  ```java
  Greeter worldGreeter = new Greeter("Hello World");
  Greeter anotherGreeter = worldGreeter;
  // So anotherGreeter.setName("Dave") will change the value inside worldGreeter
  worldGreeter = null;
  if(worldGreeter == null){...}
  ```

* Parameter Passing: you can always change a state of a object(private/public member variable), but not the object's value. __Primitive types and object references__ are passed by value, not reference. 

* Packaging:

  ```java
  package edu.sjsu.cs151.alice;
  public class Greeter{
    ...
  }

  //=======import statement=======
  import java.util.ArrayList;
  // Then you can use ArrayList class directly by calling ArraList
  ```

* Package File directory:![](http://i.imgur.com/nAqriwq.png)

* ArrayList and Array:

  ```java
  // Looks like Java's version of std::vector
  ArrayList countries = new ArrayList();
  countries.add("Belgium");
  countries.add("Italy");
  countries.add("Thailand");
  countries.get(1); // return type = Object, the superclass of all Java classes
  countries.set(1, "France");
  countries.insert(1, "Genermay");
  countries.remove(2);
  // ArrayList means you can do both array and list things 
  // __DrawBack__: can only contains object, no primitive types;
  ```

  __Drawback__ of `ArrayList`: can only contains objects, no primitive types;

  This is __Why__ `Array` comes into play(__Array__ can hold anything):

  ```java
  int[] numbers = new int[3];
  int[][] numbers_2d = new int[3][4];
  Greeter[] greeters = new Greeters[10];
  int n = numbers.length; // which equals to 3; so args.length can be used to access any element in the array
  ```

* String:

  ```java
  String greeting = "Hello";
  char ch = greeting.charAt(1); // 
  ```

  Strings are __immutable__,  so __no__ `String.setCharAt()` method. 

  ```java
  String ss = "Hello".substring(1, 3); // which equals to "el"
  ```

  __Care__ should be taken when you use `==` for String comparison, because it just compare the location of objects instead of their contents. so you should use

  ```java
  if(greeting.equals("Hello")){...}
  ```

  __StringTokenizer__

  ```java
  StringTokenizer tokenizer = new StringTokenizer(countries, ",");
  while(tokenizer.hasMoreTokens()){
    String contries = tokenizer.nextToken();
  }
  ```

  __Concatenation__

  ```java
  int n = 7;
  String newHello = "Hello" + n; // like c++ but much more convenient
  Date now = new Date();
  String greeting = "Hello" + now; // end up being "Hello, Wed Jan 17 ....", toString() method will be called. 
  ```

* File I/O:

  ```java
  // console IO
  BufferReader console = new BufferReader(new InputStreamReader(System.in));
  System.out.println("How old are you?");
  String input = console.readLine();
  int count = Integer.parseInt(input);
  ```

* Static Methods:

  * Used across different objects of a class and cannot operate on objects(because there is only one)

    ```java
    // save space
    public class Greeter{
      //...
      private static Random generator = new Random(); // Constructed here???
    }

    public class Math{
      public static final PI = 3.1415926;
      //...
    }

    // Factory method
    public class Greeter{
      public static Greeter getRandomInstance(){
        if(generator.nextBoolean())
          return new Greeter("World");
        else
          return new Greeter("Mars");
      
      }
    }
    ```

* Programming Style:

  * `if (x > y)` instead of `if (x > y)`

  * `(int)x ` instead of `(int) x`

  *  use `getName()` or `setName()` to indicate setter or getter

    ​

  ​