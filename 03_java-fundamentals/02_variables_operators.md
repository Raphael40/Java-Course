# Variables & Operators

In this section:

-   Data types
-   Assigning data values to Variables
-   What make Java striongly typed

### Primitive data types

There are eight primitive data types in Java:

Numeric data types include: `byte`, `short`, `int` and `long`. `int` is the default.

With decimal point numbers: `float` and `double` are both available with `double` being the default.

The difference between all of these types comes down to the range of numbers they can handle and the amount of storage they take up.

Following this we have `char` which is used to store a single character in single quotes. It is closely linked with the non-primitive data type; `String`, which is used for a sequence of characters. So in this case, 'H' (single quotes) is a `char` and "Hi" (double quotes) is a `String`. You will normally use `String`.

The final primitive data type is `boolean` which is used to represent either `true` or `false`. Booleans are commonly used for conditional statements and evaluating expressions.

### Variable declaration

Variables are containers for storing data values of any data type (both primitive and non-primitive).
A variable can store a data value which is helpful for reusing specific values, configuring programs to use dynamic data values, and improving readability throughout your code.

In order to assign a data to a variable, you have to state the data type and the name of the variable, then use the `=` assignment operator and provide the value.

For example, to assign the number 10 to a variable I would do this:

```
int myNumber = 10;
```

Where `int` is the data type, myNumber is the name of the variable and it is being assigned the number 10 with the = assignment operator.

The line always end with a semi-colon `;`

The rest follow the same pattern:

```
double myDouble = 2.5;
char myLetter = 'B';
boolean myBoolean = true;
String myString = "Kitten";
```

In the Java-fundamentals-starter branch of the supporting repo create a new package; `main/java/variables_and_operators` and inside it create a class called Variables.

It should look like this:

<details>
<summary>FirstCLass</summary>

```
public class Variables {
    public static void main(String[] items) {

    }
}
```

</details>

Copy this code into the file and run it:

```
int myNumber = 10;
double myDouble = 2.5;
char myLetter = 'B';
boolean myBoolean = true;
String myString = "Kitten";

System.out.println(myNumber);
System.out.println(myDouble);
System.out.println(myLetter);
System.out.println(myBoolean);
System.out.println(myString);
```

### More on Strings

**Strings** are non-primitive because they are objects of a `String` class which are represented by a collection of characters surrounded by double quotes. Because a `String` is a class it also has many methods which can be called upon it for a variety of results:

Create a `Cat` class in the variables_and_operators package.

<details>
<summary>FirstCLass</summary>

```
public class Cat {
    public static void main(String[] items) {

    }
}
```

</details>

Here are som epopular methods to call on strings:

```
String cat = "Caspian"; // Assign a String to a variable

// This will print the number of characters in a String
System.out.println(cat.length());
>> 7

// This one converts every character to a capital letter
System.out.println(cat.toUpperCase());
>> "CASPIAN";

// This returns true if a String starts with a specific letter.
System.out.println(cat.startsWith("C")); // We can pass values into the parenthesis of many methods
>> true;

```

You can also concatenate multiple Strings together. This can be confusing because it uses the `+` operator for concatenation rather than addition.

```
String cat = "Caspian";
String meow = "Meow";

// Add the strings together
String greeting = cat + " says " + meow + "!";
System.out.println(greeting);
>> Caspian says Meow!

// You can accomplish the same thing with the concat() method
String greeting2 = cat.concat(" says ").concat(meow).concat("!");
System.out.println(greeting2);
>> Caspian says Meow!

// We can even concatenate a String and an int
String fiftyStr = "50";
int fiftyInt = 50;
String fiftyFifty = fiftyStr + fiftyInt; // ints get coerced into Strings when concatenated
System.out.println(fiftyFifty);
>> "5050"
```

If you have to write text that uses double or single quotes you can use an escape character `\`:

```
String sentence = "And then cat went "Meow"";
>> error

 // Double quote escape with a backslash
String sentence = "And then the cat went \"Meow\"";
System.out.println(sentence);
>> And then the cat went "Meow"

// to write an actual backslash in Java use two of them
String backslash = "This is a backslash - \\";
System.out.println(backslash);
>> "This is a backslash - \"
```

## Operators

Operators are sets of syntax used to conduct operations between different pieces of data.

Create an `Operators` class with a `main` method.

The assignment operator `=` is used to assign values to varibales. We can also use `+=` or `-=` operators to reassign it with a new value:

```
int five = 5;

// Plus equals
System.out.println(five += 3);
>> 8

// Minus equals
System.out.println(five -= 2);
>> 6

// Times equals
System.out.println(five *= 2);
>> 12

// Divide equals
System.out.println(five /= 3);
>> 4
```

Following from this we have arithmetic operators. These are used for general mathematical operations and are similar to assignment operators but have different use cases:

```
int ten = 10;
int three = 3;

// Addition
System.out.println(ten + three);
>> 13

// Subtraction
System.out.println(ten - three);
>> 7

// Multiplication
System.out.println(ten * three);
>> 30

// Division
System.out.println(ten / three);
>> 3

// Modulus (remainder after one number is divided by the other)
System.out.println(ten % three);
>> 1

// Increment by 1
System.out.println(++ten);
>> 11

// Decrement by 1
System.out.println(--ten);
>> 9

```

The next group is comparison operators which are used to compare two values and output a boolean.

```
int five = 5;
int twenty = 20;

// Equal to
System.out.println(five == twenty);
>> false

// Not equal to
System.out.println(five != twenty);
>> true

// Greater than
System.out.println(five > twenty);
>> false

// Less than
System.out.println(five < twenty);
>> true

// Greater than or equals to
int alsoFive = 5;
System.out.println(five >= alsoFive);
>> true

// less than or equals to
System.out.println(five <= alsoFive);
>> true
```

The final group of operators are logical operators which evaluate true or false by comparing two statements.

```
int five = 5;
int six = 6;

// Logical && (and) returns true if both statements are true
System.out.println((five < 20 && six < 20));
>> true

System.out.println((five < 20 && six == five));
>> false

// Logical || (or) returns true if at least one statement is true
System.out.println((five < 20 || six == five));
>> true

// Logical ! (not) reverses a boolean
System.out.println(!true);
>> false

System.out.println(!(five == six));
>> true
```

Now that we know how to compare values we can put it into practice. In the next section we'll look at conditionals which depend on these operations.

## References

https://www.baeldung.com/java-char-vs-string

---

[back](../README.md) <span style="float: right;">[next](03_conditionals.md)</span>
