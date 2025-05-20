- [1. foreach](#1-foreach)
- [2. params](#2-params)

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

