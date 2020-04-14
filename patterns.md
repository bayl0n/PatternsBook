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

