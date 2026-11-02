
# [0242. Valid Anagram - E](https://leetcode.com/problems/valid-anagram/)
- `Topics: Hash Table, String, Sorting`

Given two strings s and t, return true if t is an anagram of s, and false otherwise.
 
> Constraints: 
> - 1 <= s.length, t.length <= 5 * 10^4
> - s and t consist of lowercase English letters.
> 
> Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

## Solution 1: primitive HashMap

### Idea.
- hashmap: sum letters of `s` rest letter of `t`.
- if any count letter is `!= 0,` return false.

### Complexity
> **TC: \(O(n)\). SC: \(O(1)\).**

### Code

> **Java**

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    int[] freq = new int[26];
    for (int i = 0; i < s.length(); i++) {
        freq[s.charAt(i) - 'a']++;
        freq[t.charAt(i) - 'a']--;
    }valid
    
    for (int f : freq) {
        if (f != 0) return false;
    }

    return true;
}
```

> **Python**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        freq = [0] * 26
        for i in range(len(s)):
            freq[ord(s[i]) - ord('a')] += 1
            freq[ord(t[i]) - ord('a')] -= 1
            
        for f in freq:
            if f != 0:
                return False

        return True
```

## Solution 2: HashMap.merge

### Complexity
> `TC: O(n). SC: O(k), k number of distinct characters.`

### Code

> **Java**

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()){
            return false;
    }

    Map<Character, Integer> count = new HashMap<>();
    for (int i = 0; i < s.length(); i++) {
        count.merge(s.charAt(i), 1, Integer::sum);
        count.merge(t.charAt(i), -1, Integer::sum); 
    }

    for (int val : count.values()) {
        if (val != 0){
                return false;
        }
    }

    return true;
}
```

> **Python**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        count = {}
        for i in range(len(s)):
            cs, ct = s[i], t[i]
            count[cs] = count.get(cs, 0) + 1
            count[ct] = count.get(ct, 0) - 1

        for val in count.values():
            if val != 0:
                return False

        return True
```

## Solution 3: Two H**Python**ashMap
### Complexity
> `TC: O(n). SC: O(k), k := number of distinct characters.`

### Code

> **Java**

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()){
        return false;
    }

    Map<Character,Integer> countsI = new HashMap<>();
    Map<Character,Integer> countsJ = new HashMap<>();
    for (int i=0; i<s.length(); i++){
        countsI.put(s.charAt(i), countsI.getOrDefault(s.charAt(i), 0) + 1);
        countsJ.put(t.charAt(i), countsJ.getOrDefault(t.charAt(i), 0) + 1);
    }

    return countsI.equals(countsJ);
}
```

> **Python**

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        countsI = {}
        countsJ = {}
        for i in range(len(s)):
            countsI[s[i]] = countsI.get(s[i], 0) + 1
            countsJ[t[i]] = countsJ.get(t[i], 0) + 1

        return countsI == countsJ
```