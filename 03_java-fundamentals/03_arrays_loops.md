# Java fundamentals - advanced data Types

In this section we'll cover the following: Arrays, ArrayLists loops

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

### add(), get(), set(), remove(), clear()

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

// Clear the array of all elements.
ArrayList.clear()
System.out.println("ArrayList count: " + anime.size());
>> : ArrayList count: 0
// Note that .size() returns the number of elements and .length returns the capacity
```

If you know the exact length of your data then you should always use an `Array` as it takes less memory and improves performance. Otherwise, use an `ArrayList`.

There are many more methods for manipulating ArrayLists but for now we're going to look at another condional that will help us manipulate our arrays.

## Loops

Loops are used to count and iterate. Java has multiple types of loop which have similar functionality but different syntax. First we are going to look at the `for` loop.

### for loop

The syntax is as follows:

```
for (start-count; condition; update-counter) {
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

The the counter is incremented by 1 and we check the condition again:
`2 <= 10 >> True;` >> `System.out.print(2);`
`3 <= 10 >> True;` >> `System.out.print(3);`
`4 <= 10 >> True;` >> `System.out.print(4);`

This repeats until the counter is incremented to 10 and the condition returns false:
`11 <= 10 >> False;` >> exit loop

It is important to note that if we make a mistake with the condition we can accidentally cause an infinite loop. For example if we increment using >= instead of <= and start at 0 like this: `counter >= 0;` we would be saying `1 >= 0; >> True;`, `2 >= 0; >> True;` and so on. The loop would never end. This can crash our devices so be careful.

Make a for loop that counts down from 10 to 1 and prints `'launching in ' + counter` to the console. For a bonus print `Blast off!` at the end.

<details>
<summary>10-0 for loop</summary>

```
public class Loop {
    public static void main(String[] args) {
        for (int counter = 10; counter >= 1; 1--) {
            System.out.println('launching in ' + counter)
        }
        System.out.println('Blast off!')
    }
}
```

Ater the loop ends the code below it is read.

</details>

### Loop through an Array / ArrayList

To loop through an Array and print each item we can do this:

```
String[] chocolates = {"Dairy Milk", "Crunchie", "Yorkie", "Freddo"};

for (int counter = 0; counter <= chocolates.length - 1; counter++) {
    System.out.println(chocolates[counter]);
}

>> Dairy Milk
>> Crunchie
>> Yorkie
>> Freddo

```

chocolates.length is 4 but because the Arrays are indexed at 0 we want to count from 0-3 rather than 1-4 which is why state length - 1. We then use the counter to print each chocolate by index: `chocolates[0] >> Dairy Milk`, `chocolates[1] >> Crunchie` and so on.

However, Java gives us another, easier way to iterate through Arrays:

### for-each loop

```
String[] chocolates = {"Dairy Milk", "Crunchie", "Yorkie", "Freddo"};

for (String chocolate : chocolates) {
System.out.println(chocolate);
}

>> Dairy Milk
>> Crunchie
>> Yorkie
>> Freddo
```

In this example we can access a chocolate for each iteration of the chocolates array. It automatically runs the same number of iterations as there are items in the array.

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

## Exercises

Make a loop that prints `helloWorld` five times

Make a for loop that prints only even numbers up to 20

Make a while loop that prints multiples of 5 up to 100

Given an `Array` of names, print out `Good morning ` + name

Given an `Array` of days, print whether its a weekday or weekend.

Given an array of numbers print out the number and state its index. `number n at index i`

Given an `Array` of numbers, use a loop to find the sum of all the numbers

Given an `ArrayList` of animals get the animal with the longest name
// You can nest if statements inside loops

Given an `ArrayList` of animals, remove the rat

Do Fizzbuzz but it prints off every number in the range

[next](../04_advanced-fundamentals/01_class-methods.md)

---

## [back](../README.md)
