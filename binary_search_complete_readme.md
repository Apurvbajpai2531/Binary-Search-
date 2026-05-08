# Binary Search

Binary Search is an efficient searching algorithm used on a sorted array.

It works by repeatedly dividing the search space into half.

---

# Condition

Binary Search works only on:

```java
Sorted Array
```

---

# Example

```java
Input:
arr = [1,2,3,4,5,6,7]
target = 5
```

Output:

```java
4
```

Because target `5` is present at index `4`.

---

# Idea Behind Binary Search

We maintain two pointers:

```java
low
high
```

Find middle index:

```java
mid = low + (high - low) / 2
```

Then:

- If target found → return index
- If target is greater than middle element → move right
- Else move left

---

# Why Use

```java
mid = low + (high - low) / 2
```

instead of:

```java
mid = (low + high) / 2
```

?

To avoid integer overflow.

Example:

```java
low = 2000000000
high = 2100000000
```

Then:

```java
low + high
```

can exceed Java int limit.

Safe formula:

```java
mid = low + (high - low) / 2
```

---

# Dry Run

## Input

```java
arr = [1,2,3,4,5,6,7]
target = 5
```

Initial:

```java
low = 0
high = 6
```

---

# Step 1

Find mid:

```java
mid = 0 + (6-0)/2
mid = 3
```

```java
arr[mid] = 4
```

Since:

```java
5 > 4
```

Move right:

```java
low = mid + 1
low = 4
```

---

# Step 2

Now:

```java
low = 4
high = 6
```

Find mid:

```java
mid = 4 + (6-4)/2
mid = 5
```

```java
arr[mid] = 6
```

Since:

```java
5 < 6
```

Move left:

```java
high = mid - 1
high = 4
```

---

# Step 3

Now:

```java
low = 4
high = 4
```

Find mid:

```java
mid = 4
```

```java
arr[mid] = 5
```

Target found.

Return:

```java
4
```

---

# Iterative Binary Search Code

```java
class Solution {

    public int search(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            else if (nums[mid] < target) {
                low = mid + 1;
            }

            else {
                high = mid - 1;
            }
        }

        return -1;
    }
}
```

---

# Recursive Binary Search Code

```java
class Solution {

    public int search(int[] nums, int target) {

        return binarySearch(nums, 0, nums.length - 1, target);
    }

    int binarySearch(int[] arr, int low, int high, int target) {

        if (low > high)
            return -1;

        int mid = low + (high - low) / 2;

        if (arr[mid] == target)
            return mid;

        else if (arr[mid] < target)
            return binarySearch(arr, mid + 1, high, target);

        else
            return binarySearch(arr, low, mid - 1, target);
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

### Iterative

```java
O(1)
```

### Recursive

```java
O(log n)
```

---

# Lower Bound

Lower Bound means:

First index where:

```java
arr[i] >= target
```

---

# Example

```java
arr = [1,2,4,4,5,6]
target = 4
```

Output:

```java
2
```

Because first element satisfying:

```java
arr[i] >= 4
```

is at index `2`.

---

# Lower Bound Code

```java
class Solution {

    int lowerBound(int[] arr, int target) {

        int n = arr.length;

        int low = 0;
        int high = n - 1;

        int ans = n;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] >= target) {

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

# Upper Bound

Upper Bound means:

First index where:

```java
arr[i] > target
```

---

# Example

```java
arr = [1,2,4,4,5,6]
target = 4
```

Output:

```java
4
```

Because first element greater than `4` is `5` at index `4`.

---

# Upper Bound Code

```java
class Solution {

    int upperBound(int[] arr, int target) {

        int n = arr.length;

        int low = 0;
        int high = n - 1;

        int ans = n;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] > target) {

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

# Applications of Binary Search

- Search in sorted array
- Lower Bound
- Upper Bound
- First and Last Occurrence
- Search Insert Position
- Peak Element
- Rotated Sorted Array
- Square Root
- Binary Search on Answers
- Allocate Minimum Pages
- Aggressive Cows

---

# Key Learnings

- Binary Search works only on sorted arrays
- Divide search space into half
- Use safe mid formula to avoid overflow
- Time complexity is very efficient
- Lower Bound uses `>=`
- Upper Bound uses `>`

