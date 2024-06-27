# HashMap

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

## HashMap

You can initialise a new HashMap like this:

```
// import the HashMap class at the top of your file
import java.util.HashMap;

Map<KeyDataType, ValueDataType> hashmapName = new HashMap<>();
```

For example:

```
import java.util.HashMap;

public class Hashing {
  public static void main(String[] args) {

    // Create a HashMap
    Map<String, Integer> movieRatings = new HashMap<>();

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
    // >> Iron Man

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

    movieRatings.replace("Captian Marvel", 2) // replace 4 with 2

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

class Main {
    public static void main(String[] args) {

        // create a HashMap with a rank and a team as Integer and String
        HashMap<Integer, String> championsLeague = new HashMap<>();
        championsLeague.put(1, "Man City");
        championsLeague.put(2, "Arsenal");
        championsLeague.put(3, "Liverpool");

        // iterate through keys with keySet()
        for (Integer rank : championsLeague.keySet()) {
          System.out.print(rank + ": " + championsLeague.get(rank));
        }

    }
}

>> 1: Man City
>> 2: Arsenal
>> 3: Liverpool
```

Another option is to use the `java.util.Map.Entry` package for more advanced iteration syntax and improved performance:

```
import java.util.Map.Entry; // import at the top
import java.util.HashMap;

class Main {
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

## Set?
