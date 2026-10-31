# Classic Java Programs

Short programs that often open a Java interview round. Write them without an IDE.

<details><summary>

## Reverse a string without using reverse()
</summary>

**Example:** `"tracxn"` → `"nxcart"`

```java
String reverse(String s) {
    char[] c = s.toCharArray();
    for (int i = 0, j = c.length - 1; i < j; i++, j--) {
        char t = c[i]; c[i] = c[j]; c[j] = t;
    }
    return new String(c);
}
```
</details>

<details><summary>

## Check whether a number is prime
</summary>

**Example:** `29` → `true`; `21` → `false`

```java
boolean isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; (long) i * i <= n; i++) if (n % i == 0) return false;
    return true;
}
```

Only check up to √n. For many numbers, use the Sieve of Eratosthenes.
</details>

<details><summary>

## Fibonacci series (iterative and memoised)
</summary>

**Example:** first 8 → `0 1 1 2 3 5 8 13`

```java
long fib(int n) {                 // iterative, O(n) time, O(1) space
    long a = 0, b = 1;
    for (int i = 0; i < n; i++) { long t = a + b; a = b; b = t; }
    return a;
}

Map<Integer, Long> memo = new HashMap<>();
long fibMemo(int n) {             // naive recursion is O(2^n); memo makes it O(n)
    if (n < 2) return n;
    Long cached = memo.get(n);
    if (cached != null) return cached;
    long v = fibMemo(n - 1) + fibMemo(n - 2);
    memo.put(n, v);
    return v;
}
```
</details>

<details><summary>

## Check whether two strings are anagrams
</summary>

**Example:** `"listen", "silent"` → `true`

```java
boolean isAnagram(String a, String b) {
    if (a.length() != b.length()) return false;
    int[] count = new int[26];
    for (int i = 0; i < a.length(); i++) {
        count[a.charAt(i) - 'a']++;
        count[b.charAt(i) - 'a']--;
    }
    for (int c : count) if (c != 0) return false;
    return true;
}
```
</details>

<details><summary>

## Find the missing number in 1..n
</summary>

**Example:** `[1, 2, 4, 5]` (n = 5) → `3`

```java
int missing(int[] a, int n) {
    int xor = 0;
    for (int i = 1; i <= n; i++) xor ^= i;
    for (int x : a) xor ^= x;
    return xor;   // XOR avoids overflow that n*(n+1)/2 can hit
}
```
</details>

<details><summary>

## Move all zeros to the end, keeping order
</summary>

**Example:** `[0, 1, 0, 3, 12]` → `[1, 3, 12, 0, 0]` · [LeetCode 283](https://leetcode.com/problems/move-zeroes/)

```java
void moveZeroes(int[] a) {
    int w = 0;
    for (int x : a) if (x != 0) a[w++] = x;
    while (w < a.length) a[w++] = 0;
}
```
</details>

<details><summary>

## Remove duplicates from a sorted array in place
</summary>

**Example:** `[1, 1, 2, 3, 3]` → length `3`, array starts `[1, 2, 3]` · [LeetCode 26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

```java
int removeDuplicates(int[] a) {
    if (a.length == 0) return 0;
    int w = 1;
    for (int i = 1; i < a.length; i++) if (a[i] != a[w - 1]) a[w++] = a[i];
    return w;
}
```
</details>

<details><summary>

## Print a pattern (Floyd's triangle)
</summary>

Reported in Tracxn written rounds.

```text
1
2 3
4 5 6
7 8 9 10
```

```java
void floyd(int rows) {
    int n = 1;
    for (int i = 1; i <= rows; i++) {
        StringBuilder line = new StringBuilder();
        for (int j = 1; j <= i; j++) line.append(n++).append(' ');
        System.out.println(line.toString().trim());
    }
}
```
</details>

<details><summary>

## FizzBuzz
</summary>

```java
for (int i = 1; i <= 15; i++) {
    System.out.println(i % 15 == 0 ? "FizzBuzz" : i % 3 == 0 ? "Fizz" : i % 5 == 0 ? "Buzz" : String.valueOf(i));
}
```
</details>
