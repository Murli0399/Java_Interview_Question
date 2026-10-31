# DSA: Strings

Try each on paper (20–30 min) before opening the solution. Say brute force first, then optimise, then dry-run.

<details><summary>

## 1. Check whether a pattern exists in a text (substring search)
</summary>

**Example:** `text = "tracxn", pattern = "acx"` → `true`; `text = "abcdef", pattern = "acf"` → `false`

**Practice:** [LeetCode 28](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

**Brute force:** try every start position, O(n·m). **Optimised (KMP):** precompute the LPS array (longest proper prefix that is also a suffix) so the text pointer never moves back.

```java
boolean contains(String text, String pat) {
    int n = text.length(), m = pat.length();
    if (m == 0) return true;
    int[] lps = new int[m];
    for (int i = 1, len = 0; i < m; ) {
        if (pat.charAt(i) == pat.charAt(len)) lps[i++] = ++len;
        else if (len > 0) len = lps[len - 1];
        else lps[i++] = 0;
    }
    for (int i = 0, j = 0; i < n; ) {
        if (text.charAt(i) == pat.charAt(j)) {
            i++; j++;
            if (j == m) return true;
        } else if (j > 0) j = lps[j - 1];
        else i++;
    }
    return false;
}
```

**Complexity:** O(n + m) time, O(m) space.
</details>

<details><summary>

## 2. Valid palindrome (ignore case and non-alphanumerics)
</summary>

**Example:** `"A man, a plan, a canal: Panama"` → `true`; `"race a car"` → `false`

**Practice:** [LeetCode 125](https://leetcode.com/problems/valid-palindrome/)

```java
boolean isPalindrome(String s) {
    int l = 0, r = s.length() - 1;
    while (l < r) {
        while (l < r && !Character.isLetterOrDigit(s.charAt(l))) l++;
        while (l < r && !Character.isLetterOrDigit(s.charAt(r))) r--;
        if (Character.toLowerCase(s.charAt(l)) != Character.toLowerCase(s.charAt(r))) return false;
        l++; r--;
    }
    return true;
}
```

**Complexity:** O(n) time, O(1) space.
</details>

<details><summary>

## 3. Longest palindromic substring
</summary>

**Example:** `"babad"` → `"bab"` (or `"aba"`); `"cbbd"` → `"bb"`

**Practice:** [LeetCode 5](https://leetcode.com/problems/longest-palindromic-substring/)

**Approach:** every palindrome has a centre; expand around each of the 2n−1 centres (a character, or the gap between two).

```java
String longestPalindrome(String s) {
    int start = 0, best = 0;
    for (int i = 0; i < s.length(); i++) {
        int len = Math.max(expand(s, i, i), expand(s, i, i + 1));
        if (len > best) { best = len; start = i - (len - 1) / 2; }
    }
    return s.substring(start, start + best);
}

int expand(String s, int l, int r) {
    while (l >= 0 && r < s.length() && s.charAt(l) == s.charAt(r)) { l--; r++; }
    return r - l - 1;
}
```

**Complexity:** O(n²) time, O(1) space.
</details>

<details><summary>

## 4. Longest substring without repeating characters
</summary>

**Example:** `"abcabcbb"` → `3` ("abc"); `"pwwkew"` → `3` ("wke")

**Practice:** [LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

**Approach:** sliding window; remember each character's last index and jump the left edge past a repeat.

```java
int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> last = new HashMap<>();
    int best = 0;
    for (int l = 0, r = 0; r < s.length(); r++) {
        char c = s.charAt(r);
        if (last.containsKey(c)) l = Math.max(l, last.get(c) + 1);
        last.put(c, r);
        best = Math.max(best, r - l + 1);
    }
    return best;
}
```

**Complexity:** O(n) time, O(k) space for k distinct characters.
</details>

<details><summary>

## 5. Group anagrams
</summary>

**Example:** `["eat","tea","tan","ate","nat","bat"]` → `[["eat","tea","ate"],["tan","nat"],["bat"]]`

**Practice:** [LeetCode 49](https://leetcode.com/problems/group-anagrams/)

```java
List<List<String>> groupAnagrams(String[] words) {
    Map<String, List<String>> groups = new HashMap<>();
    for (String w : words) {
        char[] c = w.toCharArray();
        Arrays.sort(c);
        groups.computeIfAbsent(new String(c), k -> new ArrayList<>()).add(w);
    }
    return new ArrayList<>(groups.values());
}
```

**Complexity:** O(n · k log k) for n words of length k. Follow-up: a 26-count array key makes it O(n · k).
</details>

<details><summary>

## 6. String compression
</summary>

**Example:** `"aabcccccaaa"` → `"a2b1c5a3"`; `"abc"` → `"abc"` (compressed isn't shorter)

**Practice:** [LeetCode 443](https://leetcode.com/problems/string-compression/) (in-place variant)

```java
String compress(String s) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < s.length(); ) {
        int j = i;
        while (j < s.length() && s.charAt(j) == s.charAt(i)) j++;
        sb.append(s.charAt(i)).append(j - i);
        i = j;
    }
    return sb.length() < s.length() ? sb.toString() : s;
}
```

**Complexity:** O(n) time, O(n) space. Use `StringBuilder`, never `+` in a loop (Strings are immutable).
</details>
