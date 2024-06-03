# Java fundamentals - advanced data types

In this section we'll cover the following non-primitive data types: Strings, Arrays, Objects. Other non-primitive data types include Classes which are covered in the next section, Interfaces, and Enumerations which we look at later in the course.

## Strings

We briefly touched on these in the previous section but `Strings` are essentially objects of the `String` class represented by a collection of characters surrounded by double quotes. Because it is a class it also has methods which can be called upon it for a variety of results.

```
String cat = "caspian";
cat.length();
>> 7

cat.toUpperCase();
>> "CASPIAN";

cat.startsWith("c");
>> true;

```

Plus many more.

You can also concatenate multiple Strings together. This can be confusing because it uses the `+` operator for concatenation rather than addition.

```
String h = "Hello";
String t = "there";

String greeting = h + " " + t + ", General Grevious"; // Add empty strings for spaces
>> "Hello there, General Grevious"

// Concat method
String greeting = h.concat(" ").concat(t).concat(", General Grevious");
>> "Hello there, General Grevious"

String fiftyStr = "50";
int fiftyInt = 50;
String fiftyFifty = fiftyStr + fiftyInt; // ints get coerced into Strings when concatenated
>> "5050"
```

If you have to write text that uses double or single quotes you can use an escape character:

```
String text = "And then main character said "This cereal is really tasty""
>> error

// Double quote escape with a backslash
String text = "And then main character said /"This cereal is really tasty/""
>> And then main character said "This cereal is really tasty"

// Also used for single quotes
String text2 = "it\'s ok"

// to write an actual backslash in Java use two of them
String backslash = "this is a backslash - \\"
>> "this is a backslash - \"
```

## Arrays and ArrayLists

`Array's` and `ArrayLists` are used to store multiple values of a single data type in an indexed list. It is indexed such that the first item of the `Array` has the numerical value of `0` and it counts up from there. The key difference between the two is that `Array's` are fixed in size while `ArrayList's` are dynamic and change in size.

To initialize a new `Array` you specify the data type of the contents and add square brackets. There are two ways of doing it:

1. Use curly brackets

```
String[] workdays = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday"};
// Fixed at length 5 because it was initialized with 5 items

// You can access the a value by it's index
workdays[0]
>> "Monday"

workdays[3]
>> "Thursday"
```

2. Using the 'new' keyword requires you to specify the number of items in advance

```
int[] numbersArray = new int[3];

// Assign the values
marks[0] = 10;
marks[1] = 40;
marks[2] = 90;

```

Replace a value like this:

```
String[] goodLanguages = {"Python", "JavaScript", "Swift"}
goodLanguages[1] = "Java"
goodlanguages >> {"Python", "Java", "Swift"}
```

`ArrayLists` are different as their size can be changed and they have to be imported.
