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
Input: "aaabbbbccda" the longest uniform substring is "bbbb" (which starts at index 3 and is 4 characters long). 

Ex 1 : s = "abc"
Output = [0, 1] 
 
Ex 2 s = "aabbbc"
Output = [2, 3] 

Ex 3 s = "aabbbaaaa"
Output = [5, 4]

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
Input: s = “geeksforgeeks”
Output: 7 
Explanation: The longest substrings without repeating characters are “eksforg” and “ksforge”, with lengths of 7.

Input: s = “aaa”
Output: 1
Explanation: The longest substring without repeating characters is “a”

Input: s = “abcdefabcbb”
Output: 6
Explanation: The longest substring without repeating characters is “abcdef”.

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
