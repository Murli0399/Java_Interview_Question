<details><summary>

## What are the default values in an array?
</summary>
The default values for arrays in Java depend on the data type of the elements. For example, the default values for each element of an array are:

- Integer, short, long, or byte: 0
- Double or float: 0.0
- String: null
- Boolean: false
- Char: Unicode (\u0000)
</details>
<details><summary>

##  How do you print the content of an array?
</summary>
There are two ways to print the contents of an array in Java:

- Using a for loop
- Using the Arrays.toString() method

### Using a for loop

1. Declare and initialize an array.
2. Create a for loop that iterates through the array.
3. Inside the for loop, print the current element of the array.

Example:
```
int[] array = {1, 2, 3, 4, 5};

for (int i = 0; i < array.length; i++) {
  System.out.println(array[i]);
}
```
### Using the Arrays.toString() method

1. Import the java.util.Arrays class.
2. Call the Arrays.toString() method on the array.
3. Print the result of the Arrays.toString() method.

Example:
```
import java.util.Arrays;

int[] array = {1, 2, 3, 4, 5};

System.out.println(Arrays.toString(array));
```

The output of both methods will be the same.
</details>
<details><summary>

## How do you compare two arrays?
</summary>
There are several ways to compare two arrays in Java. One way is to use the Arrays.equals() method. This method takes two arrays as parameters and returns true if the arrays are equal, or false if they are not equal. The arrays must be of the same type and size in order to use the equals() method.


Another way to compare two arrays is to use the Arrays.compare() method. This method takes two arrays as parameters and returns an integer value indicating the relationship between the arrays. The return value is 0 if the arrays are equal, -1 if the first array is less than the second array, or 1 if the first array is greater than the second array.

Finally, you can also compare two arrays by using a loop and comparing the elements of the arrays one by one. This method is less efficient than the equals() or compare() methods, but it can be used if you need to compare arrays of different types or sizes.

Here is an example of how to use the Arrays.equals() method to compare two arrays:
```
int[] array1 = {1, 2, 3};
int[] array2 = {1, 2, 3};

boolean equal = Arrays.equals(array1, array2);
```

In this example, the equal variable will be true because the two arrays are equal.

Here is an example of how to use the Arrays.compare() method to compare two arrays:
```
int[] array1 = {1, 2, 3};
int[] array2 = {1, 2, 4};

int result = Arrays.compare(array1, array2);
```

In this example, the result variable will be -1 because the first array is less than the second array.

Here is an example of how to compare two arrays by using a loop:
```
int[] array1 = {1, 2, 3};
int[] array2 = {1, 2, 4};

boolean equal = true;

for (int i = 0; i < array1.length; i++) {
  if (array1[i] != array2[i]) {
    equal = false;
    break;
  }
}
```

In this example, the equal variable will be false because the two arrays are not equal.
</details>
<details><summary>

## What is an enum?
</summary>

In Java, an enum is a special data type that enables for a variable to be a set of predefined constants. The variable must be equal to one of the values that have been predefined for it.

For example, an enum type for compass directions could have the constants NORTH, SOUTH, EAST, and WEST.

Enums are useful for representing a fixed set of constants, such as the days of the week or the colors of the rainbow. They can also be used to represent more complex concepts, such as the different types of exceptions that can occur in a program.

Here is an example of an enum in Java:
```
enum DaysOfWeek {
    Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday
}
```

This enum type defines the seven days of the week. You can create a variable of type DaysOfWeek and assign it one of the constants, such as:
```
DaysOfWeek today = DaysOfWeek.Monday;
```

Enums are a powerful tool that can help you to write more readable and maintainable code.
</details>
<details><summary>

## Can you use a switch statement around an enum?
</summary>

Yes, you can use a switch statement with an enum in Java. You can use enums in switch statements in Java like you would use int primitives. In a switch-case statement, a variable is tested against a set of constant values. If the variable matches a constant value, the corresponding code is executed.

You can also use enums with if statements and iterations.

Here are some things to keep in mind when using enums in switch statements:
- Enum constants are public, static, and final by default.
- You access enum constants using dot syntax.
- An enum class can have attributes and methods, in addition to constants.
- You cannot create objects of an enum class, and it cannot extend other classes.
</details>
<details><summary>

## What are asserts used for?
</summary>


</details>
<details><summary>

## When should asserts be used?
</summary>


</details>
<details><summary>

## What is tokenizing?
</summary>


</details>
<details><summary>

## Can you give an example of tokenizing?
</summary>


</details>
<details><summary>

## 
</summary>


</details>
