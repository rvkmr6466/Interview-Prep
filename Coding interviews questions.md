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
### 2. Find the longest uniform substring.
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
```
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
```
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
```
public class Main {
    public static void main(String[] args) {
      String s1= "Ravi Kumar";
      String[] str = s1.split(" ");
      String sss = "";
      List<String> list = new ArrayList<>();
      
      for (int i=0; i<str.length; i++) {
        String s = reverStr(str[i]);
        list.add(s);
      }
      
      System.out.println(Arrays.toString(str));
      System.out.println(list.toString());
      
      System.out.println(sss.join(" ", list));
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
#### Output
```
ivaR ramuK
```
#### Solution 2:
```
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
      
      System.out.println(reverseStr.join(" ", list));
  }
  
}
```
#### Output
```
ivaR ramuK amrahS
```

---
## 15. Find output
```
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
```
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
```
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
    // void show() { System.out.println("Child show()"); } // ❌ Compilation error
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
        // x = 20; // ❌ Compilation error
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
        // v.drive(); // ❌ Compile-time error
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
        // p.status(); // ❌ Compile-time error
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
    // MyInterface() {}  // ❌ Compile-time error
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
        // Constants.MAX = 200; // ❌ Compile-time error
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

    // void stop() {} // ❌ Cannot override final method
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
---
### 21. Reverse a String  
```java
String reversed = new StringBuilder(str).reverse().toString();
```

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
### 23. fibonnaci using stream


---
### 24. Solve 
#### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `let str1 = "78";` `let str2 = "78";` | `"Result: 1416"`  |   |
 


---
### 25. 

---
### 26. 

---
### 27. 

---
### 28. 



---

### Links:
https://www.interviewbit.com/java-interview-questions-for-5-years-experience/
https://www.geeksforgeeks.org/output-of-java-program-set-1/




