## Loops

In this section:

-   For loop
-   While loop

### for loop

Loops are used to count and iterate. Java has multiple types of loop which have similar functionality but different syntax. First we are going to look at the `for` loop.

The syntax is as follows:

```
for (start-count expression; condition; update-counter) {
    // statement
}
```

Create a package called loops and make a class called `Iterators` with a `main` method.

To make a loop that counts from 1 to 10 we can do this:

```
for (int counter = 1; counter <= 10; counter++) {
    System.out.print(counter);
}

>> 12345678910
```

So whats happening?

In this example we have initialized a counter at 1 and used it as our starting count:
`int counter = 1;`

Then we have set a condition stating that the loop will run if it is `True` that counter is less than or equal to 10:
`counter <= 10;` we start with 1 which evaluates to true `1 <= 10 >> True;`

When it is `True` the statement inside gets executed and we print the counter.
`System.out.print(counter);` which in this case is printing 1 `System.out.print(1);`

The the counter is incremented by 1 and we check the condition again:
`2 <= 10 >> True;` >> `System.out.print(2);`
`3 <= 10 >> True;` >> `System.out.print(3);`
`4 <= 10 >> True;` >> `System.out.print(4);`

This repeats until the counter is incremented to 10 and the condition returns false:
`11 <= 10 >> False;` >> exit loop

It is important to note that if we make a mistake with the condition we can accidentally cause an infinite loop. For example if we increment using >= instead of <= and start at 0 like this: `counter >= 0;` we would be saying `1 >= 0; >> True;`, `2 >= 0; >> True;` and so on. The loop would never end. This can crash our devices so be careful.

Try making a for loop that counts down from 10 to 1 and prints `'launching in ' + counter` to the console. For a bonus print `Blast off!` at the end.

<details>
<summary>10-0 for loop</summary>

```
public class Iterators {
    public static void main(String[] args) {
        for (int counter = 10; counter >= 1; counter--) {
            System.out.println("launching in " + counter);
        }
        System.out.println("Blast off!");
    }
}
```

</details>

### while loop

There is one more type of loop which executes while a condition is true called a while loop. The syntax is as follows:

```
while (condition) {
  // code block to be executed

  // update counter
}
```

```
int counter = 0;

while (counter <= 5) {
  System.out.println(i);
  i++;
}

>> 0
>> 1
>> 2
>> 3
>> 4
>> 5
```

### Nested if statement

We can also place an if statement inside our loop.

Here we use an if statement to print off only odd numbers:

```
for (int counter = 1; counter <= 10; counter++) {
    if (counter % 2 == 1) {
        System.out.print(counter);
    }
}

>> 13579
```

## Exercises

Make a loop that prints `helloWorld` five times

Make a for loop that prints only even numbers up to 20

Make a while loop that prints multiples of 5 up to 100

Congratualtions you have finished the basics. In the next section we cover some ofthe more advanced fundamentlas starting with `Arrays`.

---

[back](../README.md) <span style="float: right;">[next](../04_advanced-fundamentals/01_arrays.md)</span>
