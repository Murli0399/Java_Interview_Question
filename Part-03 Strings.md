<details><summary>
	
## Are all String’s immutable?
</summary>
A String is an unavoidable type of variable while writing any application program. String references are used to store various attributes like username, password, etc. In Java, String objects are immutable. Immutable simply means unmodifiable or unchangeable.

Once String object is created its data or state can't be changed but a new String object is created.
As Java uses the concept of String literal. Suppose there are 5 reference variables, all refer to one object "Sachin". If one reference variable changes the value of the object, it will be affected by all the reference variables. That is why String objects are immutable in Java.
</details>
	
<details><summary>
	
## Where are string values stored in memory?
</summary>
String is a class and strings in java treated as an object, hence the object of String class will be stored in Heap area. But depends on how we are create them. So we have two method for creating String value.

Approach 1
In the below example we are directly referencing a String literal.
	
	String str1 = "value";
This value will be stored in a "String constant pool" – which is inside the 
Heap memory. If compiler finds a String literal, JVM checks the if String constant pool if exists in the pool. it is reused.

Approach 2
However, if new operator is used to create string object, the new object is created on the heap. There will not be any case to reuse of values.

	//String Object - created on the heap
	String str2 = new String("value");
</details>
  
<details><summary>
	
## Why should you be careful about String Concatenation(+) operator in Loops?
</summary>
Using the string concatenation operator (+) inside loops can be inefficient and lead to performance issues. It is important to be careful when concatenating strings within loops because of the following reasons:

### String immutability
In Java, String objects are immutable, meaning their values cannot be changed once they are created. When you use the + operator to concatenate strings, a new String object is created for each concatenation operation. This can lead to unnecessary memory allocation and object creation inside the loop.

### String memory overhead
Each time a new String object is created through concatenation, the previous String objects are discarded, resulting in additional memory usage. In a loop with a large number of iterations, this can cause unnecessary memory overhead and impact performance.

### Time complexity
The time complexity of string concatenation using the + operator inside a loop is quadratic, meaning it grows exponentially with the number of iterations. For each concatenation operation, the entire concatenated string is copied into a new object, resulting in increasing time complexity. This can lead to significant performance degradation for large loops.

	String s3 = "Value1";
	String s2 = "Value2";

	for (int i = 0; i < 100000; ++i) {
		s3 = s3 + s2;
	}
How many objects are created in memory? More than 100000 Strings are created. 
This will have a huge performance impact.
</details>
  
<details><summary>
	
## How do you solve above problem?
</summary>
To solve the performance problem associated with string concatenation using the + operator inside loops, we can use the StringBuilder class. StringBuilder provides a mutable buffer for efficiently constructing strings by appending individual values. 
	
	StringBuffer s3 = new StringBuffer("Value1");
	String s2 = "Value2";

	for (int i = 0; i < 100000; ++i) {
		s3.append(s2);
	}
</details>
  
<details><summary>
	
## What are differences between String and StringBuffer?
</summary>
String objects are immutable, while StringBuffer objects are mutable.
String concatenation involves creating new String objects, while StringBuffer allows in-place modifications.
String is not thread-safe, while StringBuffer is synchronized and thread-safe.
StringBuffer is more memory-efficient for frequent modifications, while String objects may result in additional memory usage.
Use String when immutability is desired, and StringBuffer when frequent modifications are needed.
</details>
  
<details><summary>
	
## What are differences between StringBuilder and StringBuffer?
</summary>
StringBuilder is not thread-safe, while StringBuffer is thread-safe.
StringBuilder provides better performance due to the absence of synchronization.
Use StringBuilder in single-threaded scenarios or when manual synchronization is applied.
Use StringBuffer in multi-threaded scenarios where thread safety is required.
</details>
  
<details><summary>
	
## Can you give examples of different utility methods in String class?
</summary>
Certainly! The String class in Java provides a wide range of utility methods to perform various operations on strings. Here are some examples of commonly used utility methods in the String class:

	1. Length:
	int length(): Returns the length of the string.

	2.Concatenation:
	String concat(String str): Concatenates the specified string to the end of the current string.
	static String join(CharSequence delimiter, CharSequence... elements): Joins multiple strings using the specified delimiter.

	3. Substring:
	String substring(int beginIndex); //Returns a new string that is a substring of the current string, starting from the specified index.
	String substring(int beginIndex, int endIndex); //Returns a new string that is a substring of the current string, starting from the specified begin index and ending at the specified end index (exclusive).

	4. Case conversion:
	String toLowerCase(): //Converts the string to lowercase.
	String toUpperCase(): //Converts the string to uppercase.

	5. Character extraction:
	char charAt(int index): //Returns the character at the specified index in the string.
	int codePointAt(int index): //Returns the Unicode code point value of the character at the specified index.

	6. Comparison:
	boolean equals(Object obj): //Checks if the current string is equal to the specified object.
	boolean equalsIgnoreCase(String anotherString): //Checks if the current string is equal to the specified string, ignoring case.
</details>