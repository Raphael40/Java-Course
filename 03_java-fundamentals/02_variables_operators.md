# Java fundamentals - variables, operators, conditionals

If you are completely new to programming it is important to understand some primitve and non-primitive data types as well as the variables they are assigned to.

Variables are containers for storing data values of any data type (both primitive and non-primitive).

## Primitive data types

There are eight primitive data types in Java: `byte`, `short`, `int`, `boolean`, `char`, `long`, `float`, and `double`

When working with numbers we can use `byte`, `short`, `int`, and `long` where `byte` but `int` is the default.

With decimal point numbers, `float` and `double` are both available with `double` being the default.

The difference between all of these terms comes down to the range of numbers they can handle and the amount of storage they take up.

Following this we have `char` which is used to store a single character in single quotes. It is closely linked with the non-primitive data type; `String`, which is used for a sequence of characters. So in this case, 'H' (single quotes) is a `char` and "Hi" (double quotes) is a `String`. You will normally use `String`.

The final primitive data type is `boolean` which is used to represent either `true` or `false`. Booleans are commonly used for conditional statements and evaluating expressions.

### Variable declaration

A variable can store a data value which is helpful for reusing specific values, configuring programs to use dynamic data values, and improving readability throughout your code.

In order to assign a data to a variable, you have to state the data type and the name of the variable, then use the `=` assignment operator and provide the value.

For example, to assign the number 10 to a variable I would do this:

```
int myNumber = 10
```

Where `int` is the data type, myNumber is the name of the variable and it is being assigned the number 10 with the = assignment operator.

The rest follow the same pattern:

```
float myFLoat = 2.5;
char myLetter = 'B';
boolean myBoolean = true;
String myString = 'Kitten';
```

Refactor your `FirstClass` so that the text we printed is saved to a variable called `text`, then print the variable and run the code.

It should look like this:

<details>
<summary>FirstCLass</summary>

```
public class FirstClass {
    public static void main(String[] items) {
        String text = "This is my first class";
        System.out.println(text);
    }
}
```

</details>

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

## Operators

Operators are sets of syntax used to conduct operations between different pieces of data.

The assignment operator `=` is used to assign values to varibales. If a variable has already been declared you can use the `+=` or `-=` operators to reassign it with a new value:

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

---

[back](../README.md) <span style="float: right;">[next](03_conditionals.md)</span>
