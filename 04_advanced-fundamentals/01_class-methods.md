# Advanced fundamentals

In this section we'll learn about class methods and

## Class Methods

### Static Methods

Methods are integral to Java and we have already seen many built in methods such as the following String methods: `.length()`, `.concat()`, `toUpperCase()`. And the following ArrayList methods: `put()`, `get()`, `remove()`. They are characterised by the parenthesis.

A class method is something we write ourselves. We have already been using the `main()` method which is mandatory for each class but we haven't had to call it because it is called automatically due to its special nature. If we want we can use similar syntax to add more methods to our class other than the main method.

```
class Dog {

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
class Dog {

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
class Dog {

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
class Dog {

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
class Dog {

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
class Game {
  public static void main(String[] args) {

  }

  public static void welcome() {

  }

}
```

Next we can call the welcome method from our main and get it to print off a welcome message:

```
class Game {
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
class Game {
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
class Game {
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
class Game {
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
class Five {
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
class Five {
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
class Five {
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
