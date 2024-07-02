# Advanced fundamentals

In this section we'll learn about the difference between static and instance methods followed by the void and return keywords.

## Class Methods

### Static Methods

Methods are integral to Java and we have already seen many built in methods such as the following String methods: `.length()`, `.concat()`, `toUpperCase()`. And the following ArrayList methods: `put()`, `get()`, `remove()`. They are characterised by the parenthesis.

A class method is something we write ourselves. We have already been using the `main()` method which is mandatory for each class but we haven't had to call it because it is called automatically due to its special nature. If we want we can use similar syntax to add more methods to our class other than the main method.

```
public class Dog {

  // a normal main method signature
  public static void main(String[] args) {
    // call our static method
    Dog.woof();
  }

  // a static method that prints a String, but returns nothing
  public static void woof() {
    System.out.println("Woof Woof");
  }

}

>> Woof Woof
```

In the example above we have our main method which is called automatically and inside it we call `Dog.woof()` which refers to the `woof()` method we have made inside the `Dog` class. Being able to call woof directly on Dog is what makes the woof method static. This program will automatically print `Woof Woof` when run.

We can also pass arguments into our static methods.

```
public class Dog {

  // a normal main method signature
  public static void main(String[] args) {
    // call our static method
    Dog.woof();
    Dog.bark("Bark Bark")
  }

  // a static method that prints a String
  public static void woof() {
    System.out.println("Woof Woof");
  }

  // a static method that prints a String
  public static void bark(String bark) {
    System.out.println(bark);
  }

}

>> Woof Woof
>> Bark Bark
```

Here the bark method takes a String parameter called bark and prints it. We then call the `bark()` method on the Dog class in the main method and pass it the String `"Bark Bark"` as an argument.

You can have as many static methods as you want, but sometimes you may want to use an instance method which is used when an instance (or object) of the class is made.

### Instance Methods

To call an instance method we first need to instantiate our class into a variable like so:

```
<typeOfClass> name = new class()
```

Here he specify our `type` of variable which is equal to the name of the class and then we save a new instance of our class to the variable.

```
Dog boris = new Dog()
```

We now have an instance called boris which we can use to call instance methods

```
public class Dog {

  // a normal main method signature
  public static void main(String[] args) {
    // instantiate our class
    Dog boris = new Dog()
    boris.woof()
  }

  // an instance method is made when you don't specify 'static'
  public void woof() {
    System.out.println("Woof Woof");
  }

}

>> Woof Woof
```

This example shows how it's done but we haven't done anything that we couldn't do with a static method. The power of instance methods becomes more apparent when we start passing in values and using instance fields.

This is how we pass a value into our class instantiation

```
Dog boris = new Dog("Boris", "Pug")
```

Here we have given boris two values, name & breed. We instantiate them in the class using a constructor method which is a public method that has the same name as the class. The constuctor method is automatically called when an instance of the class is created using the `new` keyword. You can technically omitt the constructor but including it makes your code more efficient.

```
public class Dog {

  // type declarations
  String name;
  String breed;

  // constructor
  public Dog(String name, String breed) {
    // assigning the name instance field
    this.name = name;
    // assigning the breed instance field
    this.breed = breed;
  }

  public static void main(String[] args) {
    // instantiate our class
    Dog boris = new Dog("Pug");
    // call the breed method
    boris.breed();
  }

  public void breed() {
    System.out.println(this.name + " is a " + this.breed);
  }

}

>> Boris is a pug
```

Now we can do this with multiple instances of Dog.

```
public class Dog {

  // type declarations
  String name;
  String breed;

  // constructor
  public Dog(String name, String breed) {
    // assigning the name instance field
    this.name = name;
    // assigning the breed instance field
    this.breed = breed;
  }

  public static void main(String[] args) {
    Dog boris = new Dog("Boris", "Pug");
    Dog Thibault = new Dog("Thibault", "Spaniel"); // pronounced 'Tee-Boh'

    boris.breed();
    Thibault.breed();
  }

  public void breed() {
    System.out.println(this.name + " is a " + this.breed);
  }

}

>> Boris is a Pug
>> Thibault is a Spaniel
```

Lets try another one:

First we'll create a new class called Games, give it a main method and then create a static method called welcome:

```
public class Game {
  public static void main(String[] args) {

  }

  public static void welcome() {

  }

}
```

Next we can call the welcome method from our main and get it to print off a welcome message:

```
public class Game {
  public static void main(String[] args) {
    Game.welcome();
  }

  public static void welcome() {
    System.out.println("Welcome to the Game!")
  }

}
```

Next we want to make a constructor so we can create games:

```
public class Game {
  String name;

  // constructor
  public Game(String name) {
    this.name = name;
  }

  public static void main(String[] args) {
    Game.welcome();
  }

  public static void welcome() {
    System.out.println("Welcome to the Game!")
  }

}
```

Now we are able to specify our game when we create an instance. Update your main method accordingly:

```
public static void main(String[] args) {
  Game.welcome();

  Game sudoku = new Game("Sudoku")
}
```

It would be pretty cool if we could keep track of the score in our game. Lets create another instance field for the score.

```
public class Game {
  String name;
  int score;

  // constructor
  public Game(String name) {
    this.name = name;
    this.score = 0;
    Since the score always starts at 0 we can hard code it instead of passing it in as an argument.
  }
...
}
```

Great now every new Game we create will have a score of zero so naturally we want a way to update it.

Create an instance method called addPoints that takes a number of points and adds it to the score:

```
public void addPoints(int points) {
  this.score += points;
}
```

Now lets add another static method called displayScore so we can actually view our points:

```
public void displayScore() {
  System.out.println("Your score for ".concat(this.name) + " is ".concat(this.score))
}
```

Now all we need to do is call the methods in main:

```
public class Game {
  String name;
  int score;

  // constructor
  public Game(String name) {
    this.name = name;
    this.score = 0;
    Since the score always starts at 0 we can hard code it instead of passing it in as an argument.
  }

  public static void main(String[] args) {
    Game.welcome();

    Game sudoku = new Game("Sudoku")
    suduku.addPoints(20)
    sudoku.displayPoints()
  }

  public static void welcome() {
    System.out.println("Welcome to the Game!")
  }

  public void addPoints(int points) {
    this.score += points;
  }

  public void displayScore() {
    System.out.println("Your score for ".concat(this.name) + " is ".concat(this.score))
  }
}

>> Welcome to the Game!
>> Your score for Sudoku is 20
```

### Void

The word `void`, which we have been seeing a lot of, is added in front of our method when we don't want the method to return anything. `return` is a keyword that can be used when we want to use the value that is formed inside a method. This can be easily demonstrated with an example.

```
public class Five {
  public static void main(String[] args) {
    Five.isFive(5)
    Five.isFive(6)
  }

  public void timesFive(int num) {
    System.out.println(num * 5)
  }
}

>> 25
>> 30
```

We have a class Five with a main method that calls the timesFive method. At this point we print `num * 5` to the output. This is helpful for us as the viewer but what if we want to be able to use the result of this operation in our code? This is where we decide to return the value.

Void is a keyword we use when the method does not return anything. If the method does return something, in this case an `int`, we simply replace void with int:

```
public class Five {
  public static void main(String[] args) {
    Five.isFive(5)
    Five.isFive(6)
  }

  // use int instead of void
  public int timesFive(int num) {
    int product = num * 5;

    // return the value
    return product;
  }
}
```

Now we can access the return value in our main class by saving it to a variable.

```
public class Five {
  public static void main(String[] args) {
    int number = Five.isFive(5)
    int secondNumber = Five.isFive(6)

    // We can then use these variables however we see fit, e.g. passing them to other methods
    System.out.println(Five.multiply(number, secondNumber))
  }

  // use int instead of void
  public int timesFive(int num) {
    int product = num * 5;

    // return the value
    return product;
  }

  public int multiply(number, secondNumber) {
    return number * secondNumber
  }
}

>> 750
```

## Multiple classes - make more incremental?s

We can instantiate one class from another class:

```
public class Patient {
  String name;
  int age;
  String condition;

  public Patient(String name, int age) {
    this.name = name;
    this.age = age;
    this.condition = "unknown";
  }

  public void updateCondition(String condition) {
    this.condition = condition;
  }

  public String getName() {
    return this.name;
  }

  public int getAge() {
    return this.age;
  }

  public String getCondition() {
    return this.condition;
  }
}
```

Here we have a patient class that lets you instantiate a new patient with a name and age and then update their health. It also has three methods to retrieve this information.

We can make an instance of this class from our Hospital class:

```
import java.util.ArrayList;

public class Hospital {
  // A static ArrayList exists in the class
  static ArrayList<String> patients = new ArrayList<>();

  public static void main(String[] args) {
    // Create instances of the Patient class
    Patient Rory = new Patient("Rory", 26);
    Patient Gina = new Patient("Gina", 24);

    // Make changes to the patient class by calling the updateCondition method
    Rory.updateCondition("food poisoning");
    Gina.updateCondition("Covid-19");

    Hospital.addPatient(Rory);
    Hospital.addPatient(Gina);

    Hospital.listRecords();
  }

  public static void addPatient(Patient patient) {
    String record = patient.getName() + " is " + patient.getAge() + " years old and has: " + patient.getCondition();

    // Add record made of data from Patients class to the patients array
    patients.add(record);
  }

  public static void listRecords() {
    // loop through the patients array and print each item
    for (String record : patients) {
      System.out.println(record);
    }
  }
}

>> Rory is 26 and has food poinsoning
>> Gina is 24 and has Covid-19
```

The above two classes illustrates how one class with a main method can call methods from another class. This helps with separation of concerns and gives structure to the program.

**Note:** If Patient and Hospital are in the same package (e.g., the default package or another common package), you do not need an import statement.

Otherwise, you would have to import the the Patient at the top of the Hospital script with an import statement:

```
import root.path.Patient;

pubic class Hospital {
  ...
}
```

---

In the next section we're going to have our first look at testing.

[next](../04_advanced-fundamentals/02_testing-intro.md)

---

[back](../README.md) <span style="float: right;">[next](04_testing-intro.md)</span>
