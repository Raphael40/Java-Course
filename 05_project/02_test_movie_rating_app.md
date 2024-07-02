# Testing the Movie Rating commandline app

### MovieTest class

Now we can test our class. This time when we create our `MovieTest` class from the actions dropdown we can tick the items under `Generate test methods for for`:

![MovieTest](images/newTest.png)

This will give us some starter code:

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

### MovieLibraryTest class

Generate your `MovieLibraryTest` class, it should look likt this:

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

Import BeforeEach and DisplayName at the top. We want to create an instance of `MovieLibrary` and `Movie` in our BeforeEach block:

```
class MovieLibraryTest {

    private MovieLibrary testMovieLibrary;
    private Movie testMovie;

    @BeforeEach
    void setUp() {
        testMovieLibrary = new MovieLibrary();
        testMovie = new Movie("test title", "test director", 5.0, 2021);
    }

   @Test
    @DisplayName("addMovie test")
    void addMovie() {
    }

    ...
}
```

We can start writing our `addMovie Test` which takes an instance of `Movie`. We have to use the `getMovies()` method to check that it has been added because the add method doesn't return anything and the `movies` ArrayList is private.

Call the `addMovie` method then check that the size of the ArrayList returned by `getMovies()` is 1:

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
@DisplayName("rateMovie test")
void rateMovie() {
    testMovieLibrary.addMovie(testMovie);

    testMovieLibrary.rateMovie(testMovie, 4.0);

    assertEquals(4.0, testMovie.getRating());
}
```

</details>

<br>

Our `getMovies test` looks pretty much the same as our `addMovie test` but we can add in an extra `Movie` instance to make sure it works for multiple values:

<details>
<summary>getMovies test</summary>

```
@Test
@DisplayName("rateMovie test")
void rateMovie() {
    testMovieLibrary.addMovie(testMovie);

    testMovieLibrary.rateMovie(testMovie, 4.0);

    assertEquals(4.0, testMovie.getRating());
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
    testMovieLibrary.addMovie(testMovie);

    assertEquals(testMovie, testMovieLibrary.getMovieByTitle("test title"));
    assertNull(testMovieLibrary.getMovieByTitle("incorrect title"));
}
```

</details>

<br>

### Main class Test

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
