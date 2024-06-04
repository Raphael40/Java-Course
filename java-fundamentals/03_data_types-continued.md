# Java fundamentals - advanced data Types

In this section we'll cover the following non-primitive data types: Strings, Arrays, Hashes. The latter two can also be called data structures.

### Strings

**Strings** are essentially objects of the `String` class which are represented by a collection of characters surrounded by double quotes. Because a `String` is a class it also has many methods which can be called upon it for a variety of results:

```
String cat = "caspian";
System.out.println(cat.length());
>> 7

System.out.println(cat.toUpperCase());
>> "CASPIAN";

System.out.println(cat.startsWith("c"));
>> true;

```

You can also concatenate multiple Strings together. This can be confusing because it uses the `+` operator for concatenation rather than addition.

```
String h = "Hello";
String t = "there";

String greeting = h + " " + t + ", General Grevious"; // Add empty strings for spaces
System.out.println(greeting);
>> "Hello there, General Grevious"

// You can accomplish the same thing with the concat() method
String greeting2 = h.concat(" ").concat(t).concat(", General Grevious");
>> "Hello there, General Grevious"

// Add a String and an int
String fiftyStr = "50";
int fiftyInt = 50;
String fiftyFifty = fiftyStr + fiftyInt; // ints get coerced into Strings when concatenated
>> "5050"
```

Curious what happens when you add Strings and chars? Check section 5 of this [article](https://www.baeldung.com/java-char-vs-string)

If you have to write text that uses double or single quotes you can use an escape character:

```
String sentence = "And then main character said "This cereal is really tasty"";
>> error

// Double quote escape with a backslash
String sentence = "And then the main character said \"This cereal is really tasty\"";
System.out.println(sentence);
>> And then the main character said "This cereal is really tasty"

// Also used for single quotes
String text2 = "it\'s ok";

// to write an actual backslash in Java use two of them
String backslash = "This is a backslash - \\";
System.out.println(backslash);
>> "This is a backslash - \"
```

## Data Structures

### Arrays and ArrayLists

Make a new class called DataStructures.

<details>
<summary>With the terminal</summary>

```
cd exercises
touch DataStructures.java
```

Then add the class declaration:

```
package exercises;

public class DataStructures {

}

```

Finally add your main method

</details>

## Arrays and ArrayLists

`Array's` and `ArrayLists` are used to store multiple values of a single data type in an indexed list. It is indexed such that the first item of the `Array` has the numerical value of `0` and it counts up from there. The key difference between the two is that `Array's` are fixed in size while `ArrayList's` are dynamic and change in size.

There are two ways to initialize an `Array`:

1. Use curly brackets

```
public class DataStructures {
    public static void main(String[] args) {

        String[] workdays = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday"};
        // Fixed at length 5 because it was initialized with 5 items

        // You can access the first value by its index of 0
        System.out.println(workdays[0]);
        >> "Monday"

        System.out.println(workdays[3]);
        >> "Thursday"
    }
}
```

2. Using the 'new' keyword requires you to specify the number of items in advance

```
int[] numbersArray = new int[3];

// Assign the values
numbersArray[0] = 10;
numbersArray[1] = 40;
numbersArray[2] = 90;

// Get its length, don't use parenthesis for <Array>.length
System.out.println(numbersArray.length);
>> 3
```

Replace a value like this:

```
String[] goodLanguages = {"Python", "JavaScript", "Swift"};
goodLanguages[1] = "Java";
goodlanguages >> {"Python", "Java", "Swift"}

```

`ArrayLists` have a different functionality to `Arrays` as their size can be changed. Their declaration syntax is slightly different to what we have seen so far and we also have to import them at the top of our file to use them.

```
import java.util.ArrayList;
```
