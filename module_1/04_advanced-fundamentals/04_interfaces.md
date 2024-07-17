# Interfaces

In this lesson:

-   What are Interfaces?
-   Creating Interfaces
-   Built-in Interfaces

## What are interfaces?

An interface is a simplified abstract class that is implemented by other classes. They are always static and contain methods and variables. Interfaces are good for writing abstract, reusable and secure code.

We can decalre an interface with the `interface` keyword like this:

```
interface interfaceName {
    // declare constant fields
    // declare abstract or static methods
    // by default.
}
```

## GameCharacter interface

Lets imagine we are making an adventure game. Part of that game involves making characters like Warrior and Mage:

```
package main.java.Interfaces;

public class Warrior {
    private String characterType;

    public Warrior() {
        this.characterType = "Warrior";
    }
}
```

```
package main.java.Interfaces;

public class Mage {
    private String characterType;

    public Mage() {
        this.characterType = "Mage";
    }
}
```

Both of these classes represent similar concepts and the next step would be to give them the same methods such as `attack()` and `defend()`. In the future we may also want to add many more chacters that have the same methods like Archer etc. In order to keep track of all these classes and emthods we can make a `GameCharacter` interface that is implemented in each class.

Create a new .java file and call it `GameCharacter` then declare an interface:

```
package main.java.Interfaces;

public interface GameCharacter {

}
```

Since we want to give both our `Warrior` and `Mage` classes an `attack()` and `defend()` method we can add them to the interface:

```
public interface GameCharacter {
    void attack();
    void defend();
}
```

Now we can go to our `Warrior` and `Mage` classes and implement the class:

```
public class Warrior implements GameCharacter { // Implement the GameCharacter interface
    private String characterType;

    public Warrior() {
        this.characterType = "Warrior";
    }
}
```

```
public class Mage implements GameCharacter { // Implement tje GameCharacter interface
    private String characterType;

    public Mage() {
        this.characterType = "Mage";
    }
}
```

Notice that as soon as we implement the interface in our classes we get an error this error `Class 'Warrior' must either be declared abstract or implement abstract method 'attack()' in 'GameCharacter'`.

Now out class is required to implement the `attack()` method:

```
public void attack() {
    System.out.println("Warrior attacks!");
}
```

After adding this the message will change to say you must imlement the `defend()` method:

```
public void defend() {
    System.out.println("Warrior attacks!");
}
```

We can add a method to our `interface` that must return a value like `String` like this:

```
interface GameCharacter {
    void attack();
    void defend();
    String getCharacterType();
}
```

Now if we tried to implement the `getCharacterType()` method in our Warrior class with a return type of `void` liek this:

```
public void getCharacterType() {
    return this.characterType;
}
```

We get an error saying there is a clash with the interface because we have an incompatible return type. Change the return type to `String` and add the method to the `Mage` class.

We can still add methods to our `Warrior` and `Mage` classes that are not included on the interface.

Add `WarriorSpecialAttack()` method to your Warrior class:

```
public String warriorSpecialMove() {
    return "Warrior Whirlwind attack!";
}
```

Notice how this doesn't cause any errors, however it is now hard to differentiate between the methods implemented from our `GameCharacter` interface and methods unique to the `Warrior` class. This is why it is good practice to mark which methods are implementations of an interface using the `@override` keyword above each method declaration.

```
public class Warrior implements GameCharacter{
    private String characterType;

    public Warrior() {
        this.characterType = "Warrior";
    }

    @Override
    public void attack() {
        System.out.println("Warrior attacks!");
    }

    @Override
    public void defend() {
        System.out.println("Warrior defends!");
    }

    @Override
    public String getCharacterType() {
        return this.characterType;
    }

    // you will get an error if you place an @override here
    public String warriorSpecialMove() {
        return "Warrior Whirlwind attack!";
    }
}
```

`@override` can also help catch errors if the implemented method doesn't match a method in the interface.

Create a `Game` class with a `main` method and instantiate your characters in it:

```
public class Game {
    public static void main(String[] args) {
        Warrior warrior = new Warrior();
    }
}
```

We can now use the methods in each instance as usual:

```
System.out.println(warrior.getCharacterType());
warrior.attack();
warrior.defend();
System.out.println(warrior.warriorSpecialMove());

>> Warrior
>> Warrior attacks!
>> Warrior defends!
>> Warrior Whirlwind attack!
```

We can also create static methods with method bodies in our interface. Lets create a method called `printCharacterInfo()` which takes `GameCharacter` instance and calls the `getCharacterType()`, `attack()` and `defend()` methods:

```
interface GameCharacter {
    void attack();
    void defend();
    String getCharacterType();

    static void printCharacterInfo(GameCharacter character) {
        System.out.println("Character Type: " + character.getCharacterType());
        character.attack();
        character.defend();
    }
}
```

This method will now only take instances of classes that implement the `GameCharacter` interface:

```
public class Game {
    public static void main(String[] args) {
        Mage mage = new Mage();

        GameCharacter.printCharacterInfo(mage);
    }
}

>> Character Type: Mage
>> Mage attacks!
>> Mage defends!
```

Some additional points:

1. A class can inherit from multiple interfaces. For example a `Dog` class could inherit from both an `Animal` interface and a `Friend` interface: public class Dog implements Animal, Pet {}
2. One interface can `extend` another interface, adding functionality to it. For example an `Animal` interface could have `eat()` and `sleep()` methods and a `FlyingAnimal` interface could extend it: `public interface FlyingAnimal extends Animal {}` and declare a new `fly()` method. Now any class, such as `Bird` that implements `FlyingAnimal` must use the `eat()`, `sleep()`, and `fly()` methods.

## Built in interfaces

The **Java Collections Framework** which is part of the `java.util` package (usable in any project because it is located in the JDK) contains a collection of interfaces that we are already familiar with:

-   List
-   Map
-   Set

The `List` interface is implemented in classes like `ArrayList`, `LinkedList` and `SingletonList` which are all slight variations of each other and have different use cases.

`Map` is implemented in `HashMap`, `TreeMap`, and `LinkedHashMap` classes (and more).

`Set` is similar to a `List` but the classes that implement it cannot contain duplicate elements. It can be implemented in `HashSet`, `TreeSet` and `LinkedHashSet`

As a beginner you do not need to know every interface and every class in the Java Collections Framework. You will gradually become familiar with them and their use cases over time.

---

In the next section we're going to have our first look at testing.

[next](../04_advanced-fundamentals/02_testing-intro.md)

---

[back](../README.md) <span style="float: right;">[next](04_testing-intro.md)</span>
