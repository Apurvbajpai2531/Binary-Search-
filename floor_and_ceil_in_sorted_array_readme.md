# Floor and Ceil in Sorted Array

## Problem Statement

Given a sorted array and a target value `x`, find:

- Floor of x
- Ceil of x

---

# Definitions

## Floor

Floor of `x` is:

```java
Largest element <= x
```

---

## Ceil

Ceil of `x` is:

```java
Smallest element >= x
```

---

# Example

```java
Input:
arr = [1,2,4,6,10,12,14]
x = 7
```

Output:

```java
Floor = 6
Ceil  = 10
```

Explanation:

- Largest element <= 7 is 6
- Smallest element >= 7 is 10

---

# Brute Force Approach

Traverse the array:

- Keep updating floor
- Keep updating ceil

---

# Brute Force Code

```java
class Solution {

    public int[] getFloorAndCeil(int[] arr, int x) {

        int floor = -1;
        int ceil = -1;

        for (int num : arr) {

            if (num <= x) {
                floor = num;
            }

            if (num >= x) {

                ceil = num;
                break;
            }
        }

        return new int[]{floor, ceil};
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

---

# Finding Floor

We need:

```java
Largest element <= x
```

Idea:

- If arr[mid] <= x
  - possible floor
  - move right for larger value

Else:
- move left

---

# Floor Code

```java
class Solution {

    int floor(int[] arr, int x) {

        int low = 0;
        int high = arr.length - 1;

        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] <= x) {

                ans = arr[mid];
                low = mid + 1;
            }

            else {

                high = mid - 1;
            }
        }

        return ans;
    }
}
```

---

# Finding Ceil

We need:

```java
Smallest element >= x
```

Idea:

- If arr[mid] >= x
  - possible ceil
  - move left for smaller value

Else:
- move right

---

# Ceil Code

```java
class Solution {

    int ceil(int[] arr, int x) {

        int low = 0;
        int high = arr.length - 1;

        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] >= x) {

                ans = arr[mid];
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

# Combined Optimal Code

```java
class Solution {

    public int[] getFloorAndCeil(int[] arr, int x) {

        int floor = getFloor(arr, x);
        int ceil = getCeil(arr, x);

        return new int[]{floor, ceil};
    }

    int getFloor(int[] arr, int x) {

        int low = 0;
        int high = arr.length - 1;

        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] <= x) {

                ans = arr[mid];
                low = mid + 1;
            }

            else {

                high = mid - 1;
            }
        }

        return ans;
    }

    int getCeil(int[] arr, int x) {

        int low = 0;
        int high = arr.length - 1;

        int ans = -1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (arr[mid] >= x) {

                ans = arr[mid];
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

# Dry Run

## Input

```java
arr = [1,2,4,6,10,12,14]
x = 7
```

---

# Floor Dry Run

Initial:

```java
low = 0
high = 6
ans = -1
```

---

# Step 1

```java
mid = 3
arr[mid] = 6
```

Since:

```java
6 <= 7
```

Possible floor:

```java
ans = 6
```

Move right:

```java
low = mid + 1
```

---

# Step 2

```java
mid = 5
arr[mid] = 12
```

Since:

```java
12 > 7
```

Move left:

```java
high = mid - 1
```

---

# Step 3

```java
mid = 4
arr[mid] = 10
```

Since:

```java
10 > 7
```

Move left.

Loop ends.

Floor:

```java
6
```

---

# Ceil Dry Run

Initial:

```java
low = 0
high = 6
ans = -1
```

---

# Step 1

```java
mid = 3
arr[mid] = 6
```

Since:

```java
6 < 7
```

Move right.

---

# Step 2

```java
mid = 5
arr[mid] = 12
```

Since:

```java
12 >= 7
```

Possible ceil:

```java
ans = 12
```

Move left.

---

# Step 3

```java
mid = 4
arr[mid] = 10
```

Since:

```java
10 >= 7
```

Better ceil found.

```java
ans = 10
```

Loop ends.

Ceil:

```java
10
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

## Floor Relation

Floor is similar to:

```java
Last occurrence of <= x
```

---

## Ceil Relation

Ceil is similar to:

```java
Lower Bound
```

Because Lower Bound finds:

```java
First element >= x
```

---

# Key Learnings

- Array must be sorted
- Binary Search reduces complexity
- Floor uses `<=`
- Ceil uses `>=`
- Floor searches right side
- Ceil searches left side
- Use safe mid formula:

```java
mid = low + (high - low) / 2
```

