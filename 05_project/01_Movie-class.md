# Movie Rating Command Line App

In this section we are going to write the first class of a mini project to which is a `Movie-Rating-App`. A completed repo is available, however there is no starter repo since we will be starting from scratch.

Before we start we are going to quickly look at one more class from the `java.util` package called `Scanner` which is integral to our prject.

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

Next we want to setup our testing suite. Just like we did in the previous section. Install the `JUnit Jupiter` library into your project using this prompt `org.junit.jupiter:junit-jupiter:5.9.1`, thenj add a test directory and make it the testing root. Then add your main.java packages.

It should look like this:

```
-   Movie-Rating-App
    -   .idea
    -   out
    -   src
        -   main
            -   java
                -   Calculator
                -   MyCalculatorTest
    -   test
        -   main
            -   java
    -   .gitignore
    -   movie-rating-app.iml
```

If you are planning to push any of your work to github it's common to add the `.iml` file and `.idea` directory to the `.gitignore` file.

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

And lastly we can add our setRatings() method. It takes a rating and reassigns the instance rating to the value:

<details>
<summary>setRating()</summary>

```
public void setRating(double rating) {
    this.rating = rating;
}
```

</details>

<br>

The `this` keyword ensures it will only update the value of the instance that the method is called on.

We ought to add in some error handling here to ensure that users can only submit a rating greater than 0 and less than 10.

We can use the `throw` keyword to give the user a custom error like this:

`throw new Exception("Desciption");`

Use an if statement to enforce an `IllegalArgumentException` in the setRating() method:

<details>
<summary>setRating()</summary>

```
public void setRating(double rating) {
    if (rating < 0 || rating > 10) {
        throw new IllegalArgumentException("Rating must be between 0 and 10");
    }
    this.rating = rating;
}
```

</details>

<br>

You can view a list of built in Exceptions [here](https://www.tutorialspoint.com/java/java_builtin_exceptions.htm) and there are also some you can import.

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
        if (rating < 0 || rating > 10) {
            throw new IllegalArgumentException("Rating must be between 0 and 10");
        }
        this.rating = rating;
    }

}

```

</details>

### MovieTest class

Now we can test our class. Create a `MovieTest` file:

![MovieTest](images/newTest.png)

```
package main.java;

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

class MovieTest {

    @Test
    void getTitle() {
    }

    @Test
    void getDirector() {
    }

    @Test
    void getRating() {
    }

    @Test
    void getYear() {
    }

    @Test
    void setRating() {
    }
}
```

To avoid repeating code we can instantiate our `Movie` class above the tests. We have to nest it in a `beforeEach` block so that it is re-instantiated before each test to prevent our tests from affecting one another:

```
import org.junit.jupiter.api.BeforeEach;

class MovieTest {

    private Movie testMovie; // instantiate here to give global scope

    @BeforeEach
    void setUp() {
        // Assign here because BeforeEach only works on methods
        testMovie = new Movie("test title", "test director", 5.0, 2021);
    }

    @Test
    void getTitle() {
    }
    ...
}
```

Now we can write our tests. Inside the `getTitle()` test make an assertion that `testMovie.getTitle()` is equal to "test title":

<details>
<summary>getTitle() test</summary>

```
 @Test
@DisplayName("getTitle test")
void getTitle() {
    assertEquals("test title", testMovie.getTitle());
}
```

</details>

<br>

We can take the same approach for the `getDirector()`, `getRating()`, and `getYear()` methods:

<details>
<summary>getDirector(), getRating(), and getYear() tests</summary>

```
@Test
@DisplayName("getDirector test")
void getDirector() {
    assertEquals("test director", testMovie.getDirector());
}

@Test
@DisplayName("getRating test")
void getRating() {
    assertEquals(5.0, testMovie.getRating());
}

@Test
@DisplayName("getYear test")
void getYear() {
    assertEquals(2021, testMovie.getYear());
}
```

</details>

<br>

And for the `setRating()` method we can check that the rating is equal to 5.0 using the `getRating()` method, call the `setRating()` method to update it to `8.0` and then confirm the new rating using the `getRating()` method again:

<details>
<summary>setRating() test</summary>

```
@Test
@DisplayName("setRating test")
void setRating() {
    assertEquals(5.0, testMovie.getRating());
    testMovie.setRating(4.0);
    assertEquals(4.0, testMovie.getRating());
}
```

</details>

<br>

As an extra, it is good practice to test that our error messages are working.

We can use the `assertThrows` assertion to accomplish this:

```
assertThrows(ExceptionType.class, Lambda method)
```

When we throw an exception, there isn't a value returned, which is why the assertion can miss it. If we use a lambda expression with assertThrows, it ensures that the exception is thrown within the controlled execution context of the lambda. This allows assertThrows to accurately detect that the exception.

Our test looks like this:

```
@Test
@DisplayName("setRating test exception")
void setRatingException() {
    assertThrows(IllegalArgumentException.class, () -> testMovie.setRating(-1.0));
}
```

With that our `Movie` and `MovieTest` are complete.

In the next section we're going to write our `MovieLihbrary` app.

---

[back](../README.md) <span style="float: right;">[next](02_MovieLibrary-class.md)</span>
