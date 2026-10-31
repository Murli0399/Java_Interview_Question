# DSA: Trees and Binary Search

Assume:

```java
class TreeNode { int val; TreeNode left, right; TreeNode(int v) { val = v; } }
```

<details><summary>

## 18. Level order traversal (BFS)
</summary>

**Example:** tree `[3, 9, 20, null, null, 15, 7]` → `[[3], [9, 20], [15, 7]]`

**Practice:** [LeetCode 102](https://leetcode.com/problems/binary-tree-level-order-traversal/)

```java
List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;
    Queue<TreeNode> q = new ArrayDeque<>();
    q.add(root);
    while (!q.isEmpty()) {
        List<Integer> level = new ArrayList<>();
        for (int k = q.size(); k > 0; k--) {     // process one level at a time
            TreeNode n = q.poll();
            level.add(n.val);
            if (n.left != null) q.add(n.left);
            if (n.right != null) q.add(n.right);
        }
        res.add(level);
    }
    return res;
}
```

**Complexity:** O(n) time, O(n) space.
</details>

<details><summary>

## 19. Lowest common ancestor of a binary tree
</summary>

**Example:** tree `[3,5,1,6,2,0,8,null,null,7,4]`, p = 5, q = 1 → `3`; p = 5, q = 4 → `5`

**Practice:** [LeetCode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

```java
TreeNode lca(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode l = lca(root.left, p, q), r = lca(root.right, p, q);
    if (l != null && r != null) return root;   // p and q on different sides
    return l != null ? l : r;
}
```

**Complexity:** O(n) time, O(h) recursion space. For a BST, walk down by comparing values in O(h).
</details>

<details><summary>

## 20. Search in a rotated sorted array
</summary>

**Example:** `nums = [4,5,6,7,0,1,2], target = 0` → `4`; `target = 3` → `-1`

**Practice:** [LeetCode 33](https://leetcode.com/problems/search-in-rotated-sorted-array/)

**Approach:** binary search; one half is always sorted, so check whether the target lies in it.

```java
int search(int[] a, int t) {
    int lo = 0, hi = a.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;            // avoids int overflow
        if (a[mid] == t) return mid;
        if (a[lo] <= a[mid]) {                   // left half sorted
            if (a[lo] <= t && t < a[mid]) hi = mid - 1; else lo = mid + 1;
        } else {                                 // right half sorted
            if (a[mid] < t && t <= a[hi]) lo = mid + 1; else hi = mid - 1;
        }
    }
    return -1;
}
```

**Complexity:** O(log n).
</details>

<details><summary>

## Before you say "done" in an interview
</summary>

- Empty input, one element, all duplicates, negative numbers
- Integer overflow on sums or the binary-search midpoint
- Dry-run a small example out loud, line by line
- State time and space complexity
</details>
