# DSA: Medium and Hard Problems

Patterns that show up once the easy rounds are done: heaps, two pointers, graphs, dynamic programming and advanced sliding windows.

<details><summary>

## [Medium] 21. Top K frequent elements
</summary>

**Example:** `nums = [1,1,1,2,2,3], k = 2` → `[1, 2]`

**Practice:** [LeetCode 347](https://leetcode.com/problems/top-k-frequent-elements/)

**Approach:** count with a HashMap, then keep a **min-heap of size k** ordered by frequency.

```java
int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.merge(n, 1, Integer::sum);
    PriorityQueue<Map.Entry<Integer, Integer>> heap =
        new PriorityQueue<>(Comparator.comparingInt(Map.Entry::getValue));
    for (Map.Entry<Integer, Integer> e : freq.entrySet()) {
        heap.offer(e);
        if (heap.size() > k) heap.poll();          // drop the least frequent
    }
    int[] res = new int[k];
    for (int i = k - 1; i >= 0; i--) res[i] = heap.poll().getKey();
    return res;
}
```

**Complexity:** O(n log k) time, O(n) space. Follow-up: bucket sort by frequency gives O(n).
</details>

<details><summary>

## [Medium] 22. Kth largest element in an array
</summary>

**Example:** `[3,2,1,5,6,4], k = 2` → `5`

**Practice:** [LeetCode 215](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```java
int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for (int n : nums) {
        minHeap.offer(n);
        if (minHeap.size() > k) minHeap.poll();
    }
    return minHeap.peek();                         // smallest of the k largest
}
```

**Complexity:** O(n log k). Follow-up: Quickselect gives O(n) on average.
</details>

<details><summary>

## [Medium] 23. Longest consecutive sequence
</summary>

**Example:** `[100, 4, 200, 1, 3, 2]` → `4` (1, 2, 3, 4)

**Practice:** [LeetCode 128](https://leetcode.com/problems/longest-consecutive-sequence/)

**Approach:** put everything in a HashSet; only start counting from numbers that begin a sequence (`n - 1` not in the set).

```java
int longestConsecutive(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int n : nums) set.add(n);
    int best = 0;
    for (int n : set) {
        if (set.contains(n - 1)) continue;         // not a sequence start
        int len = 1;
        while (set.contains(n + len)) len++;
        best = Math.max(best, len);
    }
    return best;
}
```

**Complexity:** O(n) time, O(n) space (each number is visited at most twice).
</details>

<details><summary>

## [Medium] 24. Three sum
</summary>

**Example:** `[-1, 0, 1, 2, -1, -4]` → `[[-1, -1, 2], [-1, 0, 1]]`

**Practice:** [LeetCode 15](https://leetcode.com/problems/3sum/)

**Approach:** sort, fix one number, and find the other two with **two pointers**; skip duplicates.

```java
List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> res = new ArrayList<>();
    for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int l = i + 1, r = nums.length - 1;
        while (l < r) {
            int sum = nums[i] + nums[l] + nums[r];
            if (sum < 0) l++;
            else if (sum > 0) r--;
            else {
                res.add(List.of(nums[i], nums[l], nums[r]));
                while (l < r && nums[l] == nums[l + 1]) l++;
                while (l < r && nums[r] == nums[r - 1]) r--;
                l++; r--;
            }
        }
    }
    return res;
}
```

**Complexity:** O(n²) time, O(1) extra space besides the output.
</details>

<details><summary>

## [Medium] 25. Container with most water
</summary>

**Example:** `[1,8,6,2,5,4,8,3,7]` → `49`

**Practice:** [LeetCode 11](https://leetcode.com/problems/container-with-most-water/)

**Approach:** two pointers at both ends; always move the **shorter** wall inward, because moving the taller one can't increase the area.

```java
int maxArea(int[] h) {
    int l = 0, r = h.length - 1, best = 0;
    while (l < r) {
        best = Math.max(best, Math.min(h[l], h[r]) * (r - l));
        if (h[l] < h[r]) l++; else r--;
    }
    return best;
}
```

**Complexity:** O(n) time, O(1) space.
</details>

<details><summary>

## [Medium] 26. Number of islands
</summary>

**Example:**
```text
1 1 0 0 0
1 1 0 0 0
0 0 1 0 0
0 0 0 1 1      → 3 islands
```

**Practice:** [LeetCode 200](https://leetcode.com/problems/number-of-islands/)

**Approach:** scan the grid; on each unvisited `'1'`, count an island and flood-fill (DFS) its connected land to mark it visited.

```java
int numIslands(char[][] grid) {
    int count = 0;
    for (int r = 0; r < grid.length; r++)
        for (int c = 0; c < grid[0].length; c++)
            if (grid[r][c] == '1') { count++; sink(grid, r, c); }
    return count;
}

void sink(char[][] g, int r, int c) {
    if (r < 0 || c < 0 || r >= g.length || c >= g[0].length || g[r][c] != '1') return;
    g[r][c] = '0';
    sink(g, r + 1, c); sink(g, r - 1, c); sink(g, r, c + 1); sink(g, r, c - 1);
}
```

**Complexity:** O(R·C) time; recursion depth up to R·C (use BFS with a queue for very large grids).
</details>

<details><summary>

## [Medium] 27. Course schedule (cycle detection / topological sort)
</summary>

**Example:** `numCourses = 2, prerequisites = [[1,0]]` → `true`; `[[1,0],[0,1]]` → `false` (cycle)

**Practice:** [LeetCode 207](https://leetcode.com/problems/course-schedule/)

**Approach:** Kahn's algorithm. Count incoming edges (in-degree); repeatedly take courses with in-degree 0. If all courses get taken, there's no cycle.

```java
boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> graph = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
    int[] indegree = new int[numCourses];
    for (int[] p : prerequisites) { graph.get(p[1]).add(p[0]); indegree[p[0]]++; }

    Deque<Integer> queue = new ArrayDeque<>();
    for (int i = 0; i < numCourses; i++) if (indegree[i] == 0) queue.add(i);
    int taken = 0;
    while (!queue.isEmpty()) {
        int course = queue.poll();
        taken++;
        for (int next : graph.get(course)) if (--indegree[next] == 0) queue.add(next);
    }
    return taken == numCourses;
}
```

**Complexity:** O(V + E). The same idea orders build steps, task dependencies or microservice startup.
</details>

<details><summary>

## [Medium] 28. Coin change (dynamic programming)
</summary>

**Example:** `coins = [1, 2, 5], amount = 11` → `3` (5 + 5 + 1); `coins = [2], amount = 3` → `-1`

**Practice:** [LeetCode 322](https://leetcode.com/problems/coin-change/)

**Approach:** `dp[a]` = fewest coins to make amount `a`. For each amount, try every coin: `dp[a] = min(dp[a], dp[a - coin] + 1)`.

```java
int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);                   // "infinity"
    dp[0] = 0;
    for (int a = 1; a <= amount; a++)
        for (int coin : coins)
            if (coin <= a) dp[a] = Math.min(dp[a], dp[a - coin] + 1);
    return dp[amount] > amount ? -1 : dp[amount];
}
```

**Complexity:** O(amount × coins) time, O(amount) space. Greedy (take the largest coin first) fails for coins like `[1, 3, 4]` and amount 6.
</details>

<details><summary>

## [Medium] 29. Validate a binary search tree
</summary>

**Example:** `[2,1,3]` → `true`; `[5,1,4,null,null,3,6]` → `false` (3 is in 5's right subtree)

**Practice:** [LeetCode 98](https://leetcode.com/problems/validate-binary-search-tree/)

**Approach:** pass down the allowed range; every node must be strictly within (low, high). Checking only parent vs child is the common mistake.

```java
boolean isValidBST(TreeNode root) {
    return valid(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

boolean valid(TreeNode n, long low, long high) {
    if (n == null) return true;
    if (n.val <= low || n.val >= high) return false;
    return valid(n.left, low, n.val) && valid(n.right, n.val, high);
}
```

**Complexity:** O(n) time, O(h) space. `long` bounds handle nodes equal to `Integer.MIN_VALUE/MAX_VALUE`.
</details>

<details><summary>

## [Hard] 30. Trapping rain water
</summary>

**Example:** `[0,1,0,2,1,0,1,3,2,1,2,1]` → `6`

**Practice:** [LeetCode 42](https://leetcode.com/problems/trapping-rain-water/)

**Approach:** water above a bar = `min(maxLeft, maxRight) - height`. With two pointers, the side with the smaller max is already determined, so process it and move inward.

```java
int trap(int[] h) {
    int l = 0, r = h.length - 1, leftMax = 0, rightMax = 0, water = 0;
    while (l < r) {
        if (h[l] < h[r]) {
            leftMax = Math.max(leftMax, h[l]);
            water += leftMax - h[l];
            l++;
        } else {
            rightMax = Math.max(rightMax, h[r]);
            water += rightMax - h[r];
            r--;
        }
    }
    return water;
}
```

**Complexity:** O(n) time, O(1) space.
</details>

<details><summary>

## [Hard] 31. Merge k sorted lists
</summary>

**Example:** `[1→4→5, 1→3→4, 2→6]` → `1→1→2→3→4→4→5→6`

**Practice:** [LeetCode 23](https://leetcode.com/problems/merge-k-sorted-lists/)

**Approach:** a min-heap holding the current head of each list; repeatedly take the smallest and push its successor.

```java
ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> heap = new PriorityQueue<>(Comparator.comparingInt(n -> n.val));
    for (ListNode head : lists) if (head != null) heap.offer(head);
    ListNode dummy = new ListNode(), tail = dummy;
    while (!heap.isEmpty()) {
        ListNode node = heap.poll();
        tail.next = node;
        tail = node;
        if (node.next != null) heap.offer(node.next);
    }
    return dummy.next;
}
```

**Complexity:** O(N log k) for N total nodes and k lists. This is the same idea as merging sorted files or Kafka partitions by timestamp.
</details>

<details><summary>

## [Hard] 32. Sliding window maximum
</summary>

**Example:** `nums = [1,3,-1,-3,5,3,6,7], k = 3` → `[3,3,5,5,6,7]`

**Practice:** [LeetCode 239](https://leetcode.com/problems/sliding-window-maximum/)

**Approach:** a **monotonic deque** of indices whose values are decreasing; the front is always the window's max. Drop indices that leave the window, and pop smaller values from the back before adding a new one.

```java
int[] maxSlidingWindow(int[] nums, int k) {
    int[] res = new int[nums.length - k + 1];
    Deque<Integer> dq = new ArrayDeque<>();        // indices, values decreasing
    for (int i = 0; i < nums.length; i++) {
        if (!dq.isEmpty() && dq.peekFirst() <= i - k) dq.pollFirst();       // out of window
        while (!dq.isEmpty() && nums[dq.peekLast()] <= nums[i]) dq.pollLast();
        dq.offerLast(i);
        if (i >= k - 1) res[i - k + 1] = nums[dq.peekFirst()];
    }
    return res;
}
```

**Complexity:** O(n) time (each index is added and removed once), O(k) space.
</details>

<details><summary>

## [Hard] 33. Minimum window substring
</summary>

**Example:** `s = "ADOBECODEBANC", t = "ABC"` → `"BANC"`

**Practice:** [LeetCode 76](https://leetcode.com/problems/minimum-window-substring/)

**Approach:** expand the right edge until the window contains all of `t`, then shrink from the left while it still does, tracking the smallest valid window.

```java
String minWindow(String s, String t) {
    int[] need = new int[128];
    for (char c : t.toCharArray()) need[c]++;
    int missing = t.length(), start = 0, bestLen = Integer.MAX_VALUE;
    for (int l = 0, r = 0; r < s.length(); r++) {
        if (need[s.charAt(r)]-- > 0) missing--;
        while (missing == 0) {                      // window is valid: try to shrink
            if (r - l + 1 < bestLen) { bestLen = r - l + 1; start = l; }
            if (++need[s.charAt(l++)] > 0) missing++;
        }
    }
    return bestLen == Integer.MAX_VALUE ? "" : s.substring(start, start + bestLen);
}
```

**Complexity:** O(|s| + |t|) time, O(1) space (fixed 128-char table).
</details>
