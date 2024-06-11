# Java fundamentals - advanced data Types

In this section we'll cover the following: Strings, Arrays, loops

## Strings

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

## Arrays

`Arrays` are used to store multiple values of a single data type in an indexed list. It is indexed such that the first item of the `Array` has the numerical value of `0` and it counts up from there.

There are two ways to initialize an `Array`:

1. Use curly brackets

```
<type>[] name = {1, 2, 3}

public class DataStructuresArray {
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

Here is the indexing visualised:

| Monday | Tuesday | Wednesday | Thursday | Friday |
| ------ | ------- | --------- | -------- | ------ |
| 0      | 1       | 2         | 3        | 4      |

2. Using the 'new' keyword requires you to specify the number of items in advance

```
String[] myLanguages = new String[4];

// Already has a .length of 4 before we have added the elements
System.out.println(myLanguages.length); // Don't use parenthesis for <Array>.length
>> 4

myLanguages[0] = "Python";
myLanguages[1] = "JavaScript";
myLanguages[2] = "Swift";
myLanguages[3] = "Ruby";

System.out.println(myLanguages[2]);
>> Swift

// In both versions we can replace a value like this
myLanguages[2] = "Java";

System.out.println(myLanguages[2]);
>> Java
```

Since Array's have a fixed length you cannot add or remove elements, you can only change the value of existing elements. There are a few tricks such as making a shorter copy of the Array excluding the element you want to remove or replacing the value with `null`. But generally, if you are working with an Array that you want to manipulate it is better to use an `ArrayList` rather than an Array.

## ArrayLists

You may find `ArrayLists` to be more appropriate in most cases as we often need to manipulate our data which may involve increasing or reducing its size. An `ArrayList` is a type of `List` that has many useful methods we can call on it.

To create an `ArrayList` we have to import it at the top of our page and then declare it using slightly differeny syntax to the `Array`.

```
import java.util.ArrayList;

ArrayList<Type> arrayListName= new ArrayList<>();

// Which becomes

ArrayList<Integer> myNumbers= new ArrayList<>();

```

Note that we use `Integer` rather than `int`. This is because you cannot declare an ArrayList with a primitive data type so we use `Integer` which is the parent class of `int` instead.

### add(), get(), set(), remove(), size()

```
ArrayList<String> anime = new ArrayList<>();

// Add new items:
anime.add("Naruto");
anime.add("One Piece");
anime.add("Full Mental Alchemist Brotherhood");

System.out.println("ArrayList: " + anime);
>> ArrayList: [Naruto, One Piece, Full Metal Alchemist Brotherhood]

// Get a single item by index
int indexOfNaruto = anime.indexOf("Naruto");
System.out.println("Naruto: " + anime.get(indexOfNaruto));
>> Naruto: Naruto

// Set method for replacing an item by index
int indexOfOnePiece = anime.indexOf("One Piece");
anime.set(indexOfOnePiece, "Hunter X Hunter")
System.out.println("ArrayList: " + anime);
>> ArrayList: [Naruto, Hunter X Hunter, Full Metal Alchemist Brotherhood]

// Remove elements by index
int indexOfFMAB = anime.indexOf("Full Metal Alchemist Brotherhood");
String fMAB = anime.remove(indexOfFMAB);
System.out.println("Updated ArrayList: " + anime);
>> Updated ArrayList: [Naruto, Hunter X Hunter]
System.out.println("Removed Element: " + fMAB);
>> Removed Element: Full Metal Alchemist Brotherhood

// Size returns the number of elements in the array
System.out.println("ArrayList count: " + anime.size());
>> : ArrayList count: 2
// Note that .size() returns the number of elements and .length returns the capacity
```

There are many more methods for manipulating ArrayLists but for now we're going to look at another method that will help us manipulate our arrays and much more.

## Loops

Loops are used to count and iterate. Java has multiple types of loop which have similar functionality but different syntax. First we are going to look at the `for` loop.

### for loop

The syntax is as follows:

```
for (start-count; condition; update-by) {
    // statement
}
```

To make a loop that counts from 1 to 10 we can do this:

```
int counter = 1;
for (counter; counter <= 10; counter++) {
    System.out.print(counter)
}

>> 12345678910
```

In this example we have initialized a counter at 1 and used it as our starting count:
`int counter = 1;`

Then we have set a condition stating that the loop will run if it is `True` that counter is less than or equal to 10:
`counter <= 10;` we start with 1 which evaluates to true `1 <= 10 >> True;`

When it is `True` the statement inside gets executed and we print the counter.
`System.out.print(counter);` which in this case is printing 1 `System.out.print(1);`

The the counter is incremented and we check the condition again:
`2 <= 10 >> True;` >> `System.out.print(2);`
`3 <= 10 >> True;` >> `System.out.print(3);`
`4 <= 10 >> True;` >> `System.out.print(4);`

This repeats until the counter is incremented to 10 and the condition returns false:
`11 <= 10 >> False;` >> exit loop

It is important to note that if we make a mistake with the condition we can accidentally cause an infinite loop. For example if we increment using >= instead of <= and start at 0 like this: `counter >= 0;` we would be saying `1 >= 0; >> True;`, `2 >= 0; >> True;` and so on. The loop would never end. This can crash our devices so be careful.

Make a for loop that counts down from 10 to 0 and prints each count to the console.

<details>
<summary>10-0 for loop</summary>

```
public class Loop {
    public static void main(String[] items) {
        for (int counter = 10; counter >= 0; 1--) {
            System.out.print(counter)
        }
    }
}
```

</details>
