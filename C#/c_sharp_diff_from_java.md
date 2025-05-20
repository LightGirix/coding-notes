# C# difference from Java: Note Syllabus
- [1. foreach](#1-foreach)
- [2. params](#2-params)
- [3. static class](#3-static-class)
- [4. Multi-Dimensional Array](#4-multi-dimensional-array)
- [5. Access Modifiers](#5-access-modifiers)
- [6. Inheritance](#6-inheritance)
- [7. Method Overriding](#7-method-overriding)
- [8. List](#8-list)
- [9. Getter/Setter](#9-gettersetter)
- [10. Generics](#10-generics)
- [11. Delegates](#11-delegates)
- [12. ?-Involved Operators](#12--involved-operators)
  - [12.1. Null-Coalescing Operators](#121-null-coalescing-operators)
  - [12.2. Null-Conditional Operators](#122-null-conditional-operators)
- [Others](#others)

Note: I have studied Java before so if you've got no basics about C#, find a video to watch. This'll cover only the differences between C# and Java.

# 1. foreach 
Is a range-based for loop in C# Here's the syntax:
```C#
String[] names = {"A", "B", "C"};

foreach (String name in names)
{
  Console.WriteLine(name);
}
```
Output
```
A
B
C
```

# 2. params
Is a keyword that tells that the method can take a variable number of arguments of a specific data type. Here's the syntax:
```C#
static int addAll(params int[] numbers) // This must only be a single-dimensional array
{
  int sum = 0;
  foreach (int i in numbers)
  {
    sum += i;
  }
  return sum;
}
```
Now I know you're wondering: How is this different from using an array???
Pay attention to how I send in arguments
```C#
Console.WriteLine(addAll(1,2,3,4,5,6));
```
Instead of sending in an array, I can send any amount of the same data type into the function.
Output:
```
21
```
Note: without params, you'd have to send in this instead:
```C#
new int[] {1, 2, 3, 4, 5, 6}
```

# 3. static class
In java we know static method, static variable, but we can't define a class as static  But we can now do it in C#.

Well, to be simple, static class is a class that **cannot be instantiated** and **all methods and variables** must also be static.

```C#
static class Ghost
{
  static string name;
  static void Haunt()
  {
    Console.WriteLine("YOU CAN NEVER ESCAPE!!!");
  }
}
```

Static classes are often ultility classes, one example of that is the Math class.

# 4. Multi-Dimensional Array
These kinds of array `int[][]`, `int[][][]` do exists in C#, these are called **jagged arrays**, the word **multi-dimensional array** 
is actually used to call these:

`int[,]`, `int[,,]`

Which, on basic functionality like looping through and assigning values, they can do the exact same thing.

The main differences comes to how the memory is allocated when defining these arrays, with the multidimensional array, **the memory is allocated as a single regtangular block and is allocated as a whole**, instead of being allocated independently for each sub-array (which has the top-level array contain pointers to them). Performance-wise, multidimensional arrays is better than jagged arrays.

# 5. Access Modifiers
- `public` accessible from anywhere
- `private` accessible only within the same class
- `protected` accessible within the same class and derived (child) class
Same as java, but not for the following:
- `internal` accessible within the same assembly (project)
- `protected internal` accessible within the same assembly or by derived class in any assembly
- `private protected` accessible only in the same class or derived classes in the same assembly

Java would treat any blank modifier as `package`, but for C#, here's the default access modifier if you left them blank:
- `internal` on top-level class
- `private` on class members

# 6. Inheritance
Not much, basically if there's this class:
```C#
public class Dragon
{
  public void Roar()
  {
    Console.WriteLine("The Dragon Roars!");
  }
}
```
Doing this
```C#
public class Drake : Dragon
```
Is equivalent to this in Java
```java
public class Drake extends Dragon
```

# 7. Method Overriding
Not much, just a bit more complicated than Java.

In Java, you could just override a method right away by declaring a method with the same name and same return type as the superclass. (Perhaps add the `@Override` overhead too)

Here's how you do that in C#
```C#
public class Dragon
{
  public virtual void Roar()
  {
    Console.WriteLine("The Dragon Roars!");
  }
}
public class Drake : Dragon
{
  public override void Roar()
  {
    Console.WriteLine("The Drake Roars!");
  }
}
```
- `virtual` declares that a method is overrideable, without this there'll be an error when attempting to override the method.
- `override` is name-wise, declares an overriding method. Simple.

# 8. List
`List<>` is the data type that represents a dynamic array , same as `ArrayList<>` in java, figure it out yourself.

Note: We do have `ArrayList` here, but you have to cast the data type every time you call an element from it which is slow and wasteful in performance.

# 9. Getter/Setter
With this line of code above with following fields:
```C#
public class Dragon {
  private String name;
  private int age;
```

In java, you'd follow it with this:
```java
  public String getName() {
    return name;
  }
  public void setName(String name) {
    this.name = name
  }
  public int getAge() {
    return age;
  }
  public void setAge(int age) {
    this.age = age;
  }
}
```

But in C# there's this thing called **property** that makes writing getter/setter easier. A property shares the name of
the field that you're using getter/setter on.

This is how we do it in C# continuing from the example code:
```
public String Name { get; set; } //Auto-implemented, works as the java version
```
There! You got the getter/setter for that field!

Or if you wanna specify how it works:

```C#
public String Name
{
  get
  {
  //Your code here
  }
  set
  {
  //Your code here 2
  }
}
```
Note: you can also have just the getter or the setter alone by omitting one that you don't want `... { get; }` or  `... { set; }`
but not both of them since that means they won't be recognized as a property, thus causing a syntax error.

# 10. Generics
See the `<>` in `List<>`? That's what we call a generic. A generic lets you define classes, methods, interfaces, and delegates (see [delegates](#11-delegates)) **without specifying the data type**, allow them to be used with any data types (unless you specify its constraints).

Generic Class
```C#
public class Computer<T>
{
  private T data;

  public T value { get; set;}

}
```

Generic Method
```C#
public void shout<T>(T thing)
{
  Console.WriteLine($"Shouting {thing}");
}
```

Generic constraints uses the `where` keyword after everything but before the `{`

```C#
public class Utility
{
    // T must implement IComparable<T>
    public static T GetMax<T>(T a, T b) where T : IComparable<T>
    {
        return a.CompareTo(b) > 0 ? a : b;
    }
}
```

# 11. Delegates
A delegate is a type that references to a method, its importance is that **it allows a method to be passed as a parameter** in another method.

For example: (Taken from: [](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/))
```C#
public delegate int PerformCalculation(int x, int y);
```
Now that we declare a delegate this can now contain any method with the **same parameter list** as the delegate.

Next, if we have these methods:

```C#
public int Add(int a, int b) {
  return a - b;
}

public int Subtract(int a, int b) {
  return a - b;
}
```

We can now do this!
```C#
int a = 5;
int b = 3;

PerformCalculation calc; //Declaration

calc = Add; //calc now acts as Add
Console.WriteLine(calc(a, b)); //Will return 8

calc = Subtract; //calc now acts as Subtract
Console.WriteLine(calc(a, b)); //Will return 2
```

Now, let's try passing the method as a parameter!
```
public void DoOperation(int a, int b, PerformCalculation p) {
  Console.WriteLine(p(a, b));
}
```

```
Console.WriteLine(DoOperation(a, b, Add); //Will return 8
Console.WriteLine(DoOperation(a, b, Subtract); //Will return 2
```
PS. This is meant to be an example, don't make a method like this one!

# 12. ?-Involved Operators

## 12.1. Null-Coalescing Operators
There's two of them that you need to know `??` and `??=`

- `??` is a binary operator which **returns the value of the left operand if it's not null** and returns the right value vice versa.
  ```
  value = someValue ?? backupValue //If someValue happens to be null, backupValue will be assigned to value instead
  ```
- `??=` assigns the value of its right-hand operand to its left-hand operand only **if the left-hand operand evaluates to null**
  ```
  nullValue ??= someValue //someValue is assigned.
  notNullValue ??= someValue //someValue is not assgined. notNullValue remains the same.
  ```

## 12.2 Null-Conditional Operators 
There's two of them that you need to know (again) `?.` and `?[]`

The two of them works the same but:
`?.` is for member access.
`?[]` is for element access.

How it works is that: it allows member/element access only if the object preceding it is not null, otherwise it returns `null`.

For example: A is an object that has object B as their public field, B also has object C as their public field.

If I write:
```
var Test = A?.B?.C
```
As you can see, if A or B is null, then the entire thing will be null. This is done to prevent errors in case of something 
has a chance to be null. This can chained with `??` to provide a backup in case of null. I won't provide an example of the `?[]`.

# Others

Things you need to know more:

- `Thread` works the same here!
- `Dictionary<TKey, TValue>` do exists as a mapping data type
- Many more!
