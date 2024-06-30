# Movie Rating Command Line App

In this section we are going to build an app that will put everything we have learned so far to practice. A completed repo is available, however there is no starter repo since we will be starting from scratch.

First we are going to quickly look at one more class from the `java.util` package called `Scanner`

## Scanner

The idea of the `Scanner` class is to get user input from the command line as long as it is a primitive value (or String).

By importing Scanner at the top of our file:

```
import java.util.Scanner;
```

We are able to use methods of the Scanner class such as `nextBoolean()`, `nextLine()`, and `nextInt()`.

To use it we have to create a new `Scanner` object and then use the scanner methods to save user input to a variable:

```
class Main {
  public static void main(String[] args) {
    Scanner myScanner = new Scanner(System.in);  // Create a Scanner object

    System.out.println("Enter name here:");
    String name = myObj.nextLine();  // nextLine() takes a user input of String
    // At this point I will be prompted to type a value into the CLI. I enter "Jonny"

    System.out.println("Username is: " + name);  // Now we can use the value
  }
}

>> Username is: Jonny
```

**Note** how we declare a new Scanner object with `System.in` to receive a value from the command line. This is just like how we use System.out to print lines (println) to the console.

We are going to use Scanner to enter movies into our movie rating app.

## Movie Rating App

### Create a new project

From the menu select File >> New >> Project and a New Project panel will appear. **Name** your project `movie-rating-app` and save it to a location of your choice. Leave Create Git repository selected and select IntelliJ as your Build system. **Unselect** Add sample code and leave Generate code with onboarding tips unselected.

![new-project-panel](./images/Java-project-setup.png)

This should create a new module containing a .idea directory, a .gitignore file, a project-name.iml file and an src directory.

Inside the src directory we are going to create a `main` package and inside that we are going to create a `java` package. Your path should be movie-rating-app/src/main/java.

### Movie Class

To make this app we are going to create three classes; `Movie`, `MovieLibrary`, and `Main` which will have our `main` method and act as our user interface. Our `Movie` class represents a single movie. Each instance of `Movie` requires a title for identification and a rating. We can also add a Director and release year to be more informative. The Movie class will have methods to return each value and a method to set a new rating.

Right click on `main.java` package and select New > Java Class:

```
package main.java;

public class Movie {

}
```

Next add the instance fields (title(String), director(String), rating(Double), year(int)) and `Movie` constructor method:

<details>
<summary>constructor</summary>

```
package main.java;

public class Movie {
  private String title;
  private String director;
  private double rating;
  private int year;

  public Movie(String title, String director, double rating, int year) {
      this.title = title;
      this.director = director;
      this.rating = rating;
      this.year = year;
  }
}
```

</details>

<br>

Now we can add our methods. Create 4 methods; `getTitle()`, `getDirector()`, `getRating()` and `getYear()`. Each one just needs to return its corresponding value.

<details>
<summary>getMethods()</summary>

```
public String getTitle() {
    return title;
}

public String getDirector() {
    return director;
}

public double getRating() {
    return rating;
}

public int getYear() {
    return year;
}
```

</details>

<br>

And lastly we can add our setRatings() method. It takes a rating and reassigns the instance rating to the value.

<details>
<summary>setMethod()</summary>

```
public void setRating(double rating) {
    this.rating = rating;
}
```

</details>

<br>

Thats all we need for the movie class. Your code should look like this:

<details>
<summary>Movie Class</summary>

```
package main.java;

public class Movie {
private String title;
private String director;
private double rating;
private int year;

    public Movie(String title, String director, double rating, int year) {
        this.title = title;
        this.director = director;
        this.rating = rating;
        this.year = year;
    }

    public String getTitle() {
        return title;
    }

    public String getDirector() {
        return director;
    }

    public double getRating() {
        return rating;
    }

    public int getYear() {
        return year;
    }

    public void setRating(double rating) {
        this.rating = rating;
    }

}

```

</details>

### MovieTest class

### MovieLibrary class

Now we can make our `MovieLibrary` class. As a library we want to be able to add a movie to the library, rate a movie in the library, get a single movie from the library, and get all the movies from the library. We can use an ArrayList to store our movies.

Lets create our `MovieLibrary` class and give it a constructor that initialises the `movies` ArrayList.

<details>
<summary>MovieLibrary class & constructor</summary>

```
package main.java;

import java.util.ArrayList;

public class MovieLibrary {
    private ArrayList<Movie> movies;

    public MovieLibrary() {
        movies = new ArrayList<Movie>();
    }

}
```

</details>

<br>

Next we can make our addMovie method. In this method we want to be able to add an instance of our `Movie` to the `movies` ArrayList. However, the instance of `Movie` is going to be created in the `UI` and then passed into the method:

```
UI class

private static MovieLibrary movieLibrary = new MovieLibrary();

...

main() {}

'''

someMethod() {
  Movie hotFuzz = new Movie("Hot Fuzz", "Edgar Wright", 9.2, 2007)

  movieLibrary.addMovie(hotFuzz) // This method
}
```

Therefore our `addMovie()` method just need to take a movie and add it to the list:

<details>
<summary>addMovie() method</summary>

```
public void addMovie(Movie movie) {
    movies.add(movie); // adds hotFuzz to the library
}
```

</details>

<br>

Now we want a method to set a new rating for the movie. This method will be slightly more complex because we have to find the movie in the ArrayList before we update the rating.

The `rateMovie()` method will take in a movie (String) and rating (Double) and loop through the `movies` ArrayList. If it finds an instance of movie with an equal title, then is will call the `setRating()` method of the movie instance.

<details>
<summary>rateMovie() method</summary>

```
public void rateMovie(String title, double rating) {

    // Find the movie by title and set its rating
    for (Movie movie : movies) {
        if (movie.getTitle().equalsIgnoreCase(title)) { // Ignoring case, are two Strings equal?
            movie.setRating(rating); // If so then we set the new rating
            break; // And break out of the loop
        }
    }

    System.out.println("Movie not found.");
}
```

</details>

<br>

The method above should set a new rating however it doesn't return anything so how can we check that our rating has actually been updated. We can make a `getMovieByTitle(String title)` method.

Once again we want to loop through the `movies` ArrayList, and when we get a match we return the movie:

<details>
<summary>getMovie() method</summary>

```
public void getMovieByTitle(String title, double rating) {

    // Find the movie by title and return it
    for (Movie movie : movies) {
        if (movie.getTitle().equalsIgnoreCase(title)) {
            return movie;
        }
    }

    System.out.println("Movie not found.");
}
```

**Note** return automatically breaks our the of loop so we don't need to use the `break` keyword.

</details>

<br>

Notice that both our `rateMovie()` method and our `getMovieByTitle()` methods use the same loop. In order to avoid repetition we can refactor our `rateMovie()` method to take an instance of `Movie` rather than a title and call the `getMovieByTitle()` method from our main class:

<details>
<summary>rateMovie() method refactor</summary>

```
public void rateMovie(Movie movie, double rating) {
    movie.setRating(rating);
}
```

</details>

<br>

Now lets create a method called `removeMovie()` which takes and deletes an instance of the `Movie` class from the ArrayList and returns nothing:

<details>
<summary>removeMovie() method</summary>

```
public void removeMovie(Movie movie) {
    movies.remove(movie);
}
```

</details>

<br>

And finally we can make a `getMovies` method to return the entire library. For this we can just return the ArrayList.

<details>
<summary>getMovies() method</summary>

```
public ArrayList<Movie> getMovies() {
    return movies;
}
```

</details>

<br>

Thats all we need for the `MovieLibrary` class, your code should look like this:

<details>
<summary>MoviesLibrary class completed</summary>

```
package main.java;

import java.util.ArrayList;

public class MovieLibrary {
    private ArrayList<Movie> movies;

    public MovieLibrary() {
        movies = new ArrayList<Movie>();
    }

    public void addMovie(Movie movie) {
        movies.add(movie);
    }

    public void rateMovie(String title, double rating) {
        Movie movie = getMovieByTitle(title);
        if (movie != null) {
            movie.setRating(rating);
        } else {
            System.out.println("Movie not found.");
        }
    }

    public void removeMovie(Movie movie) {
        movies.remove(movie);
    }

    public ArrayList<Movie> getMovies() {
        return movies;
    }

    public Movie getMovieByTitle(String title) {
        for (Movie movie : movies) {
            if (movie.getTitle().equalsIgnoreCase(title)) {
                return movie;
            }
        }
        return null;
    }
}
```

</details>

<br>

### Testing the MovieLibrary class

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

However, if we use a `try/catch` statement we can try to run a a block of code and if it throws an exception we can catch the error and execute a second block of code instead:

```
try {
  //  Block of code to try
}
catch(Exception e) {
  //  I run if there is an error in the try block
}
```

This will come in handy later on to avoid exiting our program if we make an error.

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
        System.out.println("Invalid input. Please enter the correct data types.");
        movieScanner.nextLine();
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
        System.out.println("Invalid input. Please enter the correct data types.");
        movieScanner.nextLine();
    }
}
```

</details>

<br>

Excellent, now lets move onto the next method:
