- [1. foreach](#1-foreach)
- [2. params](#2-params)
- [3. static class](#3-static-class)
- [4. Access Modifiers](#4-access-modifiers)
- [5. Inheritance](#5-inheritance)
- [6. Method Overriding](#6-method-overriding)

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
# 4. Access Modifiers
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

# 5. Inheritance
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

# 6. Method Overriding
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
