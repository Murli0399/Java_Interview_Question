# DSA: Linked Lists, Matrix and Stack

Assume:

```java
class ListNode { int val; ListNode next; ListNode() {} ListNode(int v) { val = v; } }
```

<details><summary>

## 13. Reverse a linked list
</summary>

**Example:** `1 → 2 → 3 → 4 → null` → `4 → 3 → 2 → 1 → null`

**Practice:** [LeetCode 206](https://leetcode.com/problems/reverse-linked-list/)

```java
ListNode reverse(ListNode head) {
    ListNode prev = null, cur = head;
    while (cur != null) {
        ListNode next = cur.next;
        cur.next = prev;
        prev = cur;
        cur = next;
    }
    return prev;
}
```

**Complexity:** O(n) time, O(1) space. Be ready to write the recursive version too.
</details>

<details><summary>

## 14. Detect a cycle and return where it starts
</summary>

**Example:** `3 → 2 → 0 → -4 → (back to 2)` → node with value `2`

**Practice:** [LeetCode 142](https://leetcode.com/problems/linked-list-cycle-ii/)

**Approach:** Floyd's slow/fast pointers. After they meet, reset one to head and move both one step; they meet at the cycle start.

```java
ListNode cycleStart(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) {
            slow = head;
            while (slow != fast) { slow = slow.next; fast = fast.next; }
            return slow;
        }
    }
    return null;
}
```

**Complexity:** O(n) time, O(1) space.
</details>

<details><summary>

## 15. Merge two sorted lists
</summary>

**Example:** `1 → 2 → 4` and `1 → 3 → 4` → `1 → 1 → 2 → 3 → 4 → 4`

**Practice:** [LeetCode 21](https://leetcode.com/problems/merge-two-sorted-lists/)

```java
ListNode merge(ListNode a, ListNode b) {
    ListNode dummy = new ListNode(), tail = dummy;
    while (a != null && b != null) {
        if (a.val <= b.val) { tail.next = a; a = a.next; }
        else { tail.next = b; b = b.next; }
        tail = tail.next;
    }
    tail.next = (a != null) ? a : b;
    return dummy.next;
}
```

**Complexity:** O(n + m) time, O(1) space.
</details>

<details><summary>

## 16. Word search in a matrix
</summary>

**Example:** board `[["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]]`, word `"ABCCED"` → `true`; `"ABCB"` → `false`

**Practice:** [LeetCode 79](https://leetcode.com/problems/word-search/)

**Approach:** DFS from every cell with backtracking; mark a cell visited, then restore it.

```java
boolean exist(char[][] b, String word) {
    for (int r = 0; r < b.length; r++)
        for (int c = 0; c < b[0].length; c++)
            if (dfs(b, word, r, c, 0)) return true;
    return false;
}

boolean dfs(char[][] b, String w, int r, int c, int i) {
    if (i == w.length()) return true;
    if (r < 0 || c < 0 || r >= b.length || c >= b[0].length || b[r][c] != w.charAt(i)) return false;
    char tmp = b[r][c];
    b[r][c] = '#';
    boolean found = dfs(b, w, r + 1, c, i + 1) || dfs(b, w, r - 1, c, i + 1)
                 || dfs(b, w, r, c + 1, i + 1) || dfs(b, w, r, c - 1, i + 1);
    b[r][c] = tmp;
    return found;
}
```

**Complexity:** O(R · C · 4^L) time for word length L, O(L) recursion space.
</details>

<details><summary>

## 17. Valid parentheses
</summary>

**Example:** `"()[]{}"` → `true`; `"(]"` → `false`; `"([)]"` → `false`

**Practice:** [LeetCode 20](https://leetcode.com/problems/valid-parentheses/)

```java
boolean isValid(String s) {
    Deque<Character> st = new ArrayDeque<>();
    for (char ch : s.toCharArray()) {
        if (ch == '(') st.push(')');
        else if (ch == '[') st.push(']');
        else if (ch == '{') st.push('}');
        else if (st.isEmpty() || st.pop() != ch) return false;
    }
    return st.isEmpty();
}
```

**Complexity:** O(n) time, O(n) space. Use `ArrayDeque`, not the legacy synchronized `Stack` class.
</details>
