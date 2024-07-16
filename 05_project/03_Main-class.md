### Main class

Finally, we can do the `Main` class. This is where we will implement the built in `Scanner` class to get input from the user.

Lets start by creating a new class called `Main` and adding in a `main` method:

```
public class Main {
    public static void main(String[] args) {

    }
}
```

Then we want to instantiate our `MovieLibrary` class as an instance field and assign it inside the main method. Don't forget to pass an `ArrayList` into it:

```
public class Main {
    private static MovieLibrary movieLibrary;

    public static void main(String[] args) {

        List<Movie> movies = new ArrayList<>();
        movieLibrary = new MovieLibrary(movies);

    }
}
```

The `main` method will call other methods in the class so we have to write those first. Lets create two methods, one that takes user input and returns a `Movie` instance and another that takes a `Movie` instance and adds it to the `MovieLibrary`. We can call them `enterMovieDetails()` and `addToMovieLibrary()`:

This method will be private, static and wont return anything:

```
private static Movie enterMovieDetails() {

}

private static void addMovie(Movie movie) {

}
```

When this method is called it will print "Enter the title of the movie:" to the console. On the following line we use the `Scanner` to save the title to a variable using the `nextLine()` method of Scanner. Therefore, we also need to import Scanner at the top of our file and instantiate a new `Scanner` class:

```
import java.util.Scanner;

public class Main {
    final private static Scanner movieScanner = new Scanner(System.in); // Scanner instance

    public static void main(String[] args) {

    }


    private static Movie enterMovieDetails() {
      System.out.println("Enter the title of the movie:");
      String title = movieScanner.nextLine(); // Saves input to the title variable
    }
}
```

Now we can do the same to get the director, rating, and year:

```
private static Movie enterMovieDetails() {
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

private static void addMovie(Movie movie) {

}
```

Note that after we use `nextInt()` and `nextDouble()` we have to consume the newline character. Thats because they leave a string in the input that is automatically consumed by the next `nextLine()` call which can cause errors. Read more [here](https://www.freecodecamp.org/news/java-scanner-nextline-call-gets-skipped-solved/).

Now we return a new instance of movie, passing in the values:

```
private static Movie enterMovieDetails() {
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


    return new Movie(title, director, rating, year);
}

private static void addMovie(Movie movie) {

}
```

In our `addToMovieLibrary()` method we can call the `addMovie()` method of our `MovieLibrary` class:

```
private static Movie enterMovieDetails() {
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


    return new Movie(title, director, rating, year);
}

private static void addToMovieLibrary(Movie movie) {
    movieLibrary.addMovie(movie);
    System.out.println("Movie added.");
}
```

To see your method in action you can call `enterMovieDetails()` and `addToMovieLibrary()` in your `main` method:

```
public static void main(String[] args) {
    Movie movie = enterMovieDetails();
    addToMovieLibrary(movie);
}
```

If it's successful you should be prompted so give an input. The console should look like this:

`<<` represents inputs

```

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

Depending what we want to do you we could either use to the catch block to throw an error with your our message:

```
import java.util.InputMismatchException;

...
try {
    ...
} catch (Exception e) {
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

The difference is, in the first example a custom Exception will be thrown and we quit the program. In the second example there is no Exception thrown and instead we print our custom message to the output. Thiskeeps the program keeps running.

In our case, it would be more suitable to use the latter so that the program keeps running and we can try entering a movie again.

Incorporate a `try/catch` like this:

```
public static Movie enterMovieDetails() {
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

        return new Movie(title, director, rating, year);
    } catch (Exception e) {
        movieScanner.nextLine();
        System.out.println("Invalid input. Please enter the correct data types.");
        return null;
    }
}
```

Now, when we make the same error as above we get this output:

```
>> Enter the title of the movie:
<< Alien
>> Enter the director of the movie:
<< Ridley Scott
>> Enter the rating of the movie:
<< not a Double // This causes an error
>> Invalid input. Please enter the correct data types. // From catch block
```

For the `addToMovieLibrary()` method we can also add a try/catch block:

```
public static void addToMovieLibrary(Movie movie) {
    try {
        movieLibrary.addMovie(movie);
        System.out.println("Movie added.");
    } catch (Exception e) {
        System.out.println("Movie could not be added to the MovieLibrary.");
    }
}
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
            System.out.print("\n");
            System.out.println(movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
            System.out.print("\n");
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
    Movie movie = enterMovieDetails();
    addToMovieLibrary(movie);
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

        System.out.print("\n");
        int count = 1;
        for (Movie movie : movieLibrary.getMovies()) {
            System.out.println(count + ": " + movie.getTitle() + " (" + movie.getYear() + ") - " + movie.getDirector() + " - " + movie.getRating());
            count++;
        }
        System.out.print("\n");
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
    Movie movie = enterMovieDetails();
    addToMovieLibrary(movie);
    Movie movie2 = enterMovieDetails();
    addToMovieLibrary(movie2);
    Movie movie3 = enterMovieDetails();
    addToMovieLibrary(movie3);
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
    Movie movie = enterMovieDetails();
    addToMovieLibrary(movie);
    Movie movie2 = enterMovieDetails();
    addToMovieLibrary(movie2);
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

Now that our user has given their input we can use aa `switch` statement to call the methods:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {
        printOptions()
        int choice = movieScanner.nextInt();
        movieScanner.nextLine(); // Don't forget to consume the newline!
        switch (choice) {
            case 1:
                Movie movie = enterMovieDetails();
                addToMovieLibrary(movie);
                break;
            case 2:
                rateMovie();
                break;
            case 3:
                listSingleMovie();
                break;
            case 4:
                listAllMovies();
                break;
            case 5:
                removeMovie();
                break;
        }
    }
}
```

And finally we can add in choice 6 which exits the program by changing the `running` variable to false as well as a default option:

```
public static void main(String[] args) {
    boolean running = true;

    while (running) {
        printOptions();
        int choice = movieScanner.nextInt();
        movieScanner.nextLine();
        switch (choice) {
            case 1:
                Movie movie = enterMovieDetails();
                addToMovieLibrary(movie);
                break;
            case 2:
                rateMovie();
                break;
            case 3:
                listSingleMovie();
                break;
            case 4:
                listAllMovies();
                break;
            case 5:
                removeMovie();
                break;
            case 6:
                System.out.println("Exiting...");
                running = false;
                break;
            default:
                System.out.println("Invalid choice.");
                break;
        }
    }
}
```

---

That is the end of this module and hopefully you have a good sense for the langauge and how it is used.

In module 2 we will start building more ambitious apps with Spring Boot.

---

## [back](../README.md)
