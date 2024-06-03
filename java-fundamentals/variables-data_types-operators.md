# Java fundamentals - variables, data types and operators

If you are completely new to programming it is important to understand some primitve and non-primitive data types as well as the variables they are assigned to. If this is not your first language you likely already know the majority of this module.

Variables are containers for storing data values of any data type (both primitive and non-primitive).

### Primitive data types

There are eight primitive data types in Java: `byte`, `short`, `int`, `boolean`, `char`, `long`, `float`, and `double`

When working with numbers we can use `byte`, `short`, `int`, and `long` where `byte` stores the shortest range of numbers in the least amount of space and `long` stores the broadest range of numbers in the largest amount of space. `int` is the default data-type used for storing numbers.

When working with decimal point numbers, `float` and `double` are both available with `double` being used for numbers with a larger number of decimal places. Generally `double` is the default.

Following this we have `char` which is used to store a single character in quotes. It is closely linked with the non-primitive data type; `String`, which is used for a sequence of characters. So in this case, 'H' (single quotes) is a `char` and "Hi" (double quotes) is a `String`. So what happens if we add a char and a char, a String and a char, and a String and a String? Well you can find the answers in section 5 of this [article](https://www.baeldung.com/java-char-vs-string) as chars have numeric values that make it confusing.

The final primitive data type is `boolean` which is used to represent either `true` or `false`. Booleans are commonly used for conditional statements and evaluating expressions.

### Variable declaration

In order to assign data to a variable, you have to state the data type, the name of the variable, use the `=` assignment operator and provide the value.

For example, to assign a numbe to a variable I would do this:

```
int myNumber = 10
```

Where `int` is the data type, myNumber is the name of the variable and it is being assigned the number 10 with the = assignment operator.

This is how to declare other data types:

```
float myFLoat = 2.5;
char myLetter = 'B';
boolean myBoolean = true;
String myString = 'Kitten';
```

**_Why do we use variables_**

> > We assign values to variables because it lets us store data, reuse values, configure programs to use dynamic data values, and improve readability. These will all become apparent once we start programming.

### Operators

Operators are sets of syntax used to conduct operations between different pieces of data.

The assignment operator `=` is used to assign values to varibales. If a variable has already been declared you can use the `+=` or `-=` operators to reassign it with a new value:

```
int a = 5;

// Plus equals
a += 3;
>> 8

// Minus equals
a -= 2;
>> 6

// Times equals
a *= 2;
>> 12

// Divide equals
a /= 3;
>> 4
```

Following from this we have arithmetic operators. These are used for general mathematical operations and are similar to assignment operators but have different use cases:

```
int a = 10;
int b = 3;

// Addition
int sum = a + b;
>> 13

// Subtraction
int subtract = a - b;
>> 7

// Multiplication
int multiply = a * b;
>> 30

// Division
int divide = a / b;
>> 3

// Modulus (remainder after one number is divided by the other)
int remainder = a % b;
>> 1

// Increment
int increment = a;
increment++;
>> 11

// Decrement
int decrement = a;
decrement--;
>> 9

```

The next group is comparison operators which are used to compare two values and output a boolean.

```
int a = 5;
int b = 20;

// Equal to
a == b;
>> false

// Not equal to
a != b;
>> true

// Greater than
a > b;
>> false

// Less than
a < b;
>> true

// Greater than or equals to
int c = 5;
a >= c;
>> true

// less than or equals to
a <= c;
>> true
```

The final group of operators are logical operators which evaluate true or false by comparing two statements.

```
int five = 5;
int six = 6;

// Logical && (and) returns true if both statements are true
(five < 20 && six < 20);
>> true

(five < 20 && six == five);
>> false

// Logical || (or) returns true if at least one statement is true
(five < 20 || six == five);
>> true

// Logical ! (not) reverses a boolean
!true;
>> false

!(five == six);
>> true
```

In the next section we're going to look at non-primitive data types.

[next](../java-fundamentals/advanced-data_types.md)

---

## [back](../README.md)
