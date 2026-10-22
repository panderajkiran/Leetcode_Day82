# Leetcode_Day82
# Day 82: The K Weakest Rows in a Matrix

**LeetCode Problem:** [1337. The K Weakest Rows in a Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/)  
**Difficulty:** Easy  
**Language:** Java  
**Topics:** Binary Search, Sorting, Arrays

## Problem Description

You are given an `m x n` binary matrix where `1` represents a soldier and `0` represents a civilian.

All soldiers appear before civilians in each row.

A row is considered weaker if it has fewer soldiers. If two rows have the same number of soldiers, the row with the smaller index is weaker.

Return the indices of the `k` weakest rows, ordered from weakest to strongest.

## Approach

### 1. Count Soldiers Using Binary Search

Since all the `1`s appear before the `0`s in each row, we can use binary search to find the number of soldiers efficiently.

- Initialize `low = 0` and `high = n - 1`.
- Calculate the middle index.
- If `mat[i][mid] == 1`, move `low` to `mid + 1`.
- Otherwise, move `high` to `mid - 1`.
- When the search ends, `low` represents the number of soldiers in that row.

### 2. Store Row Information

Create a two-dimensional array to store:
- The number of soldiers in each row.
- The index of each row.

### 3. Sort the Rows

Sort the rows using two conditions:

1. Sort by the number of soldiers in ascending order.
2. If two rows have the same number of soldiers, sort by their indices in ascending order.

### 4. Return the Answer

Create an array of size `k` and store the indices of the first `k` rows after sorting.

## Java Solution

```java
import java.util.Arrays;

class Solution {
    public int[] kWeakestRows(int[][] mat, int k) {
        int m = mat.length;
        int n = mat[0].length;

        int[][] rows = new int[m][2];

        for (int i = 0; i < m; i++) {
            int low = 0;
            int high = n - 1;

            while (low <= high) {
                int mid = low + (high - low) / 2;

                if (mat[i][mid] == 1) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }

            rows[i][0] = low;
            rows[i][1] = i;
        }

        Arrays.sort(rows, (a, b) -> {
            if (a[0] != b[0]) {
                return a[0] - b[0];
            }
            return a[1] - b[1];
        });

        int[] ans = new int[k];

        for (int i = 0; i < k; i++) {
            ans[i] = rows[i][1];
        }

        return ans;
    }
}
```

## Example

**Input:**
```text
mat = [[1,1,0,0,0],
       [1,1,1,1,0],
       [1,0,0,0,0],
       [1,1,0,0,0],
       [1,1,1,1,1]]
k = 3
```

**Output:**
```text
[2, 0, 3]
```

**Explanation:**

- Row 2 has 1 soldier.
- Row 0 has 2 soldiers.
- Row 3 has 2 soldiers.

Rows 0 and 3 have the same number of soldiers, so row 0 comes first because its index is smaller.

Therefore, the three weakest rows are `[2, 0, 3]`.

## Complexity Analysis

Let:
- `m` = number of rows.
- `n` = number of columns.

**Time Complexity:** `O(m log n + m log m)`

- Binary search in every row takes `O(m log n)`.
- Sorting the row information takes `O(m log m)`.

**Space Complexity:** `O(m)`

We use a two-dimensional array to store the soldier counts and row indices.

## What I Learned

- How to apply binary search to count soldiers in a sorted binary row.
- How to sort two-dimensional arrays using a custom comparator.
- How to handle tie-breaking conditions during sorting.
- How combining binary search and sorting can make a solution more efficient.

## Takeaway

**A problem becomes easier when we break it into smaller tasks and choose the right technique for each task.**

Day 82 complete! One more problem solved, one more concept learned, and one more step forward in my DSA journey.
