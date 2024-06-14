# testing intro with JUnit

In this section we're going to look at unit testing with JUnit, a testing framework for Java.

## What is a test?

A test is a program designed to verify that another program behaves as expected. There are three types of tests, unit, integration and end to end. A unit test is designed to verify smaller units of code such as methods. We will visit the other two later. If the code works as expected the test should pass, otherwise the test should fail. This is helpful for identifying bugs in your code.

Now we are going to manually write a simple test for this calculator program:

```
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}

```

First we make a new CalculatorTest class:

```
public class CalculatorTest {

    public static void main(String[] args) {

    }
}
```

Then we make a new instance of Calculator within our CalculatorTest

```
public class CalculatorTest {

    public static void main(String[] args) {
        Calculator calculator = new Calculator();

    }
}
```

Now we're going to test the add method by calling it from our CalculatorTest class. We can use an if statement to check whether the `add()` method returns the expected value:

```
public class CalculatorTest {

    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        // Test add method
        if (calculator.add(2, 3) != 5) {
            System.out.println("Test failed: add(2, 3) should be 5");
        } else {
            System.out.println("Test passed: add(2, 3)");
        }
    }
}
```

In this case we are checking if `add(2, 3)` returns `5`. If it is not true that it equals 5 we print `Test failed: add(2, 3) should be 5` else we print `Test passed: add(2, 3)` if it is equal to 5.

Lets do it again for subtract:

```
public class CalculatorTest {

    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        // Test add method
        if (calculator.add(2, 3) != 5) {
            System.out.println("Test failed: add(2, 3) should be 5");
        } else {
            System.out.println("Test passed: add(2, 3)");
        }

        // Test subtract method
        if (calculator.add(5, 3) != 2) {
            System.out.println("Test failed: subtract(5, 3) should be 2");
        } else {
            System.out.println("Test passed: subtract(5, 3)");
        }
    }
}

>> Test passed: add(2, 3)
>> Test passed: subtract(5, 3)
```

We have now made two unit tests. If we run the CalculatorTest we get two lines printed to the console confirming that the tests have passed.

Now if we break the code in the Calculator class:

```
public class Calculator {
    public int add(int a, int b) {
        // We can change it from plus to *
        return a * b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}

```

If we run the CalculatorTest now we get:

```
>> Test failed: add(2, 3) should be 5
>> Test passed: subtract(5, 3)
```

**Note:** If Calculator and CalculatorTest are in the same package (e.g., the default package or another common package), you do not need an import statement.

Otherwise, you would have to import the the Calculator at the top of the CalculatorTest script with an import statement:

```
import root.path.Calculator;

pubic class CalculatorTest {
  ...
}
```

## Testing Frameworks

### Why use a framework

If we can manually write tests like above then why would we need a testing framework? There are many reasons including:

1. Extended syntax to account for more complex code
2. Capability to run multiple tests in one command
3. Detailed test reports and logs to provide insights
4. Test coverage info (how much of your code is covered by tests)
5. Testing frameworks often integrate with various development tools like web development frameworks

### Passing tests

Before we write our own tests it can be good to get comfortable writing code to pass tests. This will be helpful getting familiar with fixing a broken test through error messages. It is also a common practice in test driven development to write the test before you write the code.

Switch onto `passing tests` branch
