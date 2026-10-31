# DSA: Arrays and Hashing

<details><summary>

## 7. Two sum
</summary>

**Example:** `nums = [2, 7, 11, 15], target = 9` → `[0, 1]`

**Practice:** [LeetCode 1](https://leetcode.com/problems/two-sum/)

**Approach:** for each number, check whether `target - num` was seen before.

```java
int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> seen = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        Integer j = seen.get(target - nums[i]);
        if (j != null) return new int[]{j, i};
        seen.put(nums[i], i);
    }
    return new int[0];
}
```

**Complexity:** O(n) time, O(n) space.
</details>

<details><summary>

## 8. Best time to buy and sell stock (I and II)
</summary>

**Example:** `[7, 1, 5, 3, 6, 4]` → I: `5` (buy 1, sell 6); II: `7` (1→5, 3→6)

**Practice:** [LeetCode 121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/), [LeetCode 122](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

```java
// I: one transaction - track the lowest price so far
int maxProfitOne(int[] p) {
    int min = Integer.MAX_VALUE, best = 0;
    for (int x : p) { min = Math.min(min, x); best = Math.max(best, x - min); }
    return best;
}

// II: unlimited transactions - collect every upward step
int maxProfitMany(int[] p) {
    int profit = 0;
    for (int i = 1; i < p.length; i++) if (p[i] > p[i - 1]) profit += p[i] - p[i - 1];
    return profit;
}
```

**Complexity:** both O(n) time, O(1) space.
</details>

<details><summary>

## 9. Maximum subarray sum (Kadane's algorithm)
</summary>

**Example:** `[-2, 1, -3, 4, -1, 2, 1, -5, 4]` → `6` (subarray `[4, -1, 2, 1]`)

**Practice:** [LeetCode 53](https://leetcode.com/problems/maximum-subarray/)

```java
int maxSubArray(int[] a) {
    int cur = a[0], best = a[0];
    for (int i = 1; i < a.length; i++) {
        cur = Math.max(a[i], cur + a[i]);   // extend or start fresh
        best = Math.max(best, cur);
    }
    return best;
}
```

**Complexity:** O(n) time, O(1) space. Starting from `a[0]` handles all-negative arrays.
</details>

<details><summary>

## 10. Merge overlapping intervals
</summary>

**Example:** `[[1,3],[2,6],[8,10],[15,18]]` → `[[1,6],[8,10],[15,18]]`

**Practice:** [LeetCode 56](https://leetcode.com/problems/merge-intervals/)

```java
int[][] merge(int[][] iv) {
    Arrays.sort(iv, (x, y) -> Integer.compare(x[0], y[0]));
    List<int[]> out = new ArrayList<>();
    for (int[] cur : iv) {
        if (out.isEmpty() || out.get(out.size() - 1)[1] < cur[0]) out.add(cur);
        else out.get(out.size() - 1)[1] = Math.max(out.get(out.size() - 1)[1], cur[1]);
    }
    return out.toArray(new int[0][]);
}
```

**Complexity:** O(n log n) for the sort.
</details>

<details><summary>

## 11. Product of array except self (no division)
</summary>

**Example:** `[1, 2, 3, 4]` → `[24, 12, 8, 6]`

**Practice:** [LeetCode 238](https://leetcode.com/problems/product-of-array-except-self/)

```java
int[] productExceptSelf(int[] a) {
    int n = a.length;
    int[] res = new int[n];
    res[0] = 1;
    for (int i = 1; i < n; i++) res[i] = res[i - 1] * a[i - 1];   // product of left side
    int right = 1;
    for (int i = n - 1; i >= 0; i--) { res[i] *= right; right *= a[i]; } // times right side
    return res;
}
```

**Complexity:** O(n) time, O(1) extra space besides the output.
</details>

<details><summary>

## 12. Subarray sum equals K
</summary>

**Example:** `nums = [1, 2, 3], k = 3` → `2` (`[1,2]` and `[3]`); `nums = [1, -1, 0], k = 0` → `3`

**Practice:** [LeetCode 560](https://leetcode.com/problems/subarray-sum-equals-k/)

**Approach:** prefix sums. If `prefix - k` was seen c times, c subarrays end here.

```java
int subarraySum(int[] a, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    count.put(0, 1);
    int sum = 0, res = 0;
    for (int x : a) {
        sum += x;
        res += count.getOrDefault(sum - k, 0);
        count.merge(sum, 1, Integer::sum);
    }
    return res;
}
```

**Complexity:** O(n) time, O(n) space. A sliding window fails here because numbers can be negative.
</details>
