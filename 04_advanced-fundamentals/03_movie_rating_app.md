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

</details>
**Note** return automatically breaks our the of loop so we don't need to use the `break` keyword.

<br>

Notice that both our `rateMovie()` method and our `getMovie()` method use the same loop. In order to avoid repetition we can refactor our `rateMovie()` method to call the `getMovieByTitle()` method which already loops through the `movies` ArrayLIst and returns a movie by its title:

<details>
<summary>rateMovie() method refactor</summary>

```
public void rateMovie(String title, double rating) {
    Movie movie = getMovieByTitle(title); // Find the movie

    if (movie != null) {
        movie.setRating(rating); // call setRating()
    } else {
        System.out.println("Movie not found.");
    }
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
