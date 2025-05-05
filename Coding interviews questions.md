## Coding Questions for Interviews

### 1. First Repeating Character from a String
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "geeksforgeeks"` | `"e"`  | 'e' repeats at third position.  |
| `s = "hellogeeks"` | `"l"`  | 'l' repeats at fourth position.  |
| `s = "abc"` | `"-1"`  | No repeated character found.         |

#### Solution:
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        String s = "geeksforgeeks";
        List<Character> seenChars = new ArrayList<>();

        for (int i = 0; i < s.length(); i++) { // Add-on: for (Character c: s.toCharArray()) can be used
            if (!seenChars.contains(s.charAt(i))) {
                seenChars.add(s.charAt(i));
            } else {
                System.out.println("First repeating character: " + s.charAt(i));
                return;
            }
        }
        System.out.println("-1"); // No repeating character found
    }
}
```
**Alternate:**
```java
public static Optional<Character> findFirstRepeatedCharacter(String input) {
    Set<Character> seen = new HashSet<>();
    return input.chars().mapToObj(c -> (char) c).filter(c -> !seen.add(c)).findFirst();
}
```
---
### 2. Find the longest uniform substring in given String.
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "aaabbbbccda"` | `"[3,4]"`  | "bbbb" the longest uniform substring (which starts at index 3 and is 4 characters long).  |
| `s = "aabbbc"` | `"[2, 3]"`  | "bbb" is the longest uniform substring.  |
| `s = "aabbbaaaa"` | `"[5, 4]"`  | "aaaa" is the longest uniform substring.         |

#### Solution:
```
public class Main {
    public static void main(String[] args) {
      String s = "aaabbbbccda";
      int left = 0, count=1, maxLen = 0, maxStart = 0;
      
      for (int right=1;right<s.length(); right++) {
        if(s.charAt(right-1)==s.charAt(right)) { // 
          count++; //2
        } else { //a==b
          if(count>maxLen) {
              maxLen = count;
              maxStart = left;
              count=1;
              left = right;
          }
        }       
      }
      if (count> maxLen) {
        maxLen = count;
        maxStart = left;
      }      
      System.out.println(maxStart + "::" + maxLen);
  }
}
```
---
### 3. Find Longest Substring Without Repeating Characters  
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "geeksforgeeks"` | `"7"`  | The longest substrings without repeating characters are “eksforg” and “ksforge”, with lengths of 7.  |
| `s = "aaa"` | `"1"`  | The longest substring without repeating characters is “a”.  |
| `s = "abcdefabcbb"` | `"6"`  | The longest substring without repeating characters is “abcdef”.         |

#### Solution:
```java
public int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int maxLength = 0, left = 0;

    for (int right = 0; right < s.length(); right++) {
        while (set.contains(s.charAt(right))) {
            set.remove(s.charAt(left));
            left++;
        }
        set.add(s.charAt(right));
        maxLength = Math.max(maxLength, right - left + 1);
    }
    return maxLength;
}
```
#### Alternate Solution:
```
public void lengthOfLongestSubstring {
    String s = "aaa";
    String str = "";
    int left = 0, count=0, maxLen = 0;
    String maxStr = "";
      
    for (int right=0; right<s.length(); right++) {
        if(str.indexOf(s.charAt(right))==-1) { // 
          str+=s.charAt(right);
        } else {
          if (str.length() > maxStr.length()) {
            maxStr = str.toString();
          }
          str = "";
        }
    }
    System.out.println(maxStr +"::"+maxStr.length());
    }
}
```
---

#### 4. Find Output
```
String str1 = new String("Java");
String str2 = new String("Java");
System.out.println(str1 == str2);      
System.out.println(str1.equals(str2));

String str3 = "Java";
String str4 = "Java";
System.out.println(str3 == str2);      
System.out.println(str3.equals(str2));
System.out.println(str3 == str4);      
System.out.println(str3.equals(str4));
String str5 = str3.intern();

System.out.println(str3 == str5);
System.out.println(str3.equals(str5));
```
```
false
true
false
true
true
true
true
true
```

**Explanation:**

1.  **`String str1 = new String("Java");` and `String str2 = new String("Java");`**
    * `str1` and `str2` are created using the `new` keyword. This explicitly creates two separate `String` objects in the heap memory.
    * `System.out.println(str1 == str2);` compares the references of `str1` and `str2`. Since they are different objects in memory, the result is `false`.
    * `System.out.println(str1.equals(str2));` compares the content of the `String` objects. Both `str1` and `str2` contain the same sequence of characters "Java", so the result is `true`.

2.  **`String str3 = "Java";` and `String str4 = "Java";`**
    * `str3` and `str4` are created using String literals. Java maintains a "String constant pool" in the method area (part of the heap in newer JVMs). When a String literal is encountered, the JVM first checks if a String with the same value already exists in the pool.
    * For `str3`, "Java" is added to the pool (if it's not already there).
    * For `str4`, the JVM finds that "Java" already exists in the pool, so `str4` is assigned a reference to the same String object in the pool as `str3`.
    * `System.out.println(str3 == str2);` compares the reference of `str3` (which points to the string pool) with the reference of `str2` (which points to an object in the heap). They are different, so the result is `false`.
    * `System.out.println(str3.equals(str2));` compares the content of `str3` and `str2`, which is the same ("Java"), so the result is `true`.
    * `System.out.println(str3 == str4);` compares the references of `str3` and `str4`. Since they both point to the same String object in the pool, the result is `true`.
    * `System.out.println(str3.equals(str4));` compares the content of `str3` and `str4`, which is the same, so the result is `true`.

3.  **`String str5 = str3.intern();`**
    * The `intern()` method is called on `str3`. This method checks if a String equal to `str3` (i.e., "Java") exists in the String constant pool.
    * Since `str3` itself is a literal "Java", it already resides in the pool. The `intern()` method returns a reference to the String in the pool. In this case, it will return the same reference that `str3` already holds.
    * `System.out.println(str3 == str5);` compares the references of `str3` and `str5`. Since `intern()` returns the existing reference from the pool, `str3` and `str5` point to the same object, and the result is `true`.
    * `System.out.println(str3.equals(str5));` compares the content of `str3` and `str5`, which is the same, so the result is `true`.
  
---
### 5. Find the character count from a string in java using getOrDefault().
```
import java.util.HashMap;
import java.util.Map;

public class CharacterCount {
    public static void main(String[] args) {
        String str = "This is java interveiw";
        Map<Character, Integer> charCountMap = getCharacterCount(str);

        for (Map.Entry<Character, Integer> entry : charCountMap.entrySet()) {
            System.out.println("Character: '" + entry.getKey() + "', Count: " + entry.getValue());
        }
    }

    public static Map<Character, Integer> getCharacterCount(String str) {
        Map<Character, Integer> countMap = new HashMap<>();

        for (int i = 0; i < str.length(); i++) {
            char currentChar = str.charAt(i);
            // Use getOrDefault to get the current count or 0 if the character is not yet in the map
            int currentCount = countMap.getOrDefault(currentChar, 0);
            countMap.put(currentChar, currentCount + 1);
        }
        return countMap;
    }
}
```
**Output of the Code:**
```
Character: 'T', Count: 1
Character: 'h', Count: 1
Character: 'i', Count: 3
Character: 's', Count: 2
Character: ' ', Count: 3
Character: 'j', Count: 1
Character: 'a', Count: 2
Character: 'v', Count: 1
Character: 'e', Count: 1
Character: 'r', Count: 1
Character: 'n', Count: 1
Character: 't', Count: 1
Character: 'w', Count: 1
```

---
### 6. Valid Paranthesis
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "()"` | `"true"`  | Follow the same pattern  |
| `s = s = "()[]{}"` | `"true"`  | Doesn't follow the pattern |
| `s = "(]"` | `"false"`  |   Doesn't follow the pattern       |
| `s = "([])"` | `"true"`  | Follow the pattern         |

### Solution:
```
TODO:

```

---
### 7. Reverse words in a String.
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "the sky is blue"` | `"blue is sky the"`  |   |
| `s = "  hello world  "` | `"world hello"`  |  Your reversed string should not contain leading or trailing spaces.  |
| `s = "a good   example"` | `"example good a"`  | You need to reduce multiple spaces between two words to a single space in the reversed string.  |

#### Solution:
```
public static void reverseWordsInString(){
    String s = "the sky is blue";

    List<String> list = Arrays.asList(s.split("\s+")); // "\s+" is mandatory to multiple remove space in between the words 
    Collections.reverse(list);
    System.out.println("Original: \"" + String.join(" ", list) + "\"");
}
```
_**List.of():**_ This method (introduced in Java 9) creates an immutable list. This is a space-efficient way to create a small list when you know you won't need to change its contents.

---
### 8. Find output
```
final int i;
i = 20;
int j = i+20;
i = j+30;
System.out.println(i + " " + j);
```
**Output:**
```
java: variable i might already have been assigned at `i = j+30;`
```
**_Note:_**
The problem is that `i` is declared as `final`. In Java, a `final` variable can only be assigned a value once.  You can initialize it at the time of declaration or assign the value later, but only once.  The code attempts to assign a value to `i` twice: first with `i = 20;` and then with `i = j + 30;`. The second assignment is illegal.

**How to fix it and find output:**
```
final int i;  // Declare i as final
i = 20;       // Initialize i
int j = i + 20; // Declare and initialize j
// i = j + 30;   // Error: Cannot assign a value to a final variable
System.out.println(i + " " + j); // corrected output
```
**Output:**
```
20 40
```

---
### 9. Find the output:
```
class Parent {
    public void print() throws FileNotFoundException {
	System.out.println("Parent");
    }
}
    
public class Child extends Parent{
    @Override
    public void print() throws  IOException{
    	System.out.println("Child");
    }
    
    public static void main(String[] args) throws IOException {
    	Parent p = new Child();
    	p.print();
    }
}
```
**Output:**
```
Child
```

---
### 10. Count repeating numbers from an array in map in java.
```java
mport java.util.*;

public class Main {
    public static void main(String[] args) {
        int[] arr = {1,2,3,4,2,2,3};
        int count=0;
        Map<Integer, Integer> h = new HashMap<>();
        
        for (Integer n: arr) {
          if (h.get(n)==null) {
            h.put(n, 1);
          } else {
            int x = h.get(n);
            h.put(n, x+1);
          }
        }  
      System.out.println(h);
}
  ``` 
**Output:**
```
{1=1, 2=3, 3=2, 4=1}
```

---
### 11. Write a program to find a string or a number is palindrome or not?.
**String palindrome:**
```
class Main {
  public static void main(String[] args) {

    String str = "Radar", reverseStr = "";
    
    int strLength = str.length();

    for (int i = (strLength - 1); i >=0; --i) {
      reverseStr = reverseStr + str.charAt(i);
    }

    if (str.toLowerCase().equals(reverseStr.toLowerCase())) {
      System.out.println(str + " is a Palindrome String.");
    }
    else {
      System.out.println(str + " is not a Palindrome String.");
    }
  }
}
```
**Palindrome of a Number:**
```
class Main {
  public static void main(String[] args) {
    
    int num = 3553, reversedNum = 0, remainder;
    
    // store the number to originalNum
    int originalNum = num;
    
    // get the reverse of originalNum
    // store it in variable
    while (num != 0) {
      remainder = num % 10;
      reversedNum = reversedNum * 10 + remainder;
      num /= 10;
    }
    
    // check if reversedNum and originalNum are equal
    if (originalNum == reversedNum) {
      System.out.println(originalNum + " is Palindrome.");
    }
    else {
      System.out.println(originalNum + " is not Palindrome.");
    }
  }
}
```

---
### 12. Shift an Array by 3 to the Right
```java
public static void rotateRight(int[] arr, int k) {
    Collections.rotate(Arrays.asList(arr), k);
}
```
---
### 13. Identify lowest positive integer which is not present in the array
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = [-8,1,-3,3,2,-10]` | `"4"`  | 4 is the lowest which is not present in given array  |

#### Solution 1:
```java
import java.util.HashSet;

public class LowestMissingPositive {
    public static int findLowestMissingPositive(int[] nums) {
        // Step 1: Create a set to store positive integers
        HashSet<Integer> positiveSet = new HashSet<>();
        
        // Step 2: Add positive integers to the set
        for (int num : nums) {
            if (num > 0) {
                positiveSet.add(num);
            }
        }
        
        // Step 3: Check for the lowest missing positive integer
        int lowestMissing = 1; // Start checking from 1
        while (positiveSet.contains(lowestMissing)) {
            lowestMissing++; // Increment until we find a missing integer
        }
        
        return lowestMissing;
    }

    public static void main(String[] args) {
        int[] array = {-8, 1, -3, 3, 2, -10};
        int result = findLowestMissingPositive(array);
        System.out.println(result); // Output: 4
    }
}
```
#### Solution 2:
```java
public class LowestMissingPositive {
    public static int findLowestMissingPositive(int[] nums) {
        int n = nums.length;

        // Step 1: Move each positive integer to its corresponding index
        for (int i = 0; i < n; i++) {
            while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
                // Swap nums[i] with nums[nums[i] - 1]
                int temp = nums[i];
                nums[i] = nums[temp - 1];
                nums[temp - 1] = temp;
            }
        }

        // Step 2: Find the first index where the value is not correct
        for (int i = 0; i < n; i++) {
            if (nums[i] != i + 1) {
                return i + 1; // The first missing positive integer
            }
        }

        // If all positions are correct, the missing integer is n + 1
        return n + 1;
    }

    public static void main(String[] args) {
        int[] array = {-8, 1, -3, 3, 2, -10};
        int result = findLowestMissingPositive(array);
        System.out.println(result); // Output: 4
    }
}
```
**Explanation of the Code:**
- **Rearranging the Array:** The first loop rearranges the array such that each positive integer `x` is placed at index `x - 1`. For example, if 1 is in the array, it will be placed at index `0`, if `2` is in the array, it will be placed at index `1`, and so on.
- **Finding the Missing Integer:** The second loop checks each index. If the value at index `i` is not `i + 1`, then `i + 1` is the lowest missing positive integer.
- **Return Value:** If all integers from `1` to `n` are present, the next missing positive integer will be `n + 1`.

---
### 14. Write a logic to implement below use-case:
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "Ravi Kumar"` | `"ivaR ramuK"`  | reverse words with the same order  |
| `s = "Ravi Kumar Sharma"` | `"ivaR ramuK amrahS"`  | reverse words with the same order  |

#### Solution 1:
```java
public class Main {
    public static void main(String[] args) {
      String s1= "Ravi Kumar";
      String[] str = s1.split(" ");
      List<String> list = new ArrayList<>();
      
      for (int i=0; i<str.length; i++) {
        String s = reverStr(str[i]);
        list.add(s);
      }
      
      System.out.println(Arrays.toString(str)); //["Ravi, Kumar]
      System.out.println(list.toString()); 
      
      System.out.println(String.join(" ", list)); // ivaR ramuK amrahS
  }
  
  public static String reverStr(String st) {
    int len = st.length()-1;
    String ss = "";
    for (int j=len; j>=0; j--) {
      ss+=st.charAt(j);
    }
    return ss;
  }
}
```

#### Solution 2:
```java
public class Main {
    public static void main(String[] args) {
      String s1= "Ravi Kumar Sharma";
      String reverseStr = "";
      List<String> list = new ArrayList<>();
      int len = s1.length()-1;
      
      for (int i = len; i>=0; i--) {
        reverseStr+=s1.charAt(i);
      }
      
      String[] reverseStrArray = reverseStr.split(" ");
      
      for (int j=reverseStrArray.length-1; j>=0; j--) {
        list.add(reverseStrArray[j]);
      }
      
      System.out.println(reverseStr.join(" ", list)); // ivaR ramuK amrahS
  }
  
}
```

---
## 15. Find output
```java
class A {
	public final void testMethod() {
		System.out.println("invoke A");
	}
}
class B extends A {
	public final void testMethod() {
		System.out.println("invoke B");
	}
}
class C {
	public static void main(String[] args) {
		A a = new B();
		a.testMethod();
	}
}
```
In the provided Java code, we have a class `A` with a final method `testMethod()`, and a class `B` that extends `A` and also defines a final method with the same name. Here’s the breakdown of the code:

1. **Class A**: Contains a final method `testMethod()` that prints "invoke A".
2. **Class B**: Extends `A` and attempts to override the `testMethod()` with its own implementation that prints "invoke B". However, since the method in class `A` is declared as `final`, it cannot be overridden in class `B`.
3. **Class C**: In the `main` method, an instance of `B` is created but referenced by a variable of type `A`. When `a.testMethod()` is called, it will invoke the method defined in class `A` because `testMethod()` in `A` is final and cannot be overridden.

#### Output
When you run the `main` method in class `C`, the output will be:
```
invoke A
```
#### Explanation
- The `final` keyword in Java indicates that a method cannot be overridden by subclasses. Therefore, even though `B` has a method with the same name, it does not override the method from `A`. The method from `A` is the one that gets called, resulting in "invoke A" being printed.

---
### 16. Find the output:
```java
public class Test implements Runnable
{
    public void run()
    {
        System.out.printf("Thread's running ");
    }
    try
    {
        public Test()
        {
            Thread.sleep(5000);
        }    
    } 
    catch (InterruptedException e) 
    {
        e.printStackTrace();
    }
    public static void main(String[] args)
    {
        Test obj = new Test();
        Thread thread = new Thread(obj);
        thread.start();
        System.out.printf("GFG ");
    }
}
```
#### Output
```
Compilation error 
```
**Explanation:** 
- A constructor cannot be enclosed inside a try/catch block.

---
### 17. Find the output:
```java
public class TestClass {
    public static void main(String[] args) {
        someMethod(null);
    }

    public static void someMethod(Object o) {
       System.out.println("Object method Invoked");
    }

    public static void someMethod(String s) {
        System.out.println("String method Invoked");
    }
}
```
#### Output
The output of this code is “String method Invoked”. We know that null is a value that can be assigned to any kind of object reference type in Java. It is not an object in Java. Secondly, the Java compiler chooses the method with the most specific parameters in method overloading. this means that since the String class is more specific, the method with String input parameter is called.

---
### 18. Find the output on inheritance + overriding:
#### Example 1: Basic Overriding
```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound();
    }
}
```

**Expected Output:**
```
Dog barks
```

#### Example 2: Static Method Hiding

```java
class A {
    static void display() {
        System.out.println("Static A");
    }
}

class B extends A {
    static void display() {
        System.out.println("Static B");
    }
}

public class Test {
    public static void main(String[] args) {
        A obj = new B();
        obj.display();
    }
}
```

**Expected Output:**
```
Static A
```

- Static methods are **not overridden** but **hidden**.

#### Example 3: Final Method

```java
class X {
    final void show() {
        System.out.println("X show");
    }
}

class Y extends X {
    // void show() {}  // Uncommenting this will cause a compile-time error
}
```

**Expected Output (if method is not overridden):**
```
X show
```

#### Example 4: Private Method

```java
class SuperClass {
    private void hello() {
        System.out.println("Hello from SuperClass");
    }
}

class SubClass extends SuperClass {
    private void hello() {
        System.out.println("Hello from SubClass");
    }

    public static void main(String[] args) {
        SubClass obj = new SubClass();
        obj.hello();
    }
}
```

**Expected Output:**
```
Hello from SubClass
```

- Private methods are not inherited or overridden. Each class has its own version.

#### Example 5: Constructor and Overriding

```java
class One {
    One() {
        print();
    }

    void print() {
        System.out.println("One");
    }
}

class Two extends One {
    int value = 100;

    void print() {
        System.out.println("Two " + value);
    }
}

public class Test {
    public static void main(String[] args) {
        new Two();
    }
}
```

**Expected Output:**
```
Two 0
```

**Why?** 
- Because during the superclass constructor call, `value` isn't initialized yet (default is `0`).

#### Example 6: Overriding with Upcasting
```java
class Vehicle {
    void run() {
        System.out.println("Vehicle is running");
    }
}

class Bike extends Vehicle {
    void run() {
        System.out.println("Bike is running safely");
    }
}

public class Demo {
    public static void main(String[] args) {
        Vehicle obj = new Bike();
        obj.run();
    }
}
```
**Expected Output:**
```
Bike is running safely
```

#### Example 7: Calling superclass method
```java
class A {
    void show() {
        System.out.println("A show()");
    }
}

class B extends A {
    void show() {
        super.show();
        System.out.println("B show()");
    }
}

public class Main {
    public static void main(String[] args) {
        B obj = new B();
        obj.show();
    }
}
```

**Output:**
```
A show()
B show()
```

#### Example 8: Accessing superclass variable
```java
class A {
    int x = 10;
}

class B extends A {
    int x = 20;

    void display() {
        System.out.println(x);
        System.out.println(super.x);
    }
}

public class Test {
    public static void main(String[] args) {
        B b = new B();
        b.display();
    }
}
```

**Output:**
```
20
10
```

#### Example 9: Abstract method implementation
```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle");
    }
}

public class Test {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.draw();
    }
}
```

**Output:**
```
Drawing Circle
```

#### Example 10: Constructor chain with abstract class
```java
abstract class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }

    abstract void message();
}

class Child extends Parent {
    Child() {
        System.out.println("Child Constructor");
    }

    void message() {
        System.out.println("Child Message");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();
        p.message();
    }
}
```

**Output:**
```
Parent Constructor
Child Constructor
Child Message
```

#### Example 11: Interface implementation
```java
interface Printer {
    void print();
}

class LaserPrinter implements Printer {
    public void print() {
        System.out.println("Printing with LaserPrinter");
    }
}

public class Demo {
    public static void main(String[] args) {
        Printer p = new LaserPrinter();
        p.print();
    }
}
```

**Output:**
```
Printing with LaserPrinter
```

#### Example 12: Interface default method
```java
interface TestInterface {
    default void show() {
        System.out.println("Default show() in Interface");
    }
}

class Impl implements TestInterface {
    public void show() {
        System.out.println("Overridden show() in Impl");
    }
}

public class Main {
    public static void main(String[] args) {
        TestInterface t = new Impl();
        t.show();
    }
}
```

**Output:**
```
Overridden show() in Impl
```

---

#### Example 13: Interface with multiple inheritance
```java
interface A {
    default void show() {
        System.out.println("A");
    }
}

interface B {
    default void show() {
        System.out.println("B");
    }
}

class C implements A, B {
    public void show() {
        A.super.show();
        B.super.show();
        System.out.println("C");
    }
}

public class Demo {
    public static void main(String[] args) {
        C obj = new C();
        obj.show();
    }
}
```

**Output:**
```
A
B
C
```

#### Example 14: Final method cannot be overridden
```java
class Parent {
    final void show() {
        System.out.println("Parent show()");
    }
}

class Child extends Parent {
    // void show() { System.out.println("Child show()"); } // Compilation error
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();
        p.show();
    }
}
```

**Output:**
```
Parent show()
```

**Explanation**: 
- Final methods cannot be overridden. The `Child` class will inherit the method as-is.

#### Example 15: Final variable reassignment
```java
class Test {
    public static void main(String[] args) {
        final int x = 10;
        // x = 20; // Compilation error
        System.out.println(x);
    }
}
```

**Output:**
```
10
```

**Explanation**: 
- Final variables can only be assigned once.


#### Example 16: Constructor chaining
```java
class A {
    A() {
        this(10);
        System.out.println("Default Constructor");
    }

    A(int x) {
        System.out.println("Parameterized Constructor: " + x);
    }
}

public class Main {
    public static void main(String[] args) {
        new A();
    }
}
```
**Output:**
```
Parameterized Constructor: 10
Default Constructor
```

#### Example 17: Method call with superclass reference
```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog();
        a.sound();
    }
}
```

**Output:**
```
Dog barks
```

**Explanation**: 
- Method is resolved at runtime based on object type (`Dog`), not reference type (`Animal`).

#### Example 18: Overloading vs Overriding
```java
class A {
    void print(String msg) {
        System.out.println("A: " + msg);
    }
}

class B extends A {
    void print(String msg, int count) {
        System.out.println("B: " + msg + " " + count);
    }
}

public class Main {
    public static void main(String[] args) {
        B obj = new B();
        obj.print("Hello");
        obj.print("Hello", 3);
    }
}
```

**Output:**
```
A: Hello
B: Hello 3
```

**Explanation**: 
- `print(String)` is inherited from `A`, while `print(String, int)` is overloaded in `B`.

#### Example 19: Static methods are not overridden
```java
class Parent {
    static void show() {
        System.out.println("Parent static method");
    }
}

class Child extends Parent {
    static void show() {
        System.out.println("Child static method");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();
        p.show(); // Resolved at compile time
    }
}
```

**Output:**
```
Parent static method
```
**Explanation**: 
- Static methods are resolved by reference type, not object type (no polymorphism).

#### **Example 20: Abstract class with no abstract methods**

```java
abstract class Vehicle {
    void start() {
        System.out.println("Vehicle starting...");
    }
}

class Car extends Vehicle {
    void drive() {
        System.out.println("Car driving...");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle v = new Car();
        v.start();
        // v.drive(); // Compile-time error
    }
}
```

**Output:**
```
Vehicle starting...
```

**Explanation**: 
- You can create abstract classes without abstract methods. Also, `v` is of type `Vehicle`, so it can’t access `Car`-specific methods unless type-casted.

#### **Example 21: Interface with default and static methods**

```java
interface Printer {
    default void print() {
        System.out.println("Default print");
    }

    static void status() {
        System.out.println("Printer status OK");
    }
}

class Epson implements Printer {
    public void print() {
        System.out.println("Epson printing...");
    }
}

public class Main {
    public static void main(String[] args) {
        Printer p = new Epson();
        p.print();
        // p.status(); // Compile-time error
        Printer.status();
    }
}
```

**Output:**
```
Epson printing...
Printer status OK
```

**Explanation**: 
- `static` methods in interfaces are not inherited. You must call them using the interface name.

#### **Example 22: Interface inheritance**

```java
interface A {
    void show();
}

interface B extends A {
    void display();
}

class C implements B {
    public void show() {
        System.out.println("Show from A");
    }

    public void display() {
        System.out.println("Display from B");
    }
}

public class Main {
    public static void main(String[] args) {
        C obj = new C();
        obj.show();
        obj.display();
    }
}
```

**Output:**
```
Show from A
Display from B
```

**Explanation**: 
- Interfaces can extend other interfaces. Class `C` must implement all inherited methods.


#### **Example 23: Abstract class implementing interface**

```java
interface Engine {
    void start();
}

abstract class DieselEngine implements Engine {
    public void fuelType() {
        System.out.println("Diesel Fuel");
    }
}

class Truck extends DieselEngine {
    public void start() {
        System.out.println("Truck started");
    }
}

public class Main {
    public static void main(String[] args) {
        Truck t = new Truck();
        t.start();
        t.fuelType();
    }
}
```

**Output:**
```
Truck started
Diesel Fuel
```

**Explanation**: 
- Abstract class can implement an interface and leave method(s) unimplemented. Concrete subclass must implement them.


#### **Example 24: Abstract class constructor**

```java
abstract class Shape {
    Shape() {
        System.out.println("Shape constructor");
    }

    abstract void draw();
}

class Circle extends Shape {
    Circle() {
        System.out.println("Circle constructor");
    }

    void draw() {
        System.out.println("Drawing Circle");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.draw();
    }
}
```

**Output:**
```
Shape constructor
Circle constructor
Drawing Circle
```

> **Explanation**: Abstract class constructors are always executed first when an object is created via subclass.


#### **Example 25: Multiple interfaces, same method signature**

```java
interface A {
    void display();
}

interface B {
    void display();
}

class Demo implements A, B {
    public void display() {
        System.out.println("Display from Demo");
    }
}

public class Main {
    public static void main(String[] args) {
        Demo d = new Demo();
        d.display();
    }
}
```

**Output:**
```
Display from Demo
```

**Explanation**: 
- Java supports multiple interface inheritance. If method signatures are the same, one implementation satisfies both.


#### **Example 26: Interface with conflicting default methods**

```java
interface A {
    default void greet() {
        System.out.println("Hello from A");
    }
}

interface B {
    default void greet() {
        System.out.println("Hello from B");
    }
}

class C implements A, B {
    public void greet() {
        System.out.println("Hello from C");
    }
}

public class Main {
    public static void main(String[] args) {
        C c = new C();
        c.greet();
    }
}
```

**Output:**
```
Hello from C
```

**Explanation**: 
- When a class implements multiple interfaces with the same default method, you **must override** it to resolve ambiguity.

#### **Example 27: Can an abstract class implement an interface without implementing its methods?**

```java
interface Drawable {
    void draw();
}

abstract class AbstractShape implements Drawable {
    // Not implementing draw()
    void info() {
        System.out.println("This is an abstract shape.");
    }
}

class Square extends AbstractShape {
    public void draw() {
        System.out.println("Drawing a Square");
    }
}

public class Main {
    public static void main(String[] args) {
        Square s = new Square();
        s.draw();
        s.info();
    }
}
```

**Output:**
```
Drawing a Square
This is an abstract shape.
```

**Explanation**: 
- Abstract classes can implement interfaces **without implementing all methods**, but any concrete subclass **must implement** the remaining ones.

---

#### **Example 28: Interface extending another interface with same method**

```java
interface A {
    void show();
}

interface B extends A {
    void show(); // same method
}

class Test implements B {
    public void show() {
        System.out.println("Showing from Test");
    }
}

public class Main {
    public static void main(String[] args) {
        A a = new Test();
        a.show();
    }
}
```

**Output:**
```
Showing from Test
```

> **Explanation**: `B` inherits `show()` from `A`. Even if you re-declare it, it's still just one method to implement.

#### **Example 29: Abstract class with static method**

```java
abstract class Animal {
    static void sound() {
        System.out.println("Animal makes sound");
    }

    abstract void eat();
}

class Dog extends Animal {
    void eat() {
        System.out.println("Dog eats bone");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal.sound();
        Dog d = new Dog();
        d.eat();
    }
}
```

**Output:**
```
Animal makes sound
Dog eats bone
```

**Explanation**: 
- `static` methods in abstract classes **can be called directly using class name**. They are not overridden.

#### **Example 30: Can an interface have constructors?**

```java
interface MyInterface {
    // constructors not allowed
    // MyInterface() {}  // Compile-time error
}
```

**Explanation**: 
- **Interfaces cannot have constructors** because they cannot be instantiated directly. Only classes can have constructors.

---

#### **Example 31: Interface with constants**

```java
interface Constants {
    int MAX = 100;
}

public class Test {
    public static void main(String[] args) {
        System.out.println(Constants.MAX);
        // Constants.MAX = 200; // Compile-time error
    }
}
```

**Output:**
```
100
```

**Explanation**: 
- All fields in interfaces are **public static final by default**. That means they are **constants** and cannot be modified.

#### **Example 32: Abstract class with final method**

```java
abstract class Vehicle {
    final void stop() {
        System.out.println("Stopping vehicle...");
    }

    abstract void run();
}

class Bike extends Vehicle {
    void run() {
        System.out.println("Bike is running");
    }

    // void stop() {} // Cannot override final method
}

public class Main {
    public static void main(String[] args) {
        Bike b = new Bike();
        b.run();
        b.stop();
    }
}
```

**Output:**
```
Bike is running
Stopping vehicle...
```

**Explanation**: 
- `final` methods cannot be overridden, even if defined in an abstract class.

---

#### **Example 33: Abstract method in interface with object return type**

```java
interface Creator {
    Object create();
}

class IntegerCreator implements Creator {
    public Integer create() {
        return 42;
    }
}

public class Main {
    public static void main(String[] args) {
        Creator c = new IntegerCreator();
        System.out.println(c.create());
    }
}
```

**Output:**
```
42
```

**Explanation**: 
- This is **covariant return type**. `Integer` is a subclass of `Object`, so it’s allowed.

---

## 19. Find the output:
**Ex 1.** 
```
String s = "A";
s = "B";
System.out.println(list);
```
**Output:** 
```
B
``` 
**Ex 2.**
```
final int x = 10;
x=20;
System.out.println(x);
```
**Output:** 
```
The Java code will result in a compile-time error because you cannot reassign a value to a final variable after its initialization.
```
**Ex 3.** 
```
final List<Integer> list = new ArrayList<>();
list.add(2);
list.add(3);
list.add(4);
list.remove(2);
System.out.println(list);
```
**Output:** 
```
[2,3]
```

---
## 20. Sort a HashMap on the basis of key
```java
import java.util.*;

public class HashMapSorting {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<Integer, String> map = new HashMap<>();
        map.put(3, "Three");
        map.put(1, "One");
        map.put(4, "Four");
        map.put(2, "Two");

        // Sorting using TreeMap (keys will be sorted)
        TreeMap<Integer, String> sortedMap = new TreeMap<>(map);

        // Printing sorted map
        for (Map.Entry<Integer, String> entry : sortedMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}

```
**Alternative**: Using Stream API
```
import java.util.*;
import java.util.stream.Collectors;

public class HashMapSorting {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(3, "Three");
        map.put(1, "One");
        map.put(4, "Four");
        map.put(2, "Two");

        // Sorting using Stream and LinkedHashMap to maintain order
        Map<Integer, String> sortedMap = map.entrySet().stream()
            .sorted(Map.Entry.comparingByKey())
            .collect(Collectors.toMap(
                Map.Entry::getKey, 
                Map.Entry::getValue, 
                (e1, e2) -> e1, LinkedHashMap::new));

        // Printing sorted map
        sortedMap.forEach((key, value) -> System.out.println(key + " -> " + value));
    }
}
```
**One more Alternative**: List and `Collections.sort()` method
```java
import java.util.*;

public class HashMapSorting {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("Three", 3);
        map.put("One", 1);
        map.put("Four", 4);
        map.put("Two", 2);

        // Step 1: Get the keys and store them in a List
        ArrayList<String> keys = new ArrayList<>(map.keySet());

        // Step 2: Sort the List
        Collections.sort(keys);

        // Step 3: Print the sorted keys with values
        for (String key : keys) {
            System.out.println(key + " -> " + map.get(key));
        }
    }
}
```
**Output:**
```
Four -> 4
One -> 1
Three -> 3
Two -> 2
```

---

### 21. Second highest element in an Array using stream (Second largest)
    public static void main(String[] args) {
        int[] arr = {21, 2, 43, 114, 45, 6, 32, 54};

        if (arr.length < 2) {
            System.out.println("Array should have at least two elements.");
            return;
        }

        int firstHighest = Integer.MIN_VALUE;
        int secondHighest = Integer.MIN_VALUE;

        for (int n : arr) {
            if (n > firstHighest) {
                secondHighest = firstHighest; // Update secondHighest before changing firstHighest
                firstHighest = n;
            } else if (n > secondHighest && n < firstHighest) {
                secondHighest = n;
            }
        }

        if (secondHighest == Integer.MIN_VALUE) {
            System.out.println("No second highest element found.");
        } else {
            System.out.println("First Highest: " + firstHighest);
            System.out.println("Second Highest: " + secondHighest);
        }    
    }
    
**Using Stream API**
```
public static void main(String[] args) {
    int[] arr = {21, 2, 43, 114, 45, 6, 32, 54};
    Optional<Integer> secondHighest = Arrays.stream(arr)
            .distinct() // Remove duplicates
            .boxed() // Convert to Integer for sorting
            .sorted((a, b) -> b - a) // Sort in descending order
            .skip(1) // Skip the highest element
            .findFirst(); // Get the second highest

    if (secondHighest.isPresent()) {
        System.out.println("Second Highest: " + secondHighest.get());
    } else {
        System.out.println("No second highest element found.");
    }
}

```

#### Reverse a String using StringBuilder
```java
String reversed = new StringBuilder(str).reverse().toString();
```


### Some Stream Questions
#### Third highest number
```java
Optional<Integer> heightestSalary = list.stream().distinct().sorted((a, b) -> b - a).skip(2).findFirst(); 
System.out.println(heightestSalary); // Optional[1500]
System.out.println(heightestSalary.get()); // 1500
```

#### Ascending order list with `sorted((a,b)->a.compareTo(b))`
```java
List<Integer> ascOrderSortedList = list.stream().distinct().sorted((a,b)->a.compareTo(b)).collect(Collectors.toList()); 
System.out.println(ascOrderSortedList); // [1000, 1500, 2000, 2300]
```

#### Ascending order list with `sorted()`
```java
List<Integer> ascOrderSortedList = list.stream().distinct().sorted().collect(Collectors.toList()); 
System.out.println(ascOrderSortedList); // [1000, 1500, 2000, 2300]
```

#### Ascending order list with `sorted((a,b)->b-a)`
```java
List<Integer> descOrderSortedList = list.stream().distinct().sorted((a,b)->b-a).collect(Collectors.toList()); 
System.out.println(descOrderSortedList); // [2300, 2000, 1500, 1000]
```

#### Ascending order list with comparator `sorted(Comparator.reverseOrder())`
```java
List<Integer> reverserOrderList = list.stream().distinct().sorted(Comparator.reverseOrder()).collect(Collectors.toList());
System.out.println(reverserOrderList); // [2300, 2000, 1500, 1000]
```

#### Number with limit 2
```java
List<Integer> limit2number = list.stream().distinct().sorted().limit(2).collect(Collectors.toList());
System.out.println(heightestSalary); // [1000, 1500]
```

#### Approach 1: Reverse String using Stream
```java
String str = "Ravi Kumar";
String rev = new StringBuilder(str.chars().mapToObj(c -> String.valueOf((char) c)).collect(Collectors.joining())).reverse().toString();
System.out.println(rev); // ramuK ivaR
```

#### Approach 2: Reverse String using Stream without `reverse()` method
```java
public static void main(String[] args) {
    String input = "hello";

    String reversed = IntStream.rangeClosed(1, input.length())
            .mapToObj(i -> input.charAt(input.length() - i))
            .map(String::valueOf)
            .collect(Collectors.joining());

    System.out.println(reversed);  // Output: olleh
}
```

#### Count character from a String
```java
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        String input = "programming";

        Map<Character, Long> characterCount = input.chars()  // IntStream of character codes
                .mapToObj(c -> (char) c)                     // convert int to Character
                .collect(Collectors.groupingBy(               // group by character
                        Function.identity(),                 // key: character itself
                        Collectors.counting()                // value: count occurrences
                )); // {p=1, a=1, r=2, g=2, i=1, m=2, n=1, o=1}

        Map<Character, Integer> cc = input.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.groupingBy(
                    Function.identity(),
                    Collectors.summingInt(c -> 1)            // If you want interger counts
                )); // {p=1, a=1, r=2, g=2, i=1, m=2, n=1, o=1}

        Map<Character, Integer> countMap = input.chars()
                .mapToObj(c -> (char) c)
                .collect(Collectors.toMap(
                    Function.identity(),    // Key: each character
                    c -> 1,                 // Initial count = 1
                    Integer::sum             // Merge function to sum counts
                )); // {p=1, a=1, r=2, g=2, i=1, m=2, n=1, o=1}

    }
}
```
#### Find String starts with "R" 
```java
List<String> list = Arrays.asList("Suman", "Shirish", "Vedant", "Vedika", "Rahul", "Rohit", "Rashmi", "Rahul");
List<String> rList = list.distinct().filter(s->s.startsWith("R")).collect(Collectors.toList());
System.out.println(rList); // [Rahul, Rohit, Rashmi]
```

---
### 21. TODO 

---
### 22. Hashmap sorting using keys where it contains one null key
In Java, when sorting a `HashMap` by keys that include a `null` key, you need to handle the `null` key explicitly. Since `HashMap` allows **one null key**, and **`TreeMap` does not allow null keys** (it throws `NullPointerException`), we must work around this using custom sorting logic.

### Approach 1: Using LinkedHashMap

```java
import java.util.*;

public class HashMapSortWithNullKey {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        map.put("Banana", "Yellow");
        map.put(null, "No Color");
        map.put("Apple", "Red");
        map.put("Mango", "Orange");

        // Separate null key entry
        String nullKeyValue = map.remove(null);

        // Sort non-null keys using TreeMap
        Map<String, String> sortedMap = new TreeMap<>(map);

        // Optional: Insert null key entry at the beginning
        LinkedHashMap<String, String> finalSortedMap = new LinkedHashMap<>();
        if (nullKeyValue != null) {
            finalSortedMap.put(null, nullKeyValue); // you can also place this at the end if needed
        }
        finalSortedMap.putAll(sortedMap);

        // Print final sorted map
        for (Map.Entry<String, String> entry : finalSortedMap.entrySet()) {
            System.out.println("Key: " + entry.getKey() + " -> Value: " + entry.getValue());
        }
    }
}
```

#### Output:
```
{null=No Color, Apple=Red, Banana=Yellow, Mango=Orange}
```

#### Explanation:
- `HashMap` allows one `null` key.
- `TreeMap` does not allow `null` keys (it throws `NullPointerException` because it uses `compareTo()`).
- We remove the `null` key entry and sort the remaining keys using `TreeMap`.
- Finally, re-insert the `null` key manually (at the beginning or end depending on your use case).


Yes, here’s **another approach** to sort a `HashMap` **by keys** including a `null` key, **without removing it manually**, using a **custom `Comparator` with `LinkedHashMap` and `Stream API`**:

---

### Approach 2: Using Java 8 Streams and a Custom `Comparator`

```java
import java.util.*;
import java.util.stream.*;

public class HashMapSortWithNullKeyStream {
    public static void main(String[] args) {
        Map<String, String> map = new HashMap<>();
        map.put("Banana", "Yellow");
        map.put(null, "No Color");
        map.put("Apple", "Red");
        map.put("Mango", "Orange");

        // Sort by keys, handling null key
        Map<String, String> sortedMap = map.entrySet()
            .stream()
            .sorted(Map.Entry.comparingByKey(
                Comparator.nullsFirst(String::compareTo) // null keys come first
            ))
            .collect(Collectors.toMap(
                Map.Entry::getKey,
                Map.Entry::getValue,
                (e1, e2) -> e1,
                LinkedHashMap::new
            ));

        // Print final sorted map
        sortedMap.forEach((key, value) -> 
            System.out.println("Key: " + key + " -> Value: " + value)
        );
    }
}
```


#### Output:
```
{null=No Color, Apple=Red, Banana=Yellow, Mango=Orange}

```

#### What's happening:
- `Map.Entry.comparingByKey(Comparator.nullsFirst(...))` safely compares keys, putting `null` first.
- The result is collected into a `LinkedHashMap` to preserve the sorted order.
- This approach avoids mutating the original map and handles `null` keys cleanly.

#### Variation: To put `null` key **at the end**
Just use `Comparator.nullsLast(String::compareTo)` instead of `nullsFirst`.

### Approach 3: Using TreeMap and Custom `Comparator`

```java
import java.util.Comparator;
import java.util.HashMap;
import java.util.Map;
import java.util.TreeMap;

public class HashMapSortingWithNullKey {

    public static void main(String[] args) {
        // Sample HashMap with a null key
        HashMap<String, Integer> myMap = new HashMap<>();
        myMap.put("apple", 1);
        myMap.put(null, 2); // Null key
        myMap.put("banana", 3);

        // Sort the HashMap by key, placing null keys at the beginning
        TreeMap<String, Integer> sortedMap = new TreeMap<>(Comparator.nullsFirst(Comparator.naturalOrder()));
        sortedMap.putAll(myMap);

        // Print the sorted map
        System.out.println(sortedMap);
    }
}
```
#### Output:
```
{null=2, apple=1, banana=3}
```

---
### 23. Print Fibonnaci series using stream
```java
import java.util.stream.Stream;
import java.util.function.UnaryOperator;

public class FibonacciStream {

    public static void main(String[] args) {
        
        // Generate the Fibonacci sequence using iterate
        // UnaryOperator<int[]> which is a functional interface
        Stream.iterate(new int[]{0, 1}, fib -> new int[]{fib[1], fib[0] + fib[1]})
              .limit(10)
              .map(fib -> fib[0])
              .forEach(System.out::println);
    }
}
```
### Explanation:
- `Stream.iterate(...)`: Starts with an initial pair {0, 1}.
- `fib -> new int[]{fib[1], fib[0] + fib[1]}`: Transforms each pair into the next one in the sequence.
- `limit(10)`: Limits the output to the first 10 Fibonacci numbers.
- `.map(fib -> fib[0])`: Extracts the first element (the current Fibonacci number) from each pair.
- `.forEach(System.out::println)`: Prints each number.

### Sample Output:
```java
0
1
1
2
3
5
8
13
21
34
```

---
### 24. Solve 
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `let str1 = "78";` `let str2 = "78";` | `"Result: 1416"`  |   |
 
```
TODO

```

---
### 25. Count character from a String using `Stream()`
```java
public static void main(String[] args) {
    String s = "adgafagagAagagag";
    long count = 0;
    char ch = 'A';

    count = s.chars().map(Character::toUpperCase).filter(x -> (x==ch)).count(); // long count()
    System.out.println("count of " + ch + " : " + count); // Output: 8
}
```

---
### 26. Remove duplicate Number from Array in Java
```java
public static void main(String[] args) {
    // Sample array with duplicates
    Integer[] numbersWithDuplicates = {1, 2, 2, 3, 4, 4, 5, 1, 6, 6, 7};

    // Remove duplicates using a Set
    Set<Integer> uniqueNumbersSet = new HashSet<>(Arrays.asList(numbersWithDuplicates));

    // Convert the Set back to an array
    Integer[] uniqueNumbersArray = uniqueNumbersSet.toArray(new Integer[0]);

    // Print the array with unique numbers
    System.out.println("Array with unique numbers: " + Arrays.toString(uniqueNumbersArray)); // Output: [1, 2, 3, 4, 5, 6, 7]
}
```

---
### 27. Remove duplicate Character from Array in Java
```java
public static void main(String[] args) {
    // Sample array with duplicates
    Character[] charactersWithDuplicates = {'a', 'l', 'g', 'n', 'a', 'l', 'a'};

    // Remove duplicates using a Set
    Set<Character> uniqueCharactersSet = new HashSet<>(Arrays.asList(charactersWithDuplicates));

    // Convert the Set back to an array
    Character[] uniqueCharactersArray = uniqueCharactersSet.toArray(new Character[0]);

    // Print the array with unique numbers
    System.out.println("Array with unique characters: " + Arrays.toString(uniqueCharactersArray)); // Output: algn
}
```

---
### 28. Create a String from a List of Character
```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

public class ListCharToString {

    public static void main(String[] args) {
        // List of characters with duplicates
        List<Character> charactersWithDuplicates = Arrays.asList('a', 'l', 'g', 'n', 'a', 'l', 'a');

        // Remove duplicates using a Set
        Set<Character> uniqueCharactersSet = new HashSet<>(charactersWithDuplicates);

        // Convert the Set to a String
        String uniqueCharactersString = uniqueCharactersSet.stream()
                .map(String::valueOf) // Convert each Character to a String
                .collect(Collectors.joining()); // Join the strings

        String uniqueCharactersString1 = charactersWithDuplicates.stream()
                .map(String::valueOf) // Convert each Character to a String
                .collect(Collectors.joining()); // Join the strings

        // Print the string
        System.out.println("String with unique characters: " + uniqueCharactersString); // Output: agln
        System.out.println("String with unique characters: " + uniqueCharactersString1); // Output: algnala
    }
}
```
**[Sample code:](https://onecompiler.com/java/43fszg2vp)**

---
### 29. Flatter an Array using Java Stream. 
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `"array = [1, [2, 3], [4, [5, 6]], 7]"` | `"[1, 2, 3, 4, 5, 6, 7]"`  | All element should be in 1D-Array  |
| `"array = [[1, 2], [3, 4], [5, 6]]"` | `"[1, 2, 3, 4, 5, 6]"`  | All element should be in 1D-Array  |
| `"array = [1, [2, 3], [4, [5, 6]], 7]"` | `"[1, 2, 3, 4, 5, 6, 7]"`  | All element should be in 1D-Array  |
 
```java
public class Main {
    public static void main(String[] args) {
        List<?> nestedList = Arrays.asList(
            1, 
            Arrays.asList(2, 3), 
            Arrays.asList(4, Arrays.asList(5, 6)),
            7
        );

        List<Integer> flatList = flatten(nestedList)
                .collect(Collectors.toList());

        System.out.println(flatList); 
    }
    
    private static Stream<Integer> flatten(List<?> list) {
        return list.stream()
                .flatMap(e->{
                  if (e instanceof Integer) {
                        return Stream.of((Integer) e); // If element is integer, stream it
                    } else if (e instanceof List<?>) {
                        return flatten((List<?>) e); // Recursive flatten
                    } else {
                        throw new IllegalArgumentException("Unsupported type: " + e.getClass());
                    }
                });
    }
}
```
#### Examples
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `"array = [[2, 3], [4], [5, 6]]"` | `"[2, 3, 4, 5, 6]"`  | All element should be in 1D-Array  |
| `"array = [[1, 2], [3, 4], [5, 6]]"` | `"[1, 2, 3, 4, 5, 6]"`  | All element should be in 1D-Array  |

```java
List<List<String>> listOfLists = Arrays.asList(
    Arrays.asList("A", "B"),
    Arrays.asList("C", "D")
);
List<String> flatList = listOfLists.stream()
                                    .flatMap(List::stream)
                                    .collect(Collectors.toList()); // flatList will contain ["A", "B", "C", "D"]

```
---
### 30. Find the longest string in a list of strings using Java streams:
```java
List<String> strings = Arrays
              .asList("apple", "banana", "cherry", "date", "grapefruit");
Optional<String> longestString = strings
              .stream()
              .max(Comparator.comparingInt(String::length)); // Output:
```

---
### 31. Calculate the average age of a list of Person objects using Java streams:
```java
List<Person> persons = Arrays.asList(
    new Person("Alice", 25),
    new Person("Bob", 30),
    new Person("Charlie", 35)
);
double averageAge = persons.stream()
                          .mapToInt(Person::getAge)
                          .average()
                          .orElse(0);
```
---
### 32. Check if a list of integers contains a prime number using Java streams:
```java
public boolean isPrime(int number) {
  if (number <= 1) {
    return false;
  }
  for (int i = 2; i <= Math.sqrt(number); i++) {
    if (number % i == 0) {
        return false;
    }
  }
  return true;
}
 
private void printPrime() {
  List<Integer> numbers = Arrays.asList(2, 4, 6, 8, 10, 11, 12, 13, 14, 15);
  boolean containsPrime = numbers.stream()
                                 .anyMatch(this::isPrime);
  System.out.println("List contains a prime number: " + containsPrime);

}
```
---
### 33. Merge two sorted lists into a single sorted list using Java streams:
```java
List<Integer> list1 = Arrays.asList(1, 3, 5, 7, 9);
List<Integer> list2 = Arrays.asList(2, 4, 6, 8, 10);
List<Integer> mergedList = Stream.concat(list1.stream(), list2.stream())
                                .sorted()
                                .collect(Collectors.toList());
```
---
### 34. Find the intersection of two lists using Java streams:
```java
List<Integer> list1 = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> list2 = Arrays.asList(3, 4, 5, 6, 7);
List<Integer> intersection = list1.stream()
                                  .filter(list2::contains)
                                  .collect(Collectors.toList());
```
---
### 35. Remove duplicates from a list while preserving the order using Java streams:
```java
List<Integer> numbersWithDuplicates = Arrays.asList(1, 2, 3, 2, 4, 1, 5, 6, 5);
List<Integer> uniqueNumbers = numbersWithDuplicates
                                       .stream()
                                       .distinct()
                                       .collect(Collectors.toList());
```
---
### 36. Given a list of transactions, find the sum of transaction amounts for each day using Java streams:
```java
List<Transaction> transactions = Arrays.asList(
    new Transaction("2022-01-01", 100),
    new Transaction("2022-01-01", 200),
    new Transaction("2022-01-02", 300),
    new Transaction("2022-01-02", 400),
    new Transaction("2022-01-03", 500)
);

Map<String, Integer> sumByDay = transactions
                        .stream()
                        .collect(Collectors.groupingBy(Transaction::getDate,
                               Collectors.summingInt(Transaction::getAmount)));
```
---
### 37. Find the kth smallest element in an array using Java streams:
```java
int[] array = {4, 2, 7, 1, 5, 3, 6};
int k = 3; // Find the 3rd smallest element
int kthSmallest = Arrays.stream(array)
                       .sorted()
                       .skip(k - 1)
                       .findFirst()
                       .orElse(-1);
```
---
### 38. Given a list of strings, find the frequency of each word using Java streams:
```java
List<String> words = Arrays.asList("apple", "banana", "apple", "cherry", 
                                    "banana", "apple");
Map<String, Long> wordFrequency = words
              .stream()
              .collect(Collectors
                    .groupingBy(Function.identity(), Collectors.counting())
                );
```
----
### 39. Implement a method to partition a list into two groups based on a predicate using Java streams:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);
Map<Boolean, List<Integer>> partitioned = numbers
                        .stream()
                        .collect(Collectors.partitioningBy(n -> n % 2 == 0));
List<Integer> evenNumbers = partitioned.get(true);
List<Integer> oddNumbers = partitioned.get(false);
System.out.println("Even numbers: " + evenNumbers);
System.out.println("Odd numbers: " + oddNumbers);
```
---
### 40. Q. Implement a method to calculate the Fibonacci sequence using Java streams:
```java
Stream<Long> fibonacci = Stream.iterate(
                    new long[]{0, 1}, f -> new long[]{f[1], f[0] + f[1]})
                 .mapToLong(f -> f[0]);
// Print first 10 Fibonacci numbers
fibonacci.limit(10).forEach(System.out::println); 
```
---
### 41. Find the median of a list of integers using Java streams:
```java
List<Integer> numbers = Arrays.asList(5, 2, 1, 3, 4);
OptionalDouble median = numbers.stream()
                               .sorted()
                               .mapToInt(Integer::intValue)
                               .collect(IntStatistics.summaryStatistics())
                               .getMedian();
System.out.println("Median: " + median.getAsDouble());
```
---
### 42. Given a list of strings, find the longest common prefix using Java streams:
```java
List<String> strings = Arrays.asList("flower", "flow", "flight");
String longestCommonPrefix = strings.stream()
                   .reduce((s1, s2) -> {
                       int length = Math.min(s1.length(), s2.length());
                       int i = 0;
                       while (i < length && s1.charAt(i) == s2.charAt(i)) {
                           i++;
                       }
                       return s1.substring(0, i);
                   })
                   .orElse("");
System.out.println("Longest common prefix: " + longestCommonPrefix);
```
---
### 43. Find the maximum product of two integers in an array using Java streams:
```java
int[] array = {1, 4, 3, 6, 2, 7, 8};
int maxProduct = IntStream.range(0, array.length)
                      .mapToObj(i -> IntStream.range(i + 1, array.length)
                                              .map(j -> array[i] * array[j])
                                              .max()
                                              .orElse(Integer.MIN_VALUE))
                      .max(Integer::compare)
                      .orElse(Integer.MIN_VALUE);
System.out.println("Maximum product: " + maxProduct);
```
---
### 44. Implement a method to find all anagrams in a list of strings using Java streams:
```java
List<String> words = Arrays.asList("listen", "silent", "hello",
                                   "world", "night", "thing");
Map<String, List<String>> anagrams = words.stream()
                                   .collect(Collectors.groupingBy(str -> {
                                       char[] chars = str.toCharArray();
                                       Arrays.sort(chars);
                                       return new String(chars);
                                   }));
System.out.println("Anagrams: " + anagrams); // TODO
```
---
### 45. Given a list of intervals, find the total covered length using Java streams:
```java
List<Interval> intervals = Arrays.asList(new Interval(1, 3),
                   new Interval(5, 8), new Interval(10, 12));
int totalCoveredLength = intervals.stream()
             .mapToInt(interval -> interval.getEnd() - interval.getStart())
             .sum();
System.out.println("Total covered length: " + totalCoveredLength); // TODO
```
### 46. Find the number of occurrences of a given character in a list of strings using Java streams:
```java
List<String> strings = Arrays.asList("apple", "banana", "orange", 
                                    "grape", "melon");
char target = 'a';
long occurrences = strings.stream()
                         .flatMapToInt(CharSequence::chars)
                         .filter(c -> c == target)
                         .count();
System.out.println("Occurrences of '" + target + "': " + occurrences); // TODO
```
---
### 47. Given a list of integers, find all pairs of numbers that sum up to a given target using Java streams:
```java
List<Integer> numbers = Arrays.asList(2, 4, 6, 8, 10);
int target = 12;
Set<String> pairs = numbers.stream()
      .flatMap(i -> numbers.stream().
                    map(j -> i + j == target ? "(" + i + ", " + j + ")" : ""))
      .filter(s -> !s.isEmpty())
      .collect(Collectors.toSet());
System.out.println("Pairs that sum up to " + target + ": " + pairs); // TODO
```

---
### 48. Given a list of integers, find all non duplicate integers using Java streams:
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 2, 4, 5, 6, 4, 7, 8, 9, 9);

// Count the occurrences of each number
Map<Integer, Long> frequencyMap = numbers.stream()
        .collect(Collectors
              .groupingBy(Function.identity(), Collectors.counting())
         );

// Filter out non-duplicate numbers
numbers.stream()
        .filter(number -> frequencyMap.get(number) == 1)
        .forEach(System.out::println); // TODO
```
---
### 49. Given a list of strings, find the longest string using Java streams.
```java
List<String> strings = Arrays.asList("apple", "banana", "orange",
                                     "grape", "kiwi");

String longestString = strings.stream()
        .max((s1, s2) -> Integer.compare(s1.length(), s2.length()))
        .orElse(null);
        System.out.println(longesString); // TODO
```



### 50. Stream API  
Stream API in Java is used for processing collections efficiently.

Examples:
```java
List<Integer> evenNumbers = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

List<String> stringList = numbers.stream()
    .map(String::valueOf)
    .collect(Collectors.toList());
```
---
### 51. Reverse a String in O(n/2) time complexity.
```java
public static void main(String[] args) {
    String str= "ghfgytytyp";

    char[] ss = str.toCharArray();
    
    for (int i = 0; i < ss.length/2; i++) {
    char temp = ss[i];
    ss[i] = ss[ss.length-1-i];
    ss[ss.length-1-i] = temp;
    }
    
    String rev = new String(ss);
    System.out.println(rev); // Output: pytytygfhg
}
```
---
### 52. What will be the result of a given code
```java
class Example {
    private static List<String> cache = new ArrayList<>();

    public void addData() {
        for (int i = 0; i < 1000000; i++) {
            cache.add("Data-" + i);
        }
    }
}
```

The `Example` class you've provided uses a **static list** (`cache`) that stores data when `addData()` is called. Let me break down the behavior, and point out potential concerns and use cases.

### Key Observations

1. **`cache` is static:**
   - This means the list is **shared among all instances** of the `Example` class.
   - The data persists as long as the application is running (in memory).

2. **Memory Usage:**
   - You're adding 1 million strings to memory.
   - This could cause **OutOfMemoryError** if called multiple times or on constrained memory environments.

3. **Thread-Safety:**
   - `ArrayList` is **not thread-safe**.
   - If multiple threads call `addData()` concurrently, **data corruption** or **ConcurrentModificationException** may occur.

---

### When to Use This Approach

- If you're **caching data** that needs to be **globally accessible** across instances.
- When the list doesn't need to change often (read-heavy scenarios).
- When memory and thread safety are carefully managed.

### Potential Improvements
#### 1. Use a thread-safe collection:

```java
private static List<String> cache = Collections.synchronizedList(new ArrayList<>());
```

#### 2. Avoid memory overflow:

Consider clearing or limiting the size of the list:

```java
if (cache.size() > 1000000) {
    cache.clear();
}
```

#### 3. Use better caching strategies:
If this is for real caching, consider using:
- **`ConcurrentHashMap`**
- **`Guava Cache`**
- **`Caffeine Cache`**

### Real-World Analogy
Imagine a static list as a **global whiteboard in an office**: every employee (object instance) can write to and read from it. If too many employees write to it at once (threads), it can become unreadable (corrupted). And if you never erase anything, it’ll eventually run out of space (memory).

---
## Q. To optimize the following Spring Boot controller logic:
```java
@GetMapping("/fn")
public ResponseEntity<MyResponseDTO> fn() {
    List<?> m1 = m1(); 
    List<?> m2 = m2(); 
    List<?> m3 = m3(); 

    MyResponseDTO response = new MyResponseDTO(m1, m2, m3);
    return ResponseEntity.ok(response);
}
```

you can consider multiple types of **optimizations** based on your **application needs**—whether it’s **performance**, **code maintainability**, or **scalability**. Here’s how:

### **Use `CompletableFuture` for Parallel Execution (Async)**

If `m1()`, `m2()`, and `m3()` are **independent**, you can call them in **parallel** using `CompletableFuture` to improve performance:

```java
@GetMapping("/fn")
public ResponseEntity<MyResponseDTO> fn() throws ExecutionException, InterruptedException {
    CompletableFuture<List<?>> f1 = CompletableFuture.supplyAsync(() -> m1());
    CompletableFuture<List<?>> f2 = CompletableFuture.supplyAsync(() -> m2());
    CompletableFuture<List<?>> f3 = CompletableFuture.supplyAsync(() -> m3());

    CompletableFuture.allOf(f1, f2, f3).join();

    MyResponseDTO response = new MyResponseDTO(f1.get(), f2.get(), f3.get());
    return ResponseEntity.ok(response);
}
```

#### Note:
You may annotate your service with `@Async` and enable `@EnableAsync` in a config class.

---
## Q. WAP using Java8 features: Compute average age of the all male authors having age less than 25 years
```java
import java.util.*;
import java.util.stream.*;

class Book {
    int book_id;
    String name;
    Author author;

    // constructor & getter setter
}

class Author {
    String name;
    int age;
    String gender;

    // constructor & getter setter
}

public class Main {
    public static void main(String[] args) {
        List<Book> books = Arrays.asList(
            new Book(1, "Java Basics", new Author("John", 22, "Male")),
            new Book(2, "Advanced Java", new Author("Mike", 24, "Male")),
            new Book(3, "Spring Boot", new Author("Anna", 26, "Female")),
            new Book(4, "Microservices", new Author("Tom", 28, "Male")),
            new Book(5, "Streams API", new Author("Alex", 21, "Male"))
        );

        OptionalDouble averageAge = books.stream()
            .map(Book::getAuthor)
            .filter(author -> author.getGender().equalsIgnoreCase("Male") && author.getAge() < 25)
            .mapToInt(Author::getAge)
            .average();

        if (averageAge.isPresent()) {
            System.out.println("Average age of male authors < 25: " + averageAge.getAsDouble());
        } else {
            System.out.println("No male authors under 25 found.");
        }
    }
}
```
---
## Q. nth Highest salary using stream.
```java
Long nthSalary = list.stream().distinct().sorted((a,b)-> b-a).skip(n).findFirst().orElse(0);

Long nthSalary = list.stream().map(n->n.getSalary()).distinct().sorted((a,b)-> b-a).skip(n).findFirst().orElse(0);
```
---
## Q. How to find the most frequent character (case-insensitive, ignoring spaces and digits) across a list of strings using Java streams
```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class MostFrequentChar {

    public static Character findMostFrequentCharacter(List<String> strings) {
        return strings.stream()
                .flatMap(s -> s.toLowerCase().chars() // Convert to lowercase and get IntStream of chars
                        .filter(Character::isLetter) // Filter out non-letter chars
                        .mapToObj(c -> (char) c)) // Convert back to Stream of Character objects
                .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
                .entrySet().stream()
                .max(Map.Entry.comparingByValue())
                .map(Map.Entry::getKey)
                .orElse(null);
    }

    public static void main(String[] args) {
        List<String> input = Arrays.asList("Java", "Streams 123", "are powerful!");
        Character mostFrequent = findMostFrequentCharacter(input);
        System.out.println(mostFrequent); // Output: a
    }
}
```
The code first converts all strings to lowercase and extracts characters, filtering out spaces and digits. Then, it counts the occurrences of each character and returns the most frequent one.

---
## Q. How to return a new list with each value multiplied by 2 using reduce() in Java
```java
import java.util.Arrays;
import java.util.List;
import java.util.ArrayList;

public class MultiplyList {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        List<Integer> multipliedNumbers = numbers.stream()
            .reduce(new ArrayList<>(), (list, number) -> {
                List<Integer> newList = new ArrayList<>(list);
                newList.add(number * 2);
                return newList;
            }, (list1, list2) -> {
                list1.addAll(list2);
                return list1;
            });

        System.out.println(multipliedNumbers); // Output: [2, 4, 6, 8, 10]
    }
}
```
This code uses the `reduce` operation to iterate through the original list and construct a new list with doubled values. The accumulator function creates a new list in each step, avoiding modification of the original. The combiner function is essential for parallel streams, ensuring correct merging of results.

---
## Q.  


### Links:
https://www.interviewbit.com/java-interview-questions-for-5-years-experience/
https://www.geeksforgeeks.org/output-of-java-program-set-1/






