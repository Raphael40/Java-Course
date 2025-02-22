# Class Methods - OOP

In this lesson:

-   Static and instance methods
-   The return keyword
-   Using multiple classes

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
    Dog.bark("Bark Bark");
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
    Dog boris = new Dog("Boris", "Pug");
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
    System.out.println("Welcome to the Game!");
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
    System.out.println("Welcome to the Game!");
  }

}
```

Now we are able to specify our game when we create an instance. Update your main method accordingly:

```
public static void main(String[] args) {
  Game.welcome();

  Game sudoku = new Game("Sudoku");
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
    // Since the score always starts at 0 we can hard code it instead of passing it in as an argument.
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
  System.out.println("Your score for ".concat(this.name) + " is " + this.score)
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
    // Since the score always starts at 0 we can hard code it instead of passing it in as an argument.
  }

  public static void main(String[] args) {
    Game.welcome();

    Game sudoku = new Game("Sudoku");
    sudoku.addPoints(20);
    sudoku.displayScore();
  }

  public static void welcome() {
    System.out.println("Welcome to the Game!");
  }

  public void addPoints(int points) {
    this.score += points;
  }

  public void displayScore() {
    System.out.println("Your score for ".concat(this.name) + " is " + this.score);
  }
}

>> Welcome to the Game!
>> Your score for Sudoku is 20
```

### Void

The word `void`, which we have been seeing a lot of, is added in front of our method when we don't want the method to return anything. `return` is a keyword that can be used when we want to use the value that is formed inside a method. This can be easily demonstrated with an example.

Here is a class `Five` that has a void method `timesFive`:

```
public class Five {
  public static void main(String[] args) {
    Five.timesFive(5);
    Five.timesFive(6);
  }

  public static void timesFive(int num) {
    System.out.println(num * 5);
  }
}

>> 25
>> 30
```

If we want to use the result of this operation in our code we can refractor the `timesFive()` method to return the value.

Void is a keyword we use when the method does not return anything. If the method does return something, in this case an `int`, we simply replace void with int:

```
public class Five {
  public static void main(String[] args) {
    Five.timesFive(5)
    Five.timesFive(6)
  }

  public static int timesFive(int num) { // change this line
    return num * 5;
  }
}
```

Then we can access the return value by saving the method calls to a variable.

```
public class Five {
  public static void main(String[] args) {
    int number = Five.timesFive(5)
    int secondNumber = Five.timesFive(6)

    System.out.println("number: " + number + " secondNumber: " + secondNumber);
  }

  public static int timesFive(int num) {
    return num * 5;
  }

}

>> number: 25 secondNumber: 30
```

As you can see, we can now use the returned values in our main method. Lets add a multiply method which takes and multiplies two ints and pass in `number` and `secondNumber`:

```
public class Five {
  public static void main(String[] args) {
    int number = Five.timesFive(5)
    int secondNumber = Five.timesFive(6)

    System.out.println("number: " + number + " secondNumber: " + secondNumber);

    System.out.println(Five.multiply(number, secondNumber)); // use the values in another method
  }

  public static int timesFive(int num) {
    return num * 5;
  }

  public static int multiply(int number, int secondNumber) {
      return number * secondNumber;
  }

}

>> number: 25 secondNumber: 30
>> 750
```

As you develop more advanced programs, returning values will become the default behavious of your methods. It becomes much more obvious in an application with two or more classes as we will see next.

## Multiple classes - make more incremental?s

We can instantiate one class from another class. Here is a public class called `Patient`. It has no `main` method but does have a constructor and multiple instance methods so we know we are going to make instrances of this class. There are three mthods to return the instance values and one to update the condition variable:

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

Now lets make a second class called `Hospital` and give it a `main` method and `addPatient()` method which takes a `Patient` argument:

```
public class Hospital {

  public static void main(String[] args) {

  }

  public static void addPatient(Patient patient) {

  }

}

```

Now we can create an instance of our `Patient` class inside the `Hosital` class:

```
public class Hospital {

  public static void main(String[] args) {
    // Create instances of the Patient class
    Patient Rory = new Patient("Rory", 26);
    Patient Gina = new Patient("Gina", 24);

  }

  public static void addPatient(Patient patient) {

  }

}
```

From our `Hospital.main` method we can also call the `Patient` instance methods like `updateCondition()`:

```
public class Hospital {

  public static void main(String[] args) {
    Patient Rory = new Patient("Rory", 26);
    Patient Gina = new Patient("Gina", 24);

    Rory.updateCondition("food poisoning");
    Gina.updateCondition("Covid-19");
  }

  public static void addPatient(Patient patient) {

  }

}
```

Now we can give the Hospital its own functionality. Lets create an `ArrayList` called `patients` to store our `Patient` instances in. Use the `addPatient()` method to add them to the Arraylist:

```
import java.util.ArrayList;

public class Hospital {
  // Initialised with a type of Patient
  static ArrayList<Patient> patients = new ArrayList<>();

  public static void main(String[] args) {
    Patient Rory = new Patient("Rory", 26);
    Patient Gina = new Patient("Gina", 24);

    Rory.updateCondition("food poisoning");
    Gina.updateCondition("Covid-19");

    // Call the addPatient method, passing in the Patient instances
    Hospital.addPatient(Rory);
    Hospital.addPatient(Gina);
  }

  public static void addPatient(Patient patient) {
      patients.add(patient);
  }

}
```

Now that we have stored our data we want a way to retreieve it. Make a `listPatients()` method which loops through the `patients` ArrayList and prints of each Patient.You can call the the `get` methods of the Patient class within the loop.

<details>
<summary>Hospital class</summary>

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

    Hospital.listPatients(); // Don't forget to call the method
  }

  public static void addPatient(Patient patient) {
    // Add record made of data from Patients class to the patients array
    patients.add(record);
  }

  public static void listPatients() {
    // loop through the patients array and print each item
    for (Patient patient : patients) {
        System.out.println("Name: " + patient.getName() + " Age: " + patient.getAge() + " Condition: " + patient.getCondition());
    }
  }
}

>> Rory is 26 and has food poinsoning
>> Gina is 24 and has Covid-19
```

</details>

We have made a simple program using two classes which is a good example of Object Oriented Programming. The Patient instances are Objects and both classes have methods that manipulate their data.

---

In the next section we're going to have our first look at interfaces.

[back](../README.md) <span style="float: right;">[next](04_interfaces.md)</span>
