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

## Arrays
