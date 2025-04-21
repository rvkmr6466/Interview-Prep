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
    		System.out.println("Child ");
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
### 13.  

