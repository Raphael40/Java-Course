# Conditionals

In this lesson:

-   If statements
-   If else statements
-   Else If statements

### If statements

The concept of the `if` statement is simple, we are writing a program that will execute a specific code block **if** a specified condition evaluates to true.

The syntax is as follows:

```
if (condition is true) {
    // Execute code in curly backets
}
```

Create a new package called `conditionals` and add a `Conditionals` class with a `main` method.

Try running the following code:

```
// If 10 is greater than 5
int ten = 10;

if (ten > 5) {
    System.out.println("I printed because it is true that 10 is greater than 5");
}
```

Any operation that evaluates to a boolean can be used as the conditional of an if statement.

```
int five = 5;
String six = "six";

if (five < 20 && six == "six") {
    System.out.println("Logical operators can be used in if statements");
}

```

### else

We can use the keyword `else` to add a secondary condition.

```
if (condition) {
    // Execute code in curly backets
} else {
    // Execute this second code block
}
```

If the condition equates to false, the code after the else will be run instead.

```
String cat = "Hendrix";

if (cat == "Caspian") {
    System.out.println("That's my cat, Caspian!");
} else {
    System.out.println("Oh nah that's not my cat");
}
```

### else if

We're not done, there's also `else if` statements that let us add even more conditions!

```
if (condition) {
    // Execute code in curly backets
} else if (second condition) {
    // Execute this second code block
} else {
    // Execute if first two both fail
}

String cat = "Hendrix";

if (cat == "Caspian") {
    System.out.println("That's my cat, Caspian!");
} else if (cat == "Hendrix") {
    System.out.println("Ah it's Hendrix");
} else {
    System.out.println("I do not know this cat");
}
```

In this scenario we have three different outcomes. If the cat is "Caspian" we print "That's my cat, Caspian!", if the cat is "Hendrix" we print "Ah it's Hendrix" and if the cat is neither "Caspian" nor "Hendrix" we print "I do not know this cat". Feel free to change the value of `cat` and see what happens.

### Switch

There is one more type of conditional called a `switch` statement. The syntax is (in my opinion) a little unusual but there are scanarios where it is more optimal and readble than an `if else` statement.

It is initialised with the `switch` keyword which takes an expression. It then has multiple cases that execute if the expression is equal to the value for each case. Then use the `break` keyword to exit the statement. We also have a `default` case which is similar to an `else` as it executes if none of the cases match the expression:

```
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

The switch is a good choice if you have a fixed number of options. Here is a basic example:

```
String day = "Friday";

switch(day) {
  case "Monday":
    System.out.println("The day today is" + day)
    break;
  case "Tuesday":
    System.out.println("The day today is" + day)
    break;
  case "Wednesday":
    System.out.println("The day today is" + day)
    break;
  case "Thursday":
    System.out.println("The day today is" + day)
    break;
  case "Friday":
    System.out.println("The day today is" + day)
    break;
  case "Saturday":
    System.out.println("The day today is" + day)
    break;
  case "Sunday":
    System.out.println("The day today is" + day)
    break;
  default:
    System.out.println("invalid day)
}
```

## Exercises

Check if a number is positive or negative

Check if a number is odd or even

Check if a person is 18 years old

Find the largest of three numbers

Grade calculation based on marks

In the next section we're going to look at loops which we can use to count and iterate through data.

---

[back](../README.md) <span style="float: right;">[next](04_loops.md)</span>
