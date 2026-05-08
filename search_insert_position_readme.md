# Search Insert Position

## Problem Statement

Given a sorted array of distinct integers and a target value, return the index if the target is found.

If not found, return the index where it would be inserted in order.

---

# Example 1

```java
Input:
nums = [1,3,5,6]
target = 5
```

Output:

```java
2
```

Because target `5` is present at index `2`.

---

# Example 2

```java
Input:
nums = [1,3,5,6]
target = 2
```

Output:

```java
1
```

Because `2` should be inserted at index `1`.

---

# Example 3

```java
Input:
nums = [1,3,5,6]
target = 7
```

Output:

```java
4
```

Because `7` should be inserted at the end.

---

# Brute Force Approach

Traverse the array:

- If current element is greater than or equal to target
- Return current index

Otherwise return `n`.

---

# Brute Force Code

```java
class Solution {

    public int searchInsert(int[] nums, int target) {

        int n = nums.length;

        for (int i = 0; i < n; i++) {

            if (nums[i] >= target) {
                return i;
            }
        }

        return n;
    }
}
```

---

# Time Complexity

```java
O(n)
```

---

# Optimal Approach (Binary Search)

Since array is sorted, Binary Search can be used.

Idea:

- If target found → return index
- Else find first position where:

```java
nums[i] >= target
```

That position becomes insertion index.

---

# Binary Search Idea

Take:

```java
low = 0
high = n - 1
```

Find middle:

```java
mid = low + (high - low) / 2
```

---

# Dry Run

## Input

```java
nums = [1,3,5,6]
target = 2
```

Initial:

```java
low = 0
high = 3
ans = 4
```

---

# Step 1

Find mid:

```java
mid = 0 + (3-0)/2
mid = 1
```

```java
nums[mid] = 3
```

Since:

```java
3 >= 2
```

Possible answer found.

```java
ans = 1
```

Move left:

```java
high = mid - 1
high = 0
```

---

# Step 2

Now:

```java
low = 0
high = 0
```

Find mid:

```java
mid = 0
```

```java
nums[mid] = 1
```

Since:

```java
1 < 2
```

Move right:

```java
low = mid + 1
low = 1
```

---

Loop ends.

Return:

```java
1
```

---

# Optimal Code

```java
class Solution {

    public int searchInsert(int[] nums, int target) {

        int n = nums.length;

        int low = 0;
        int high = n - 1;

        int ans = n;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] >= target) {

                ans = mid;
                high = mid - 1;
            }

            else {

                low = mid + 1;
            }
        }

        return ans;
    }
}
```

---

# Complexity Analysis

## Time Complexity

```java
O(log n)
```

## Space Complexity

```java
O(1)
```

---

# Important Observation

Search Insert Position is exactly same as:

```java
Lower Bound
```

Because we find first index where:

```java
nums[i] >= target
```

---

# Key Learnings

- Array is sorted
- Binary Search reduces search space by half
- Search Insert Position is based on Lower Bound
- Use safe mid formula:

```java
mid = low + (high - low) / 2
```

- Time complexity becomes very efficient

