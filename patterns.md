# Patterns - Nathan Baylon

## The "sum" pattern

**Goal:** Find the sum of a collection of items.

```
<type> sum = 0;
<for each item> {
  sum += <item>;
}
```

* Words enclosed between <angled brackets> are holes that need to be filled.
* <type> is typically double or int
* <for each item> is any loop over a collection of items
* <item> refers to the next item in the loop
* `x += y` adds the amount y onto x

## The "output" pattern

**Goal:** Show a value to the user

* **Pattern:**
  `System.out.println("<label>" + <value>);`
* **e.g. show an age:**
  `System.out.println("age is" + age);`
* **e.g. show a name:**
  `System.out.println("name is" + name);`

## The "read" pattern

**Goal:** Read a value from the user.

* **Pattern:**
  ```
  System.out.print("<prompt>");
  <type> <variable> = <read operation>;
  ```
  
  *Or if `<variable>` has already been declared,*
  
  ```
  System.out.print("<prompt>");
  <variable> = <read operation>;
  ```
* **e.g. read an age:**
  ```java
  System.out.print("Age: ");
  int age = In.nextInt();
  ```

## The "read loop" pattern

**Goal:** Read values until the user enters an "end of input" value.

```
<read pattern>
while (<value != <end value>) {
  <use the value>
  <read the pattern>
}
```

**Observations:**
  * `<read pattern>` appears twice
  * always test for the "end of input" value immediately after a `<read pattern>`.

## The "array loop" pattern

**Goal:** Loop over items in an array.

```
for (int i = 0; i < <array>.length; i++) {
  <use the item array[i]>
}
```

## The "count" pattern

### Without guard

**Goal:** Count the number of items in a collection.

```
int count = 0;
<for each item>
  count++;
```

### With guard

**Goal:** Count the number of items that satisfy a condition.

```
int count = 0;
<for each item>
  if(<guard>)
    count++;
```

## The "max" pattern

**Goal:** Find the maximum value in a collection of items

```
<type> max = <smallest number>;
<for each item> {
  if(<item> > max)
    max = <item>;
}
```
**Key idea:**
If this item is bigger than the max so far, then make it the new max.

# String patterns

## The "string loop" pattern

**Goal:** Loop over the characters in a string.

```
for (int i = 0; i < <str>.length(); i++) {
    <use character str.charAt(i)>
}
```

**Example:** Count the number of l's in the word "hello".

```java
String s = "hello";
int count = 0;
for (int i = 0; i < s.length(); i++) {
    if (s.chatAt(i) == 'l')
        count++;
}
System.out.println("Number of l's = " + count);
```

## The "for-each" loop

Create an array of values

```java
String[] array = {"car", "truck", "bus", "van"};
```

These two code fragments **do the same thing:**

```java
for (int i = 0; i < array.length; i++)
    System.out.println(array[i]);
```

```java
for (String word: array)
    System.out.println(word);
```

**Read:** For each word in array, print that word.

# Functional Patterns

**NOTE:** If it produces a value, make it a function.

## Read functions

* The read pattern returns a value, so it is a function.
    * The name has the form read\<X>

e.g.

```java
int readAge() {
    System.out.print("Age: ");
    return In.nextInt();
}
```

```java
int readName() {
    System.out.print("Name: ");
    return In.nextLine();
}
```

## The "old" read loop pattern

**Specification:** Read ages until the user enters -1.

```java
System.out.print("Age: ");
int age = In.nextInt();

while (age != -1) {
    <use age>
    System.out.print("Age: ");
    age = In.nextInt():
}
```

**Problem:** There is *repeated* code. Instead, put it in a method.

## Merged read loop

```java
double age;
while ((age = readAge()) != -1) {
    <use age>
}

int readAge() {
    System.out.print("Age: ");
    return In.nextInt();
}
```

**Key:** call readAge() inside the while condition.

* Whenever you need a read loop, always use the **merged** read loop
* Example: reading characters:

    ```java
    char c;

    while ((c = readChar()) != '.') {
        <use c>
    }
    ```
* Example: reading strings:

    ```java
    String s;

    while (!(c = readString()).("end")) {
        <use s>
    }
    ```
## The "any" pattern

**Goal:** Determine if any item in a collection passes <test>

```
<for each item>
    if (<item passes test>)
        return true;
return false;
```

**Example:** Test if any number in an array is negative:

```java
boolean anyNegative(int[] array) {
    for (int item : array)
        if (item < 0)
            return true;
    return false;
}
```

**Key idea:** If any item is negative return true.

## The "every" pattern

**Goal:** Determine if all items in a collection pass <test>

```
<for each item>
    if (! <item passes test>)
        return false;
return true;
```

## The "none" pattern

**Goal:** Determine if no items in a collection pass <test>

```
<for each item>
    if (<item passes test>)
        return false;
return true;
```
# Classes

## Constructors

**Goal:** Initialise a new object

```java
public class Account {
  ...
  public Account() {
    name = ...;
    type = ...;
    balance = ...;
  }
}
```

* Constructors are named after the class.
* Constructors have no return type
* Constructors initialise the fields of a newly created object

### Initialise from literals

**Goal:** Initialise a new object with literal values

```java
public class Account {
  ...
  public Account() {
    name = "Default name";
    type = "Savings";
    balance = 0.0;
  }
}
```

* Initialise with default values

### Initialise from user

**Goal:** Initialise a new object with values read from the user.

```java
public class Account {
  ...
  public Account() {
    name = readName();
    type = readType;
    balance = readBalance();
  }

  // As no outside class needs this method, make it private
  private String readName() {
    System.out.print("Account name: ");
    return In.nextLine();
  }
}
```

* Use the read pattern

### Initialise from params

**Goal:** Initialise a new object from parameters.

```java
public class Account {
  ...
  public Account(String name, String type, double balance) {
    this.name = name;
    this.type = type;
    this.balance = balance;
  }
}
```

* Parameters are named after fields.
* Use this.[name] to refer to a field
* This [name] to refer to a parameter

## toString method

**Goal:** Return a string representation of the object.

```java
public class Account {
  ...
  @Override
  public String toString() {
    return "The account has $" + balance;
  }
}
```
* This is a standard method of all classes and we override the default behaviour

## Getter and setter methods

```java
public class Account {
  private String name;
  ...

  // Getter
  public String getName() {
    return name;
  }

  // Setter
  public void setName(String name) {
    this.name = name;
  }
}
```

* A getter returns a field
  * The name is get[Field]
* A setter sets a field
  * The name is set[Field]

# Lists

Lists are data structures that: 

* Store a sequence of elements - like an array
* Allow new elements to be added - unlike an array!
* Allow elements to be removed - unlike an array!

They are implement as classes which you import:

```java
import java.util.*;
```

Two comment implementations: `ArrayList` and `LinkedList`

## Array Lists

An array list uses an array internally, with extra space at the end so that you have more room to add more elements

When you run out of space, a bigger array is created and the elements copied across.

To insert an element, you must shift elements to the right, then insert it.

### When to use an array list

* Array lists provide instant access to any element. They are FAST.
* Adding elements to the end of an array list is reasonably fast.
* Inserting elements near the beginner of a list is slow.

Use an array list if you need random access to elements.

Don't use an array list if you often need to insert elements near the beginning.

## Linked Lists

* Elements are stored in objects that are linked together.
* To insert an element, just change two arrows to point to a new node.

### When to use a linked list

* Linked lists provide SLOW access to random elements.
* Adding elements to the beginning or end is FAST.
* Linked lists require more memory to store the "links".

Use a linked list if you add and remove elements often.

Don't use a linked list if you need fast random access to any element.

Don't use a linked list if you have a large data set and limited memory.

### Generics

* Java 4 and earlier could not restrict elements to a particular type
  * You couldn't restrict to add a particular data type to a list

* Java 5 added "generics", also known as "type parameters":

  ```java
  LinkedList<String> list = new LinkedList<String>();
  list.add("cats");
  list.add("like");
  list.add("milk");
  ```

* We pass <String> as the type parameter to the class LinkedList.
* Now, a linked list of <String> will permit only string elements:

  ```java
  list.add(new Burger());
  ```

This will now throw a compile error.

## Type parameters vs Method parameters

* Method paramaters go after a method and use round brackets:

  ```java
  System.out.println("zoo");
  repeat(5, "* ");
  ```

* Type parameters go after a type and use angled brackets:

  ```java
  LinkedList<Customer> customers;
  ArrayList<Card> cards;
  TreeSet<String> symbols;
  ```

* Type paramaters must be classes. For primitives, use class wrappers:

  ```java
  LinkedList<Integer> ages;
  ArrayList<Double> rainfall;
  ```

## LinkedList<X> and ArrayList<X> methods

| **Method** | **Description** |
| --- | --- |
| add(X element) | Add an element of type X to the end|
| add(int i, X element) | Add an element of type X at position i |
| remove(X element) | Remove this element |
| remove(int i) | Remove the element at position i |
| set(int i, X element) | Replace the element at position i |
| X get(int i) | Return the element at position i |
| int size() | Return the size of the list |
| clear() | Remove all elements |

## Looping over a list

Use a for-each loop

```java
LinkedList<String> words = new LinkedList<String>();
words.add("one");
words.add("two");
words.add("three");

for (String word : list)
  System.out.println(word);
```

## Copying a list

```java
LinkedList<String> original = new LinkedList<String>();
// Add elements to original

LinkedList<String> copy = new LinkedList<String>();
for (String word : original)
  copy.add(word);
```

You now have two lists that contain the same elements.

### What not to do

```java
LinkedList<String> original = new LinkedList<String>();
// Add elements to original

LinkedList<String> copy = original;
```

**This will not work** but instead it will just create two variables that point to the same list.

### Copying a list with addAll

| **Method** | **Description** |
| --- | --- |
| addAll(Collection<X> elements) | Add a collection of elements to this list |

```java
LinkedList<String> original = new LinkedList<String>();
// Add elements to original

LinkedList<String> copy = new LinkedList<String>();
copy.addAll(original);
```

# Find all matches

**Specification:** Find all words in a list that contain "z".

**Solution:** Create a new list and add the matching words.

```java
private LinkedList<String> zWords (LinkedList<String> words) {
  LinkedList<String> matches = new LinkedList<String>();
  for (String word : words)
    if (word.contains("z"))
      matches.add(word);
  return matches;
}
```

# Remove all matches - two solutions

* **Solution #1:** Make a list of z words, then remove them all at once

```java
LinkedList<String> zWords = zWords(list);
list.removeAll(zWords);
```

* **Solution #2:** Use an iterator:

```java
for (Iterator<String> it = list.iterator(); is.hasNext();)
  if (it.next().contains("z"))
    it.remove();
```

The first solution is simpler but slower (loops over the list twice).

The second solution is more complex but more efficient (loops once).

# Remove one match - two solutions

* **Solution #1:** Stop loop after removing to avoid an exception:

```java
for (String word : list)
  if (word.contains("z")) {
    list.remove(word);
    break;
  }
```

* **Solution #2:** Use an iterator:

```java
for (Iterator<String> it = list.iterator(); is.hasNext();)
  if (it.next().contains("z")) {
    it.remove();
    break;
  }
```

**Stop looping** when item is removed.