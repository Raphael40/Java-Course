# Testing the Movie Rating CLI app

### MovieLibrary class

Now we can make our `MovieLibrary` class. As a library we want to be able to add a movie to the library, rate a movie in the library, get a single movie from the library, and get all the movies from the library.

```
package main.java;

public class MovieLibrary {

}
```

We can use a data structure to store our movies, an `ArrayList` would be suitable for storing each instance of `Movie`.

At this point it would be natural to implement an `ArrayList` instance field and a constructor that initialises it when an instance of Movie`Library` is created:

```
package main.java;

import java.util.ArrayList;

public class MovieLibrary {
    private ArrayList<Movie> movies; // Declare a variable of ArrayList type capable of holding Movie objects

    constructor
    public MovieLibrary() {
        this.movies = new ArrayList<Movie>(); Assign it as a new Arraylist object
    }

}
```

However, this would actually be bad practice because `ArrayList` is an implementation of the `List` interface and we would be limiting ourselves to just the `ArrayList` implementation of `List`. Therefore it would be better to do something like this:

```
package main.java;

import java.util.List; // import list
import java.util.ArrayList;

public class MovieLibrary {
    private List<Movie> movies; // Declare a variable of List type capable of holding Movie objects

    constructor
    public MovieLibrary() {
        this.movies = new ArrayList<Movie>(); Assign it as a new Arraylist object
    }

}
```

But technically we are still limiting ourselves an the `ArrayList` so we can impove this further by declaring what type of `List` to implement outsdie of the class and passing it in with dependency injection:

```
package main.java;

import java.util.List;

final private List<Movie> movies;

    public MovieLibrary(List<Movie> movies) { // Pass in a `List` object from outside
        this.movies = movies; // Assign it
    }
```

With this technique our code it much more flexible and if we wanted to change the type of `List` interface from `ArrayList` to `LinkedList` we can do that easily from the main class without having to refactor this class at all. This we become clear when we develop the `Main` class in the next section.

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
    this.movies.add(movie); // adds hotFuzz to the library
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
    for (Movie movie : this.movies) {
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
    for (Movie movie : this.movies) {
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

If this doesn't make sense at the moment it should click when we get to the `Main` class.

Now lets create a method called `removeMovie()` which takes and deletes an instance of the `Movie` class from the ArrayList and returns nothing:

<details>
<summary>removeMovie() method</summary>

```
public void removeMovie(Movie movie) {
    this.movies.remove(movie);
}
```

</details>

<br>

And finally we can make a `getMovies` method to return the entire library. For this we can just return the List.

<details>
<summary>getMovies() method</summary>

```
public List<Movie> getMovies() {
    return this.movies;
}
```

</details>

<br>

Thats all we need for the `MovieLibrary` class, your code should look like this:

<details>
<summary>MoviesLibrary class completed</summary>

```
package main.java;

import java.util.List;

public class MovieLibrary {
    final private List<Movie> movies;

    public MovieLibrary(List<Movie> movies) {
        this.movies = movies;
    }

    public void addMovie(Movie movie) {
        this.movies.add(movie);
    }

    public void rateMovie(Movie movie, double rating) {
        movie.setRating(rating);
    }

    public void removeMovie(Movie movie) {
        this.movies.remove(movie);
    }

    public List<Movie> getMovies() {
        return this.movies;
    }

    public Movie getMovieByTitle(String title) {
        for (Movie movie : this.movies) {
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

### MovieLibraryTest class

Generate your `MovieLibraryTest` class and give it the boilerplate:

```
package main.java;

import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.DisplayName; // import DisplayName

import static org.junit.jupiter.api.Assertions.*;

class MovieLibraryTest {

   @Test
    @DisplayName("addMovie test")
    void addMovie() {
    }

    @Test
    @DisplayName("rateMovie test")
    void rateMovie() {
    }

    @Test
    @DisplayName("removeMovie test")
    void removeMovie() {
    }

    @Test
    @DisplayName("getMovies test")
    void getMovies() {
    }

    @Test
    @DisplayName("getMovieByTitle test")
    void getMovieByTitle() {
    }
}
```

Import BeforeEach at the top. We want to create an instance of `MovieLibrary` and an empty `ArrayList` in our BeforeEach block. We need to pass our `ArrayList` into the `MovieLibrary` instance as an argument:

```
import java.util.ArrayList;

class MovieLibraryTest {

    private MovieLibrary testMovieLibrary; // MovieLibrary instance

    @BeforeEach
    void setUp() {
        ArrayList<Movie> moviesArrayList = new ArrayList<>(); // initialise ArrayList
        testMovieLibrary = new MovieLibrary(moviesArrayList); // initialise MovieLibrary instance with ArrayList
    }

   @Test
    @DisplayName("addMovie test")
    void addMovie() {
    }

    ...
}
```

We can start writing our `addMovie Test` which takes an instance of `Movie`. We have to use the `getMovies()` method to check that it has been added because the add method doesn't return anything and the `movies` ArrayList is private.

Call the `addMovie` method then check that the size of the ArrayList returned by `getMovies()` is 2:

<details>
<summary>addMovie test</summary>

```
@Test
@DisplayName("addMovie test")
void addMovie() {
    Movie testMovie = new Movie("test title", "test director", 5.0, 2021);

    testMovieLibrary.addMovie(testMovie);

    assertEquals(1, testMovieLibrary.getMovies().size());
}
```

</details>

<br>

The `rateMovie test` adds a movie with the `addMovie()` method, then calls the `rateMovie()` method, passing in the `Movie` instance and a new rating. We can then make our assertion using the `getRating()` method of the `Movie` instance:

<details>
<summary>rateMovie test</summary>

```
@Test
@DisplayName("rateMovie test")
void rateMovie() {
    Movie testMovie = new Movie("test title", "test director", 6.0, 2022);

    testMovieLibrary.addMovie(testMovie);

    testMovieLibrary.rateMovie(testMovie, 4.0);

    assertEquals(4.0, testMovie.getRating());
}
```

</details>

<br>

Our `removeMovie test` should have two assertions. We call `addMovie()` to add our instance, we assert that 1 `getMovies()` returns an ArrayList with 1 item, we call the `removeMovie()` method with our instance, and check that the `getMovies()` returns an ArrayList with 0 items:

<details>
<summary>removeMovie test</summary>

```
@Test
@DisplayName("removeMovie test")
void removeMovie() {
    Movie testMovie = new Movie("test title", "test director", 6.0, 2022);

    testMovieLibrary.addMovie(testMovie);

    testMovieLibrary.removeMovie(testMovie);

    assertEquals(0, testMovieLibrary.getMovies().size());
}
```

</details>

<br>

Our `getMovies test` looks pretty much the same as our `addMovie test` but we can add in an extra `Movie` instance to make sure it works for multiple values:

<details>
<summary>getMovies test</summary>

```
@Test
@DisplayName("getMovies test")
void getMovies() {
    Movie testMovie = new Movie("test title", "test director", 6.0, 2022);
    testMovieLibrary.addMovie(testMovie);

    Movie testMovie2 = new Movie("test title 2", "test director 2", 6.0, 2022);
    testMovieLibrary.addMovie(testMovie2);

    assertEquals(2, testMovieLibrary.getMovies().size());
}
```

</details>

<br>

In our `getMovieByTitle test` we will add a movie and then assert that it has been returned when we pass the title into the `getMovieByTitle()` method. We can also confirm that if we pass in an incorrect value it returns `null` using `assertNull()`. We don't need a seperate test for this because `null` is a value not an exception.

<details>
<summary>getMovieByTitle test</summary>

```
@Test
@DisplayName("getMovieByTitle test")
void getMovieByTitle() {
    Movie testMovie = new Movie("test title", "test director", 6.0, 2022);
    testMovieLibrary.addMovie(testMovie);

    assertEquals(testMovie, testMovieLibrary.getMovieByTitle("test title"));
    assertNull(testMovieLibrary.getMovieByTitle("incorrect title"));
}
```

</details>

<br>

We have finished our `MovieLibrary` and `MovieLibraryTest`. In the next section we are going to write our `Main` class.

---

[back](../README.md) <span style="float: right;">[next](02_Main-class.md)</span>
