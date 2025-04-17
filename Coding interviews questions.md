# Coding Questions for Interviews

---

## 1. First Repeating Character from a String

### Examples:

| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "geeksforgeeks"` | `"e"`  | 'e' repeats at third position.  |
| `s = "hellogeeks"` | `"l"`  | 'l' repeats at fourth position.  |
| `s = "abc"` | `"-1"`  | No repeated character found.         |

### Solution:

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
---
## 2. Find the longest uniform substring.
### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "aaabbbbccda"` | `"[3,4]"`  | "bbbb" the longest uniform substring (which starts at index 3 and is 4 characters long).  |
| `s = "aabbbc"` | `"[2, 3]"`  | "bbb" is the longest uniform substring.  |
| `s = "aabbbaaaa"` | `"[5, 4]"`  | "aaaa" is the longest uniform substring.         |

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
## 3. Find Longest Substring Without Repeating Characters  
### Examples:
| Input            | Output | Explanation                          |
|-----------------|--------|--------------------------------------|
| `s = "geeksforgeeks"` | `"7"`  | The longest substrings without repeating characters are “eksforg” and “ksforge”, with lengths of 7.  |
| `s = "aaa"` | `"1"`  | The longest substring without repeating characters is “a”.  |
| `s = "abcdefabcbb"` | `"6"`  | The longest substring without repeating characters is “abcdef”.         |

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
```
public class Main {
    public static void main(String[] args) {
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

## 4. Find Output
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
