# Data Structures - HashMap

In this section:

-   HashMaps
-   Iterating through HashMaps
-   Lambdas and HashMaps

## HashMap

A HashMap is a data structure that stores data in key-value pairs. Each key is unique and maps to a specific value.

It can be visalised like this:

```
hashMap1 {
  key1: value,
  key2: value,
  key3: value
}
```

A hashMap is used as an alternative to an Array under specific cases when you don't need your data to be ordered and more generally when it makes the code more readable and functional.

You can initialise a new HashMap like this:

```
// import the HashMap class at the top of your file
import java.util.HashMap;

Map<KeyDataType, ValueDataType> hashmapName = new HashMap<>();
```

For example:

```
import java.util.Map;
import java.util.HashMap;

public class Hashing {
  public static void main(String[] args) {

    // Create a HashMap
    HashMap<String, Integer> movieRatings = new HashMap<>();

  }
}

```

We can then insert key: value pairs using `put()`:

```
import java.util.HashMap;

public class Hashing {
  public static void main(String[] args) {

    // Create a HashMap
    Map<String, Integer> movieRatings = new HashMap<>();

    // Add keys and values (title, rating)
    movieRatings.put("Avengers Endgame", 8);
    movieRatings.put("Iron Man", 9);
    movieRatings.put("Captain Marvel", 4);

  }
}

```

We can use `get()` to get a value by key and `remove()` to remove to remove both key and value by key:

```
import java.util.HashMap;

public class Hashing {
  public static void main(String[] args) {

    // Create a HashMap
    Map<String, Integer> movieRatings = new HashMap<>();

    // Add keys and values (title, rating)
    movieRatings.put("Avengers Endgame", 8);
    movieRatings.put("Iron Man", 9);
    movieRatings.put("Captain Marvel", 4);

    System.out.println(movieRatings.get("Iron Man"));
    // >> 9

    movieRatings.remove("Iron Man");

    System.out.println(movieRatings.get("Iron Man"));
    // >> null
  }
}

```

we can use `replace()` to change the value of a key:

```
import java.util.HashMap;

public class Hashing {
  public static void main(String[] args) {

    // Create a HashMap
    Map<String, Integer> movieRatings = new HashMap<>();

    // Add keys and values (title, rating)
    movieRatings.put("Avengers Endgame", 8);
    movieRatings.put("Iron Man", 9);
    movieRatings.put("Captain Marvel", 4);

    ...

    movieRatings.replace("Captian Marvel", 2); // replace 4 with 2

    System.out.println(movieRatings.get("Captain Marvel"));
    // >> 2
  }
}

```

Other useful HashMap methods inlude:

`keySet()` - get all keys from a HashMap as a `set`
`values()` - get all values from a HashMap as a `set`
`clear` - empty the HashMap
`containsKey()` - checks if a key is in a HashMap (returns a boolean)
`containsValue()` - checks if a value is in a HashMap (returns a boolean)
`size()` - get the number of keys in a HashMap

### Iterating a HashMap

We can use `KeySet()` with a `For Each` loop to cycle through the keys and get thir values:

```
import java.util.HashMap;

class PremierLeague {
    public static void main(String[] args) {

        // create a HashMap with a rank and a team as Integer and String
        HashMap<Integer, String> championsLeague = new HashMap<>();
        championsLeague.put(1, "Man City");
        championsLeague.put(2, "Arsenal");
        championsLeague.put(3, "Liverpool");

        // iterate through keys with keySet()
        for (Integer rank : championsLeague.keySet()) {
          System.out.println(rank + ": " + championsLeague.get(rank));
        }

    }
}

>> 1: Man City
>> 2: Arsenal
>> 3: Liverpool
```

Another option is to use the `java.util.Map.Entry` package for more advanced iteration syntax and improved performance:

```
import java.util.HashMap;
import java.util.Map.Entry; // import at the top

class PremierLeague {
    public static void main(String[] args) {

        // create a HashMap
        HashMap<Integer, String> championsLeague = new HashMap<>();
        championsLeague.put(1, "Man City");
        championsLeague.put(2, "Arsenal");
        championsLeague.put(3, "Liverpool");

       ...


        // we make a new Entry object which combines the key and value into one entry
        // then iterate over the entrySet()
        for (Entry<Integer, String> teamEntry : championsLeague.entrySet()) {
          // we can then use entry.getKey() and entry.getValue() instead of HashMap.get(key)
          System.out.println("key: " + teamEntry.getKey() + " value: " + teamEntry.getValue());
        }

    }
}
```

### Hashmap <String Object>

We can use <String Object> to create a HashMap with values of different types. Below we have a String value, Integer value and Array value:

```
import java.util.HashMap;

public class HashMapExtra {
    public static void main(String[] args) {
    HashMap<String, Object> objectMap = new HashMap<>();

    objectMap.put("key1", "value1"); // String value
    objectMap.put("key2", 123); // Integer value

    String[] values = {"Integer", "String", "Boolean"};
    objectMap.put("key3", values); // You can also have an Array value

    // To retrieve this Array we can use get to save the Array to a variable
    String[] retrievedArray = (String[]) objectMap.get("key3");

    System.out.println(retrievedArray[0]);
    // >> Integer

    // declare a new HashMap names placesMap and make it a value for objectMap
    HashMap<String, String> placesMap = new HashMap<>();
    placesMap.put("city", "New York");
    placesMap.put("zipcode", "10001");

    objectMap.put("key4", placesMap);

    // We can retrieve the inner HashMap from the outer HashMap in a similar way:
    HashMap<String, String> retrievedMap = (HashMap<String, String>) objectMap.get("key4");

    System.out.println(retrievedMap.get("city"));
    // >> New York

    }

}

```

We can even have a HashMap value of a HashMap:

```
import java.util.HashMap;

public class HashMapExtra {
    public static void main(String[] args) {
    HashMap<String, Object> objectMap = new HashMap<>();

    ...

    // declare a new HashMap names placesMap and make it a value for objectMap
    HashMap<String, String> placesMap = new HashMap<>();
    placesMap.put("city", "New York");
    placesMap.put("zipcode", "10001");

    objectMap.put("key4", placesMap);

    // We can retrieve the inner HashMap from the outer HashMap in a similar way:
    HashMap<String, String> retrievedMap = (HashMap<String, String>) objectMap.get("key4");

    System.out.println(retrievedMap.get("city"));
    // >> New York

    }

}

```

### HashMap Runnable/Lambda

We can use <String Runnable> to store a lambda in our HashMap.

A Lambda is an anonymous method that can be passed as a parameter or stored in a varaiable.

```
Runnable runnable = () -> System.out.println("Hello, Lambda!");

// Use the run() method to call it
System.out.println(runnable.run());
>> Hello, Lambda!
```

Another good example of lambda use is the built in method called `forEach()` which takes a lambda and applies it for each element of an ArrayList:

```
ArrayList<String> names = new ArrayList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println("Hello, " + name));

>> Hello, Alice
>> Hello, Bob
>> Hello, Charlie
```

And of course we can use lambdas in HashMaps:

```
import java.util.HashMap;

public class Lambda {
    public static void main(String[] args) {
        HashMap<String, Runnable> actions = new HashMap<>();

        actions.put("sayHello", () -> System.out.println("Hello, World!"));
        actions.put("sayGoodbye", () -> System.out.println("Goodbye, World!"));

        actions.get("sayHello").run();
        actions.get("sayGoodbye").run();

//      >> Hello, World!
//      >> Goodbye, World!
    }
}
```

This is all we're going to cover for HashMaps, in the next section we'll examine class methods.

[back](../README.md) <span style="float: right;">[next](03_class-methods.md)</span>
