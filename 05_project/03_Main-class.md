### Main class

Finally, we can do the `Main` class. This is where we will implement the built in `Scanner` class to get input from the user.

Lets start by creating a new class called `Main` and adding in a `main` method:

<details>
<summary>Main class</summary>

```
public class Main {
    public static void main(String[] args) {

    }
}
```

</details>

<br>

The `main` method will call other methods in the class so we have to write those first. Lets create a method that instantiates a `Movie` and adds it to the `MovieLibrary` called `addMovie()`.

This method will be private, static and wont return anything:

```
private static void addMovie() {

}
```

When this method is called it will print "Enter the title of the movie:" to the console. On the following line we use the `Scanner` to save the title to a variable using the `nextLine()` method of Scanner. Therefore, we also need to import Scanner at the top of our file and instantiate a new `Scanner` class:

```
import java.util.Scanner;

public class Main {
    final private static Scanner movieScanner = new Scanner(System.in); // Scanner instance

    public static void main(String[] args) {

    }


    private static void addMovie() {
      System.out.println("Enter the title of the movie:");
      String title = movieScanner.nextLine(); // Saves input to the title variable
    }
}
```

Now we can do the same to get the director, rating, and year:

```
private static void addMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();
    System.out.println("Enter the director of the movie:");
    String director = movieScanner.nextLine();
    System.out.println("Enter the rating of the movie:");
    double rating = movieScanner.nextDouble();
    movieScanner.nextLine(); // consume newline character
    System.out.println("Enter the year of the movie:");
    int year = movieScanner.nextInt();
    movieScanner.nextLine(); // consume newline character
}
```

Note that after we use `nextInt()` and `nextDouble()` we have to consume the newline character. Thats because they leave a string in the input that is automatically consumed by the next `nextLine()` call which can cause errors. Read more [here](https://www.freecodecamp.org/news/java-scanner-nextline-call-gets-skipped-solved/).

Now we create a new instance of movie, passing in the values:

```
private static void addMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();
    System.out.println("Enter the director of the movie:");
    String director = movieScanner.nextLine();
    System.out.println("Enter the rating of the movie:");
    double rating = movieScanner.nextDouble();
    movieScanner.nextLine();
    System.out.println("Enter the year of the movie:");
    int year = movieScanner.nextInt();
    movieScanner.nextLine();


    Movie movie = new Movie(title, director, rating, year);
}
```

And finally we create a new instance of MovieLibrary and call its `addMovie()` method, passing in our instance of `Movie`:

```
private static void addMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();
    System.out.println("Enter the director of the movie:");
    String director = movieScanner.nextLine();
    System.out.println("Enter the rating of the movie:");
    double rating = movieScanner.nextDouble();
    movieScanner.nextLine();
    System.out.println("Enter the year of the movie:");
    int year = movieScanner.nextInt();
    movieScanner.nextLine();

    Movie movie = new Movie(title, director, rating, year);
    MovieLibrary movieLibrary = new MovieLibrary(); // Movie library instance
    movieLibrary.addMovie(movie); // Passing movie into movieLibrary addMovie() method
    System.out.println("Movie Added") // Add this for confirmation
}
```

Since we want the `MovieLibrary` instance to be accessible by other methods of the class we can move it outside the `addMovie()` method, making it final, private, and static:

```
public class Main {
    final private static MovieLibrary movieLibrary = new MovieLibrary(); // move our instance here
    final private static Scanner movieScanner = new Scanner(System.in);

    public static void main(String[] args) {}


    private static void addMovie() {
        ...

        Movie movie = new Movie(title, director, rating, year);
        movieLibrary.addMovie(movie);
    }
}
```

To see your method in action you can call `addMovie()` in your `main` method:

```
public static void main(String[] args) {
    addMovie();
}
```

If you run it and type movie details into the input when prompted you should see this:

```
// << represents inputs

>> Enter the title of the movie:
<< Inception
>> Enter the director of the movie:
<< Christopher Nolan
>> Enter the rating of the movie:
<< 9.0
>> Enter the year of the movie:
<< 2010
>> Movie added.
```

We can improve our code with error handling. If we make an error such as entering a String when prompted for a double, we will see an `Exception` error like this:

```
>> Enter the title of the movie:
<< Alien
>> Enter the director of the movie:
<< Ridley Scott
>> Enter the rating of the movie:
<< not a double // This causes an error
>>  Exception in thread "main" java.util.InputMismatchException
      at java.base/java.util.Scanner.throwFor(Scanner.java:947)
      at java.base/java.util.Scanner.next(Scanner.java:1602)
      at java.base/java.util.Scanner.nextDouble(Scanner.java:2573)
      at main.java.Main.addMovie(Main.java:19)
      at main.java.Main.main(Main.java:10)

>> Process finished with exit code 1
```

However, if we use a `try/catch` statement we can catch the error and run our own code block instead.

```
try {
  //  Block of code to try
}
catch(Exception e) {
  //  I run if there is an error in the try block
}
```

Depending what we want to do you we could either throw an error with your our message:

```
import java.util.InputMismatchException;

...

catch (Exception e) {
    throw new InputMismatchException("Invalid input. Please enter the correct data types.");
}
```

Or we can print a message to the output:

```
catch (Exception e) {
    movieScanner.nextLine(); // In case there is a newline left in the input
    System.out.println("Invalid input. Please enter the correct data types.");
}
```

The difference is, in the first example a custom Exception will be thrown and we quit the program. In the second example we print our custom error message to the output but the program keeps running.

In our case it would be more suitable to use the latter and I will use that throughout the program. However, for this method I am going to throw an Exception just because I want to show you how to test for it later.

Incorporate a `try/catch` like this:

```
private static void addMovie() {
    try {
        System.out.println("Enter the title of the movie:");
        String title = movieScanner.nextLine();
        System.out.println("Enter the director of the movie:");
        String director = movieScanner.nextLine();
        System.out.println("Enter the rating of the movie:");
        double rating = movieScanner.nextDouble();
        movieScanner.nextLine();
        System.out.println("Enter the year of the movie:");
        int year = movieScanner.nextInt();
        movieScanner.nextLine();

        Movie movie = new Movie(title, director, rating, year);
        movieLibrary.addMovie(movie);
        System.out.println("Movie added.");
    } catch (Exception e) {
        throw new InputMismatchException("Invalid input. Please enter the correct data types.");
        // This will quit the program, which we can test later.

        // movieScanner.nextLine();
        // System.out.println("Invalid input. Please enter the correct data types.");
        // This line is more suitable and will be used inn the other methods.
    }
}
```

Now, when I make the same error as above I get this output:

```
>> Enter the title of the movie:
<< Alien
>> Enter the director of the movie:
<< Ridley Scott
>> Enter the rating of the movie:
<< not a Double // This causes an error
>> Invalid input. Please enter the correct data types. // From catch block
```

Lets move on to the next method; `rateMovie()`:

```
private static void rateMovie() {

}
```

In our `MovieLibrary` class we have a `rateMovie()` method which takes an instance of `Movie` and the new rating. We can use the `MovieLibrary.getMovieByTitle()` method to find the instance:

<details>
<summary>rateMovie() method title</summary>

```
private static void rateMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();
    Movie movie = movieLibrary.getMovieByTitle(title);
}
```

</details>

<br>

Then we can scan in the new rating:

<details>
<summary>rateMovie() method rating</summary>

```
private static void rateMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();
    Movie movie = movieLibrary.getMovieByTitle(title);

    System.out.println("Enter the new rating of the movie:");
    double rating = movieScanner.nextDouble();
    movieScanner.nextLine();
}
```

</details>

<br>

And finally we can call the `rateMovie()` method:

<details>
<summary>rateMovie() method call</summary>

```
private static void rateMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();
    Movie movie = movieLibrary.getMovieByTitle(title);

    System.out.println("Enter the new rating of the movie:");
    double rating = movieScanner.nextDouble();
    movieScanner.nextLine();

    movieLibrary.rateMovie(movie, rating);
    System.out.println("Movie rating updated.");
}
```

</details>

<br>

The logic is complete now we can give it some error handling. Nest in in a `try/catch` and use an if statement to check whether the instance of `Movie` is `null`:

<details>
<summary>rateMovie() method call</summary>

```
private static void rateMovie() {
    try {
       System.out.println("Enter the title of the movie:");
       String title = movieScanner.nextLine();

       Movie movie = movieLibrary.getMovieByTitle(title);
       if (movie == null) {
           System.out.println("Movie not found.");
           return;
       }

        System.out.println("Enter the new rating of the movie:");
        double rating = movieScanner.nextDouble();
        movieScanner.nextLine();

        movieLibrary.rateMovie(movie, rating);
        System.out.println("Movie rating updated.");
    } catch (Exception e) {
        movieScanner.nextLine();
        System.out.println("Invalid input. Please enter the correct data types.");
    }
}
```

</details>

<br>

Excellent, now lets move onto the next method; `listSingleMovie()`.

This method also uses the `getMovieByTitle()` method of the MovieLibrary class to get the instance of the desired movie:

```
private static void listSingleMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();

    Movie movie = movieLibrary.getMovieByTitle(title);


}
```

Now we have our instance of movie we can print it to the console by concatenating the instances methods; `getTitle()`, `getYear()`, `getDirector()`, `getRating()`:

```
System.out.println(movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
```

If we have previously made an instance of the Movie `Pulp Fiction` it would print this to the console:

```
Pulp Ficton (1994) - Quentin Tarantino - 9.2
```

Feel free to format this differently.

We can add in some error handling with a `try/catch` and an `if` statement in case `getMovieByTitle()` method returns null:

```
private static void listSingleMovie() {
    try {
        System.out.println("Enter the title of the movie:");
        String title = movieScanner.nextLine();

        Movie movie = movieLibrary.getMovieByTitle(title);
        if (movie != null) {
            System.out.println(movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
        } else {
            System.out.println("Movie not found.");
        }
    } catch (Exception e) {
        movieScanner.nextLine();
        System.out.println("Invalid input. Please enter the correct data types.");
    }
}
```

Try adding the method to `main`:

```
public static void main(String[] args) {
    addMovie();
    listSingleMovie();
}
```

We now only have two methods left, `listAllMovies()` and `removeMovie()`.

The `listAllMovies()` function should loop through our `movies` ArrayList in the `MovieLibrary` and return each `Movie`.

```
private static void listAllMovies() {
    for (Movie movie : movieLibrary.getMovies()) {}
}
```

Then we print of the movie in the same format as the previous method:

```
private static void listAllMovies() {
    for (Movie movie : movieLibrary.getMovies()) {
        System.out.println(movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
    }
}
```

I personally want to see a numbered list so lets add a counter:

<details>
<summary>listAllMovies() method</summary>

```
private static void listAllMovies() {
    int count = 1;
    for (Movie movie : movieLibrary.getMovies()) {
        // Add count to print then increment
        System.out.println(count + ": " + movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
        count++;
    }
}
```

</details>

<br>

And finally we can implement our error handling:

<details>
<summary>listAllMovies() method error handling</summary>

```
private static void listAllMovies() {
    try {
        if (movieLibrary.getMovies().isEmpty()) {
            System.out.println("No movies found.");
            return;
        }

        int count = 1;
        for (Movie movie : movieLibrary.getMovies()) {
            System.out.println(count + ": " + movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
            count++;
        }
    } catch (Exception e) {
        movieScanner.nextLine();
        System.out.println("Invalid input. Please enter the correct data types.");
    }
}
```

</details>

<br>

Lets add it to `main` and see if it works:

```
public static void main(String[] args) {
    addMovie();
    addMovie();
    addMovie();
    listAllMovies();
}
```

Our final method `removeMovie()`. Our `MovieLibrary.removeMovie()` method takes a `Movie` instance so lets scan in our title and use `movieLibrary.getMovieByTitle()` to get the instance we want to delete:

<details>
<summary>removeMovie() method</summary>

```
private static void removeMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();

    Movie movie = movieLibrary.getMovieByTitle(title);
}
```

</details>

<br>

Then, if `movie != null` we pass our movie into the `removeMovie()` method:

<details>
<summary>removeMovie() method</summary>

```
private static void removeMovie() {
    System.out.println("Enter the title of the movie:");
    String title = movieScanner.nextLine();

    Movie movie = movieLibrary.getMovieByTitle(title);
    if (movie != null) {
        movieLibrary.removeMovie(movie);
        System.out.println("Movie removed.");
    } else {
        System.out.println("Movie not found.");
    }
}
```

</details>

<br>

And complete it with our usual error handling:

<details>
<summary>removeMovie() method complete</summary>

```
public static void removeMovie() {
    try {
        System.out.println("Enter the title of the movie:");
        String title = movieScanner.nextLine();

        Movie movie = movieLibrary.getMovieByTitle(title);
        if (movie != null) {
            movieLibrary.removeMovie(movie);
            System.out.println("Movie removed.");
        } else {
            System.out.println("Movie not found.");
        }
    } catch (Exception e) {
        movieScanner.nextLine();
        System.out.println("Invalid input. Please enter the correct data types.");
    }
}
```

</details>

<br>

Lets try it in `main`:

```
public static void main(String[] args) {
    addMovie();
    addMovie();
    listAllMovies(); // Lists 2 movies
    removeMovie() // Input the title of an already added movie
    listAllMovies(); // Lists 1 movie
}
```

We have finished all our methods but we still don't have a functioning program. To complete the `Movie-Rating-App` we have to implement a proper control structure in the `main` method.

To do this we are going to use a `while` loop which runs as long as a `boolean` variable `running` is equal to `true`. Within the while loop we can implement an `if` statement to call different methods in the program.

Create `while` loop:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {

    }
}
```

Now we want to display our options to the user, here are the options:

1. Add Movie
2. Rate Movie
3. List Single Movie
4. List Movies
5. Remove Movie
6. Exit

To avoid making the `main` method too bulky we can make a new static method called printOptions where we print this list to the output:

```
private static void printOptions() {
    System.out.println("1. Add movie");
    System.out.println("2. Rate movie");
    System.out.println("3. List single movie");
    System.out.println("4. List movies");
    System.out.println("5. Remove movie");
    System.out.println("6. Exit");
}
```

Now we can call this method in the main class:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {
        printOptions()
    }
}
```

The user should be able to input a number to select one of the options so we can use `Scanner.nextInt()` for this:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {
        printOptions()
        int choice = movieScanner.nextInt();
        movieScanner.nextLine(); // Don't forget to consume the newline!
    }
}
```

Now that our user has given their input we can use an `if` statement to call the methods:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {
        printOptions()
        int choice = movieScanner.nextInt();
        movieScanner.nextLine(); // Don't forget to consume the newline!
        if (choice == 1) {
            addMovie();
        } else if (choice == 2) {
            rateMovie();
        } else if (choice == 3) {
            listSingleMovie();
        } else if (choice == 4) {
            listAllMovies();
        } else if (choice == 5) {
            removeMovie();
        }
    }
}
```

And finally we can add in choice 6 which exits the program by changing the `running` variable to false:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {
        printOptions();
        int choice = movieScanner.nextInt();
        movieScanner.nextLine();
        if (choice == 1) {
            addMovie();
        } else if (choice == 2) {
            rateMovie();
        } else if (choice == 3) {
            listSingleMovie();
        } else if (choice == 4) {
            listAllMovies();
        } else if (choice == 5) {
            removeMovie();
        } else if (choice == 6) {
            System.out.println("Exiting...");
            running = false;
        } else {
            System.out.println("Invalid choice."); // also check for invalid
        }
    }
}
```

### MainTest class

Testing `Main` is more advanced and therefore completely **optional**

It is challenging for two reasons; first the methods are private and not directly accessibly by JUnit. Second we are using the `Scanner` class which takes user input.

To test a private method we can use something called `reflection` which provides methods that can bypass security measures to inspect and modify code.

To use reflection add this at the top of your test file: `import java.lang.reflect.Method;`.

Regarding Scanner, we can use a library that lets create mock user input called [System Stubs](https://github.com/webcompere/system-stubs).

Download the core dependency: `uk.org.webcompere:system-stubs-core:2.1.6`
Then download the JUnit 5 extension: `uk.org.webcompere:system-stubs-jupiter:2.1.6`

Lets do the first one bit by bit. If we generate our `MainTest` file and then import DisplayName and reflection we should have something like this:

```
package main.java;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

import java.lang.reflect.Method;

import static org.junit.jupiter.api.Assertions.*;

class MainTest {

    @Test
    @DisplayName("addMovie test")
    void addMovie() throws Exception {

    }
}
```

Notice that we declare the test method with `throws Exception`. This is required because we are using `reflection` which can cause Exceptions when bypassing security measures to call the addMovie() method.

Now we want to retrieve our addMovies() method. We can use `Main.class` to target the Main class and then call `.getDeclaredMethod()` which is used to obtain a specified method. In order to save the value we need to assign it to a variable of the `Method` class. Our code will look like this:

```
Method method = Main.class.getDeclaredMethod("addMovie");
```

Now that we have our `addMovie()` method assigned to a variable we can call methods on it.

The `setAccessible()` method sets the access of a method, true is `public` and false is `private`. We will set it to true:

```
Method method = Main.class.getDeclaredMethod("addMovie");
method.setAccessible(true);
```

And now we want to call the method. We can do this with the `invoke()` method:

```
Method method = Main.class.getDeclaredMethod("addMovie");
method.setAccessible(true);
method.invoke(null);
```

It takes a `null` argument because it is expecting an instance to be passed in but since `addMovies()` is static it doesn't have an instance so we just pass in null.

Now that we are able to call our method we want to test it. Lets first setup a mock input for System.in:

```
@Test
@DisplayName("addMovie test")
void addMovie() throws Exception {
 String inputs = "test title\ntest director\n5.0\n2021\n"; // add this line


   Method method = Main.class.getDeclaredMethod("addMovie");
   method.setAccessible(true);
   method.invoke(null);

}
```

Now we can use System Stubs. We want to create a global mock SystemIn object. To do this we have to add the extension to our test class:

```
import org.junit.jupiter.api.extension.ExtendWith; // Required

import uk.org.webcompere.systemstubs.jupiter.SystemStubsExtension; // extension

...

@ExtendWith(SystemStubsExtension.class) // Add the extension
class MainTest {
    ...
}
```

Now that we have done this we can add a `@SystemStub` annotation field which we can use to inject a stubbed instance of SystemIn into our test class:

```
import uk.org.webcompere.systemstubs.jupiter.SystemStubsExtension;
import uk.org.webcompere.systemstubs.jupiter.SystemStub; // import SystemStub
import uk.org.webcompere.systemstubs.stream.SystemIn; // and SystemIn

...

@ExtendWith(SystemStubsExtension.class)
class MainTest {

    @SystemStub //
    private SystemIn systemIn;

    ...
}
```

Now that everything is setup we can return to the method. We want to set our inputs to the SystemIn inputStream.

Normally the System class works by taking inputs and converting them to `bytes` which is a unit of digital information.

We can use `ByteArrayInputStream(byte[] args)` to create an input stream of bytes but it expects and Array of bytes to be passed into it so first we have to convert our `inputs` String into a bytes Array using `inputs.getBytes()`.

And finally we pass the InputStream bytes object into our actual System input stream using `setInputStream()`:

```
import java.io.ByteArrayInputStream; // add this to your imports

@ExtendWith(SystemStubsExtension.class)
class MainTest {

    @SystemStub //
    private SystemIn systemIn;

    @Test
    @DisplayName("addMovie test")
    void addMovie() throws Exception {

    String inputs = "test title\ntest director\n5.0\n2021\n"; // add this line

    systemIn.setInputStream(new ByteArrayInputStream(inputs.getBytes())); // add this line

    Method method = Main.class.getDeclaredMethod("addMovie");
    method.setAccessible(true);
    method.invoke(null);

    }

}

```

With that we have successfully created a fake user input.

In order to confirm that our method has run successfully we make our assertions on the lines printed to `System.out`:

First we can add a new stub for SystemOut:

```
import uk.org.webcompere.systemstubs.stream.SystemOut; // import at the top

@SystemStub
private SystemOut systemOut;
```

Then we can call the SystemOut.getText() method to retrieve all text printed to the output:

```
@Test
    @DisplayName("addMovie test")
    void addMovie() throws Exception {

    String inputs = "test title\ntest director\n5.0\n2021\n";

    systemIn.setInputStream(new ByteArrayInputStream(inputs.getBytes()));

    Method method = Main.class.getDeclaredMethod("addMovie");
    method.setAccessible(true);
    method.invoke(null);

    String output = systemOut.getText(); // add this line
    }
```

And finally we can call our assertions on the output String:

```
@Test
    @DisplayName("addMovie test")
    void addMovie() throws Exception {

    String inputs = "test title\ntest director\n5.0\n2021\n";

    systemIn.setInputStream(new ByteArrayInputStream(inputs.getBytes()));

    Method method = Main.class.getDeclaredMethod("addMovie");
    method.setAccessible(true);
    method.invoke(null);

    String output = systemOut.getText();
    assertTrue(output.contains("Enter the title of the movie:"));
    assertTrue(output.contains("Enter the director of the movie:"));
    assertTrue(output.contains("Enter the rating of the movie:"));
    assertTrue(output.contains("Enter the year of the movie:"));
    assertTrue(output.contains("Movie added."));
    }
```

Try running it, your test should pass. If there are any issues try recompiling both this `MainTest` file and the `Main` file by going to `build > Recompile MainTest.java`.

Before we test for the error there are a few things we need to setup to prevent our tests from intefering with one another. They all use the same `SystemIn` and `SystemOut` so we can clear these in a beforeEach:

```
@BeforeEach
void setUp() {
    systemIn.setInputStream(new ByteArrayInputStream(new byte[0]));
    systemOut.clear();
}
```

It also helps to have our tests run in order one by one. If they are computing at the same time with the same `System` it can cause errors. We can use `@TestMethodOrder(MethodOrderer.OrderAnnotation.class)` to set an order for our methods to run.

And then specify the order of each test using `@Order(1) > @Order(2)...` like this:

```
@ExtendWith(SystemStubsExtension.class)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class) // Add this
class MainTest {

    ...

    @Test
    @Order(1) // Add this
    @DisplayName("addMovie test")
    void addMovie() throws Exception {
        ...
    }
}
```

Now that we're fairly sure our tests are isolated. Lets create the `addMovieError()` method:

```
@Test
@Order(2) // Runs second
@DisplayName("addMovieError test")
void addMovieError() throws Exception { // throws Exception

    // The inputs String is different, it enters "not a double" instead of a double
    String inputs = "test title\ntest director\nnot a double\n2021\n";
    // This is the same
    systemIn.setInputStream(new ByteArrayInputStream(inputs.getBytes()));

    // these two reflection lines are the same
    Method method = Main.class.getDeclaredMethod("addMovie");
    method.setAccessible(true);

}
```

Now things are going to chang, remember how in the `Movie` test we had to use a lambda to control when the error was caught. We do a similar thing here. We still use `assertThrows(ExceptionType.class, Lambda method)` but this time with extra steps.

Instead of `InputMismatchException.class` we use `InvocationTargetException.class` because this is the type of Exception thrown by `method.invoke()` when the method it invokes throws an error. It acts as a wrapper containig our actual error inside. We pass `() -> method.invoke(null)` as our lambda.

We can save this to an instance of the Throwable class which is the superclass of all errors and exceptions in Java:

```
Throwable thrown = assertThrows(InvocationTargetException.class, () -> method.invoke(null));
```

And then make a new instance of the `Throwable` class to save our actual error using `.getCause()` which returns the cause of an exception or error:

```
Throwable actualError = thrown.getCause();
```

Now we have our error saved to a variable we can make our assertions. First to make sure we actually have an `InputMistmatchException` we can use `assertInstanceOf`:

```
assertInstanceOf(InputMismatchException.class, actualError);
```

And second to check for our message we can use `assertEquals`:

```
assertEquals("Invalid input. Please enter the correct data types.", actualError.getMessage().trim());
```

Your entire `MainTest` file should now look like this:

```
package main.java;

import org.junit.jupiter.api.*;
import org.junit.jupiter.api.extension.ExtendWith;

import java.io.ByteArrayInputStream;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.InputMismatchException;

import uk.org.webcompere.systemstubs.jupiter.SystemStubsExtension;
import uk.org.webcompere.systemstubs.jupiter.SystemStub;
import uk.org.webcompere.systemstubs.stream.SystemIn;
import uk.org.webcompere.systemstubs.stream.SystemOut;

import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(SystemStubsExtension.class)
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
class MainTest {

    @SystemStub
    private SystemIn systemIn;

    @SystemStub
    private SystemOut systemOut;

    @BeforeEach
    void setUp() {
        systemIn.setInputStream(new ByteArrayInputStream(new byte[0]));
        systemOut.clear();
    }

    @Test
    @Order(1)
    @DisplayName("addMovie test")
    void addMovie() throws Exception {
        String inputs = "test title\ntest director\n5.0\n2021\n";
        systemIn.setInputStream(new ByteArrayInputStream(inputs.getBytes()));

        Method method = Main.class.getDeclaredMethod("addMovie");
        method.setAccessible(true);
        method.invoke(null);

        String output = systemOut.getText();
        assertTrue(output.contains("Enter the title of the movie:"));
        assertTrue(output.contains("Enter the director of the movie:"));
        assertTrue(output.contains("Enter the rating of the movie:"));
        assertTrue(output.contains("Enter the year of the movie:"));
        assertTrue(output.contains("Movie added."));
    }

    @Test
    @Order(2)
    @DisplayName("addMovieError test")
    void addMovieError() throws Exception {
        String inputs = "test title\ntest director\nnot a double\n2021\n";
        systemIn.setInputStream(new ByteArrayInputStream(inputs.getBytes()));

        Method method = Main.class.getDeclaredMethod("addMovie");
        method.setAccessible(true);

        Throwable thrown = assertThrows(InvocationTargetException.class, () -> method.invoke(null));
        Throwable actualError = thrown.getCause();

        assertInstanceOf(InputMismatchException.class, actualError);
        assertEquals("Invalid input. Please enter the correct data types.", actualError.getMessage().trim());
    }
}
```

We are going to finish here as this shoud give you a good idea of how to test a private method with user input. If you wish to see the rest of the testing file feel free to check out my code in the [completed repo]().

---

That is the end of this module and hopefully you have a good sense for the langauge and how it is used.

In module 2 we will start building more ambitious apps with Spring Boot.

## References

https://www.baeldung.com/java-junit-testing-system-in
https://www.baeldung.com/java-system-stubs
https://www.baeldung.com/java-reflection
https://mvnrepository.com/artifact/uk.org.webcompere/system-stubs-jupiter
https://www.programiz.com/java-programming/bytearrayinputstream

---

## [back](../README.md)
