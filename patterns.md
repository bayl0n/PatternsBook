# Patterns

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
* ```x += y``` adds the amount y onto x

## The "output" pattern

**Goal:** Show a value to the user

* **Pattern:**
  ```System.out.println("<label>" + <value>);```
* **e.g. show an age:**
  ```System.out.println("age is" + age);```
* **e.g. show a name:**
  ```System.out.println("name is" + name);```

## The "read" pattern

**Goal:** Read a value from the user.

* **Pattern:**
  ```
  System.out.print("<prompt>");
  <type> <variable> = <read operation>;
  ```
  
  *Or if <variable> has already been declared,*
  
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

* **Goal:** Read values until the user enters an "end of input" value.

```
<read pattern>
while (<value != <end value>) {
  <use the value>
  <read the pattern>
}
```

*Observations:*
  * <read pattern> appears twice
  * always test for the "end of input" valye immediately after a <read pattern>.

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
