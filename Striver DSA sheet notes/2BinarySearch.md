
# Binary Search om 1D Arrays
Q1 - Basic Binary Search

## 🔹 Problem Summary  
The goal is to search for a **target** element within a **sorted array** of integers. Since the array is sorted, we can use Binary Search to efficiently locate the element by repeatedly halving the search space. If the target is found, return its index; otherwise, return -1.

---

## 🔹 Key Observations & Intuition  
* **Sorted Property:** Binary Search only works on sorted data. It uses the order to eliminate half of the remaining elements at each step.
* **Pointers:** Two pointers, `low` and `high`, define the current **search space**.
* **Mid-point:** By checking the middle element (`mid`), we decide if the target is in the left half or the right half.
* **Efficiency:** Instead of a linear $O(N)$ scan, we achieve $O(\log N)$ by reducing the problem size by half in every iteration.

---

## 🔹 Approaches

### 1. Iterative Binary Search (Optimal)
**Idea:** Use a `while` loop that continues as long as the search space is valid (`low <= high`). In each iteration, calculate the middle index and adjust the pointers based on whether the target is smaller or larger than the middle element.

**Complexity:** * **Time Complexity:** $O(\log N)$ — The search space is divided by 2 at each step.  
* **Space Complexity:** $O(1)$ — No extra space or recursion stack is used.

**Java Code:**
```java
import java.util.*;

public class Solution {
    // Function to perform Binary Search on sorted array
    public static int binarySearch(int[] nums, int target) {
        int n = nums.length; // size of the array
        int low = 0, high = n - 1;

        // Keep searching until low crosses high
        while (low <= high) {
            int mid = (low + high) / 2; // Find the middle index
            if (nums[mid] == target) return mid; // Target found
            else if (target > nums[mid]) low = mid + 1; // Search in right half
            else high = mid - 1; // Search in left half
        }
        return -1; // Target not found
    }

    public static void main(String[] args) {
        int[] a = {3, 4, 6, 7, 9, 12, 16, 17}; // sorted array
        int target = 6; // target element to search
        int ind = binarySearch(a, target);
        if (ind == -1)
            System.out.println("The target is not present.");
        else
            System.out.println("The target is at index: " + ind);
    }
}
```

---

### 2. Recursive Binary Search
**Idea:** The same logic as the iterative approach is implemented using a function that calls itself. The `low` and `high` pointers are passed as arguments to define the search boundaries for each recursive call.

**Complexity:** * **Time Complexity:** $O(\log N)$  
* **Space Complexity:** $O(\log N)$ — Due to the auxiliary stack space used by recursive calls.

**Java Code:**
```java
import java.util.*;

public class Solution {
    // Recursive Binary Search function
    public static int binarySearch(int[] nums, int low, int high, int target) {
        if (low > high) return -1; // Base case: target not found

        // Find middle index
        int mid = (low + high) / 2;

        // If target is found at mid
        if (nums[mid] == target) return mid;

        // If target is greater, search right half
        else if (target > nums[mid])
            return binarySearch(nums, mid + 1, high, target);

        // Otherwise, search left half
        return binarySearch(nums, low, mid - 1, target);
    }

    // Public function to initiate search
    public static int search(int[] nums, int target) {
        return binarySearch(nums, 0, nums.length - 1, target);
    }

    public static void main(String[] args) {
        int[] a = {3, 4, 6, 7, 9, 12, 16, 17}; // sorted array
        int target = 6; // target element to search
        int ind = search(a, target);
        if (ind == -1)
            System.out.println("The target is not present.");
        else
            System.out.println("The target is at index: " + ind);
    }
}
```

---

## 🔹 Edge Cases  
* **Target not present:** The pointers will eventually cross (`low > high`), and the function should return -1.
* **Single element array:** Check if the logic correctly handles `low = 0` and `high = 0`.
* **Array size is zero:** The initial `high` becomes -1, so `low > high` is true immediately.
* **Integer Overflow:** While the website uses `(low + high) / 2`, in some scenarios with very large arrays, it is safer to use $mid = low + \frac{high - low}{2}$.

---

## 🔹 Important Notes / Takeaways  
* Binary search is the backbone for many advanced algorithms like **Binary Search on Answers**.
* Always ensure the input is **sorted** before applying this.
* The search space becomes invalid when `low` exceeds `high`.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Iterative Binary Search** | $O(\log N)$ | $O(1)$ |
| **Recursive Binary Search** | $O(\log N)$ | $O(\log N)$ (Stack Space) |

--- 
Q2
# Implement Lower Bound

## 🔹 Problem Summary
The **Lower Bound** algorithm aims to find the smallest index `ind` in a sorted array such that `arr[ind] >= x` (where `x` is the target value). 

* If such an index exists, return the smallest one.
* If no such element exists (i.e., all elements are smaller than `x`), the algorithm returns `n` (the size of the array).

---

## 🔹 Key Observations & Intuition
* **Sorted Property:** Since the input array is sorted, we can move beyond a simple linear scan and use the power of **Binary Search** to reduce time complexity.
* **The "Greater or Equal" Rule:** Unlike a standard binary search looking for an exact match, Lower Bound looks for the *first* occurrence that meets or exceeds the target.
* **Search Space:** If `arr[mid]` is already greater than or equal to `x`, it *could* be our answer, but there might be an even smaller index to the left that also satisfies the condition.

---

## 🔹 Approaches

### 1. Brute Force Approach
**Idea:**
Traverse the array from the beginning using a linear search. The first index `i` where `arr[i] >= x` is the lower bound. If the loop finishes without finding such an index, it means all elements are smaller than `x`, so we return `n`.

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int lowerBound(int []arr, int n, int x) {
        for (int i = 0; i < n; i++) {
            if (arr[i] >= x) {
                // lower bound found:
                return i;
            }
        }
        return n;
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 15, 19};
        int n = 5, x = 9;
        int ind = lowerBound(arr, n, x);
        System.out.println("The lower bound is the index: " + ind);
    }
}
```

---

### 2. Optimal Approach
**Idea:**
Use **Binary Search** to find the index. We maintain two pointers, `low` and `high`, and an `ans` variable initialized to `n`. 

1.  Calculate `mid`.
2.  If `arr[mid] >= x`, then `mid` is a potential answer. We store `mid` in `ans` and then search the **left half** (`high = mid - 1`) to see if a smaller index exists.
3.  If `arr[mid] < x`, the answer must be in the **right half**, so we move `low = mid + 1`.

**Why it is optimal:** It leverages the sorted nature of the array to eliminate half of the search space in each step, reducing the search time from linear to logarithmic.

* **Time Complexity:** $O(\log N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class tute {
    public static int lowerBound(int []arr, int n, int x) {
        int low = 0, high = n - 1;
        int ans = n;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] >= x) {
                ans = mid;
                //look for smaller index on the left
                high = mid - 1;
            } else {
                low = mid + 1; // look on the right
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 15, 19};
        int n = 5, x = 9;
        int ind = lowerBound(arr, n, x);
        System.out.println("The lower bound is the index: " + ind);
    }
}
```

---

## 🔹 Edge Cases
1.  **Target is smaller than the first element:** The lower bound will be index `0`.
2.  **Target is larger than the last element:** The lower bound will be index `n`.
3.  **Target exists multiple times:** The algorithm correctly returns the index of the **first** occurrence.
4.  **Empty Array:** The algorithm should handle this by returning `0` (size of array).

---

## 🔹 Important Notes / Takeaways
* **C++ STL Equivalent:** In C++, this is implemented as `std::lower_bound()`. In Java, `Collections.binarySearch()` returns a negative value if the element is not found, which can be transformed into the lower bound.
* **The "Search Space" Logic:** This pattern of "storing a potential answer and moving the pointer" is a classic Binary Search variation used for finding "First occurrence," "Last occurrence," "Floor," and "Ceil."

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity | Best For |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ | Unsorted arrays or very small datasets. |
| **Optimal (BS)** | $O(\log N)$ | $O(1)$ | Large, sorted datasets (Interview standard). |

---
Q3
# Implement Upper Bound

## 🔹 Problem Summary
The **Upper Bound** algorithm finds the first or the smallest index in a sorted array where the value at that index is **strictly greater** than a given key $x$. 
* The mathematical condition is: `arr[ind] > x`.
* If no such element exists (all elements are $\le x$), the result is the size of the array ($n$).

---

## 🔹 Key Observations & Intuition
* **Binary Search Eligibility:** Since the array is sorted, we can leverage Binary Search to achieve logarithmic time complexity.
* **The Search Criteria:** Unlike "Search in Sorted Array" which looks for an exact match, Upper Bound specifically looks for the first element that *exceeds* the target.
* **Potential Answer:** If `arr[mid] > x`, then `mid` is a potential answer, but we must continue searching the left half to ensure it is the *smallest* such index.

---

## 🔹 Approaches

### ➤ Brute Force
**Idea:**
Traverse the array from the beginning using a linear search. Compare each element with $x$. The first index $i$ where `arr[i] > x` is the answer. If the loop completes, return the array length.

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class UpperBoundFinder {
    // Linear search method to find upper bound
    public int upperBound(int[] arr, int x) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > x) {
                return i; // Return index of first element > x
            }
        }
        return arr.length; // Return length if no such element found
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 9, 15, 19}; // Sorted array
        int x = 9;
        UpperBoundFinder finder = new UpperBoundFinder();
        int ind = finder.upperBound(arr, x); // Call function
        System.out.println("The upper bound is the index: " + ind); // Output result
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
1. **Initialize:** Use two pointers, `low` at index $0$ and `high` at $n-1$. Initialize `ans` to $n$.
2. **Calculate Mid:** Find the middle index to divide the search space.
3. **Comparison:** * **Case 1 (arr[mid] > x):** This might be the answer. Store `mid` in `ans` and move `high = mid - 1` to look for a smaller index on the left.
   * **Case 2 (arr[mid] <= x):** This index and everything to its left cannot be the upper bound. Move `low = mid + 1` to search the right half.

**Why this approach is optimal:**
It eliminates half of the remaining elements in each step, resulting in a logarithmic time complexity, which is significantly faster than linear search for large arrays.

* **Time Complexity:** $O(\log N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class UpperBoundFinder {
    // Binary search to find upper bound
    public int upperBound(int[] arr, int x) {
        int low = 0, high = arr.length - 1;
        int ans = arr.length; // Default to length if not found

        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] > x) {
                ans = mid; // Store current index as potential answer
                high = mid - 1; // Move left
            } else {
                low = mid + 1; // Move right
            }
        }
        return ans; // Return final answer
    }

    public static void main(String[] args) {
        int[] arr = {3, 5, 8, 9, 15, 19}; // Sorted array
        int x = 9;
        UpperBoundFinder finder = new UpperBoundFinder();
        int ind = finder.upperBound(arr, x); // Call method
        System.out.println("The upper bound is the index: " + ind);
    }
}
```

---

## 🔹 Edge Cases
* **$x$ is smaller than the first element:** The index $0$ should be returned.
* **$x$ is larger than the last element:** The index $n$ (array length) should be returned.
* **$x$ is present multiple times:** The algorithm will correctly return the index of the first element *after* all occurrences of $x$.
* **All elements are the same:** If all elements are equal to $x$, the answer is $n$. If all are greater than $x$, the answer is $0$.

---

## 🔹 Important Notes / Takeaways
* **Lower vs. Upper Bound:** * Lower Bound: First index where `arr[i] >= x`.
  * Upper Bound: First index where `arr[i] > x`.
* **Standard Tooling:** In C++, this is available as `upper_bound()`. In Java, you typically implement it as shown above or use `Arrays.binarySearch()` and adjust the result.
* **Key Interview Insight:** Many problems like "Find First and Last Position of Element" or "Count Occurrences" are essentially combinations of Lower Bound and Upper Bound logic.

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---
Q4
# Search Insert Position

## 🔹 Problem Summary
The [Search Insert Position](https://takeuforward.org/arrays/search-insert-position?mode=track&sheet=a2z-dsa) problem asks you to find the index where a target value $x$ is present in a sorted array of distinct values. If the target is not found, you must return the index where it would be placed to maintain the array's sorted order.

## 🔹 Key Observations & Intuition
* **Sorted Array Property:** Whenever a problem involves searching in a sorted array, **Binary Search** is the most efficient candidate.
* **Lower Bound Connection:** This problem is a direct application of the **Lower Bound** concept. We are essentially looking for the first index `i` such that `arr[i] >= x`. 
* **Result Range:** The possible answer ranges from `0` (if $x$ is the smallest) to `n` (if $x$ is larger than all existing elements).

---

## 🔹 Approaches

### ➤ Optimal Approach
**Detailed Explanation:**
The algorithm uses two pointers, `low` and `high`, to perform a binary search. We also maintain an `ans` variable initialized to $n$ (the size of the array).
1.  **Mid Calculation:** Find the middle element.
2.  **Case 1 (`arr[mid] >= x`):** If the middle element is greater than or equal to the target, `mid` is a potential insertion point. We store `mid` in `ans` and search the left half (`high = mid - 1`) to see if there is a smaller valid index.
3.  **Case 2 (`arr[mid] < x`):** If the middle element is smaller than the target, the insertion point must be further to the right. We move the `low` pointer to `mid + 1`.

**Why this approach is optimal:**
By halving the search space in each step, it achieves logarithmic time complexity, making it significantly faster than a linear search for large datasets.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$, where $N$ is the size of the given array.
* **Space Complexity:** $O(1)$ as we are using no extra space.

**Java Code:**
```java
import java.util.*;

public class BinarySearchInsert {
    // Function to find the insert position of x in sorted array
    public int searchInsert(int [] arr, int x) {
        int n = arr.length;
        int low = 0, high = n - 1;
        int ans = n;
        // Default to end if x is greater than all elements

        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] >= x) {
                // Potential answer found, try to go left
                ans = mid;
                high = mid - 1;
            } else {
                // Go right
                low = mid + 1;
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        int [] arr = {1, 2, 4, 7};
        int x = 6;
        BinarySearchInsert obj = new BinarySearchInsert();
        int index = obj.searchInsert(arr, x);

        System.out.println("The index is: " + index);
    }
}
```

---

## 🔹 Edge Cases
* **Target is smaller than all elements:** The algorithm will return index `0`.
* **Target is larger than all elements:** The algorithm will return index `n` (the array length).
* **Target already exists:** The algorithm returns the actual index of the target.
* **Empty array:** While the problem usually assumes at least one element, the logic would return `0`.

---

## 🔹 Important Notes / Takeaways
* **Lower Bound Identity:** Always remember: `Search Insert Position` $\equiv$ `Lower Bound`.
* **Interview Tip:** When an interviewer asks for "Search Insert Position," they are testing if you can recognize that it requires the same logic as finding the first element $\ge x$.
* **Distinct Values:** The problem specifies distinct values, which simplifies the search as there is only one "correct" existing index for a target, though the binary search logic handles duplicates by finding the first occurrence anyway.

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

Q5 

# Floor and Ceil in Sorted Array

---

## 🔹 Problem Summary
Given a sorted array `arr` of `n` integers and an integer `x`, find the **floor** and **ceiling** of `x`.
* **Floor:** The largest element in the array that is smaller than or equal to `x` ($\le x$).
* **Ceiling:** The smallest element in the array that is greater than or equal to `x` ($\ge x$).

---

## 🔹 Key Observations & Intuition
* **Sorted Property:** Since the array is sorted, we don't need to check every element. We can use **Binary Search** to find both values efficiently.
* **Ceiling is Lower Bound:** The definition of the ceiling is identical to the **Lower Bound** algorithm.
* **Floor Logic:** For the floor, if `arr[mid] <= x`, it could be our answer, but we should look to the right to see if there is a *larger* number that is still $\le x$.
* **Default Value:** If no floor or ceiling exists (e.g., $x$ is smaller than the first element or larger than the last), return `-1`.

---

## 🔹 Approaches

### ➤ Optimal Approach
**Detailed Explanation:**
The approach uses two separate Binary Search logic paths (or functions) to find the floor and ceiling.
1.  **For Ceil:** We look for the smallest index where `arr[mid] >= x`. If found, we update our answer and search the left half (`high = mid - 1`) to find a smaller valid element.
2.  **For Floor:** We look for the largest index where `arr[mid] <= x`. If found, we update our answer and search the right half (`low = mid + 1`) to find a larger valid element.

**Why this approach is optimal:**
It reduces the time complexity from $O(N)$ (linear search) to $O(\log N)$ by eliminating half of the search space at each step, utilizing the sorted nature of the array.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$, where $N$ is the size of the given array.
* **Space Complexity:** $O(1)$ as no extra space is used.

**Java Code (as given on the website):**
```java
import java.util.*;

class FloorCeilFinder {
    // Function to find floor
    public int findFloor(int[] arr, int x) {
        int low = 0, high = arr.length - 1;
        int ans = -1;

        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] <= x) {
                ans = arr[mid]; // Potential floor
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return ans;
    }

    // Function to find ceiling
    public int findCeil(int[] arr, int x) {
        int low = 0, high = arr.length - 1;
        int ans = -1;

        while (low <= high) {
            int mid = (low + high) / 2;
            if (arr[mid] >= x) {
                ans = arr[mid]; // Potential ceil
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return ans;
    }

    // Function to return floor and ceil as array
    public int[] getFloorAndCeil(int[] arr, int x) {
        int f = findFloor(arr, x);
        int c = findCeil(arr, x);
        return new int[]{f, c};
    }

    public static void main(String[] args) {
        int[] arr = {3, 4, 4, 7, 8, 10};
        int x = 5;
        FloorCeilFinder finder = new FloorCeilFinder();
        int[] res = finder.getFloorAndCeil(arr, x);
        System.out.println("The floor and ceil are: " + res[0] + " " + res[1]);
    }
}
```

---

## 🔹 Edge Cases
* **$x$ is smaller than the first element:** Floor will be `-1`, Ceil will be `arr[0]`.
* **$x$ is larger than the last element:** Floor will be `arr[n-1]`, Ceil will be `-1`.
* **$x$ is present in the array:** Both Floor and Ceil will be equal to $x$.
* **All elements are the same:** If $x$ is equal to those elements, both are $x$. If not, either floor or ceil might be `-1`.

---

## 🔹 Important Notes / Takeaways
* **Lower Bound connection:** Always remember that Ceil $\equiv$ Lower Bound.
* **Binary Search variations:** This problem is a classic example of how minor changes to the `if(arr[mid] condition)` and pointer movement can solve different boundary problems.
* **Interview Tip:** Many interviewers ask to return the *index* of the floor/ceil rather than the *value*. Always clarify this before coding.

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

Q6 

# Last occurrence in a sorted array

---

## 🔹 Problem Summary
Given a sorted array of $N$ integers and a target key, find the index of the **last occurrence** of that target. If the target is not present in the array, return `-1`. The array uses 0-based indexing.

---

## 🔹 Key Observations & Intuition
* **Sorted Property:** Since the array is sorted, the identical elements will always be adjacent. This allows us to use Binary Search to optimize the search process.
* **Right-side Bias:** When we find the target element, we shouldn't stop immediately. Because we need the *last* occurrence, we must continue searching in the right half of the current range to see if the element appears again.
* **Scanning Direction:** In a brute force approach, scanning from right-to-left is more intuitive as the first match found will naturally be the last occurrence in the array.

---

## 🔹 Approaches

### ➤ Brute Force
**Idea:**
Start traversing the array from the back (last index) and move towards the first index. The moment you find an element that matches the target key, that index is the last occurrence. If the loop completes without a match, the element is not present.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$, where $N$ is the size of the array.
* **Space Complexity:** $O(1)$.

**Java Code (as given on the website):**
```java
import java.util.*; // provides last-occurrence logic
class Solution { // find last index of key by scanning from right
    public int solve ( int n, int key, List<Integer> v) { // initialize result as not found
        int res = - 1 ; // scan from the end toward the start
        for ( int i = n - 1 ; i >= 0 ; i--) { // update and stop when match found
            if (v.get(i) == key) {
                res = i;
                break ;
            }
        } // return index or -1
        return res;
    }
} // separate main class (as requested)
public class Main { // program entry
    public static void main (String[] args) { // set size
        int n = 7 ; // set key to search
        int key = 13 ; // define input list
        List<Integer> v = Arrays.asList( 3 , 4 , 13 , 13 , 13 , 20 , 40 ); // compute answer
        Solution sol = new Solution (); int ans = sol.solve(n, key, v); // print last occurrence index (or -1)
        System.out.println(ans);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
Use Binary Search to find the target. 
1.  Initialize `start = 0` and `end = n - 1`.
2.  While `start <= end`, calculate `mid`.
3.  If `arr[mid] == key`, this is a potential answer. Store `mid` in `res`, but move the `start` pointer to `mid + 1` to search the right half for a later occurrence.
4.  If `key < arr[mid]`, search the left half (`end = mid - 1`).
5.  If `key > arr[mid]`, search the right half (`start = mid + 1`).

**Why this approach is optimal:**
Binary search reduces the search space by half in each iteration, leading to logarithmic time complexity, which is much more efficient than linear scanning for large datasets.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$.
* **Space Complexity:** $O(1)$.

**Java Code (as given on the website):**
```java
import java.util.*; // provides last-occurrence binary search
class Solution { // find last index of key using binary search
    public int solve ( int n, int key, List<Integer> v) { // initialize search bounds and result
        int start = 0 ; int end = n - 1 ; int res = - 1 ; // binary search loop
        while (start <= end) { // compute mid safely
            int mid = start + (end - start) / 2 ; // when match found, store index and move right
            if (v.get(mid) == key) {
                res = mid;
                start = mid + 1 ;
            } // when key is smaller, move left
            else if (key < v.get(mid)) {
                end = mid - 1 ;
            } // otherwise move right
            else {
                start = mid + 1 ;
            }
        } // return last occurrence or -1
        return res;
    }
} // separate main class
public class Main { // program entry
    public static void main (String[] args) { // define input size and key
        int key = 13 ; // define sorted list
        List<Integer> v = Arrays.asList( 3 , 4 , 13 , 13 , 13 , 20 , 40 ); // compute n from list size
        int n = v.size(); // run search
        Solution sol = new Solution (); int ans = sol.solve(n, key, v); // print result
        System.out.println(ans);
    }
}
```

---

## 🔹 Edge Cases
* **Target not in array:** The algorithm should correctly return `-1`.
* **Target appears only once:** The algorithm should return that single index.
* **All elements are the target:** The algorithm should return `n-1`.
* **Target is at the very beginning or end:** Binary search handles these boundaries naturally.

---

## 🔹 Important Notes / Takeaways
* **Modification of Standard BS:** The key difference from standard binary search is the logic when `arr[mid] == target`. Instead of returning immediately, we save the index and keep moving `start`.
* **Foundation for Other Problems:** Finding the "last occurrence" is one half of the "First and Last Position of Element" problem.
* **Calculated Mid:** Using `mid = start + (end - start) / 2` is a good practice to prevent integer overflow in some languages.

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal Approach** | $O(\log N)$ | $O(1)$ |

---

Q7 

# Count Occurrences in Sorted Array

---

## 1. 🔹 Problem Summary
Given a sorted array of $N$ integers and a target value $X$, you need to find the total number of times $X$ appears in the array. Since the array is sorted, all occurrences of $X$ will be adjacent to each other.

---

## 2. 🔹 Key Observations & Intuition
* **Sorted Property:** The most critical observation is that the array is sorted. This immediately suggests that while a linear scan is possible, **Binary Search** will be much more efficient.
* **Contiguous Range:** In a sorted array, all instances of $X$ form a single contiguous block.
* **Mathematical Insight:** If we can find the index of the **first occurrence** and the index of the **last occurrence**, the total count can be calculated using the formula:
    $$\text{Total Count} = (\text{Last Occurrence Index} - \text{First Occurrence Index} + 1)$$
* **Empty Case:** If the element $X$ does not exist in the array (first occurrence index is $-1$), the count is simply $0$.

---

## 3. 🔹 Approaches

### ➤ Brute Force Approach
**Idea:**
Linearly search the entire array from start to finish. Use a counter variable and increment it every time the current element equals the target value $X$.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$ because we traverse the entire array once.
* **Space Complexity:** $O(1)$ as no extra space is used.

**Java Code:**
```java
import java.util.*;

public class tUf {
    public static int count(int arr[], int n, int x) {
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            // counting the occurrences:
            if (arr[i] == x) cnt++;
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr =  {2, 4, 6, 8, 8, 8, 11, 13};
        int n = 8, x = 8;
        int ans = count(arr, n, x);
        System.out.println("The number of occurrences is: " + ans);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
Instead of a linear scan, we use Binary Search twice:
1.  Find the **first occurrence** of $X$: If `arr[mid] == X`, it could be the first occurrence, so we record the index and continue searching the left half (`high = mid - 1`).
2.  Find the **last occurrence** of $X$: If `arr[mid] == X`, it could be the last occurrence, so we record the index and continue searching the right half (`low = mid + 1`).
3.  Calculate the difference: If the first occurrence is found, the count is `last - first + 1`.

**Why this approach is optimal:**
It leverages the sorted property to reduce the time complexity from $O(N)$ to $O(\log N)$. Even though we perform two binary searches, the complexity remains logarithmic, which is significantly faster for large datasets.

**Time & Space Complexity:**
* **Time Complexity:** $O(2 \times \log N)$, effectively $O(\log N)$.
* **Space Complexity:** $O(1)$ as no extra space is used.

**Java Code:**
```java
import java.util.*;

public class tUf {
    public static int firstOccurrence(int[] arr, int n, int k) {
        int low = 0, high = n - 1;
        int first = -1;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] == k) {
                first = mid;
                // look for smaller index on the left
                high = mid - 1;
            } else if (arr[mid] < k) {
                low = mid + 1; // look on the right
            } else {
                high = mid - 1; // look on the left
            }
        }
        return first;
    }

    public static int lastOccurrence(int[] arr, int n, int k) {
        int low = 0, high = n - 1;
        int last = -1;

        while (low <= high) {
            int mid = (low + high) / 2;
            // maybe an answer
            if (arr[mid] == k) {
                last = mid;
                // look for larger index on the right
                low = mid + 1;
            } else if (arr[mid] < k) {
                low = mid + 1; // look on the right
            } else {
                high = mid - 1; // look on the left
            }
        }
        return last;
    }

    public static int[] firstAndLastPosition(int[] arr, int n, int k) {
        int first = firstOccurrence(arr, n, k);
        if (first == -1) return new int[] { -1, -1};
        int last = lastOccurrence(arr, n, k);
        return new int[] {first, last};
    }

    public static int count(int arr[], int n, int x) {
        int[] ans = firstAndLastPosition(arr, n, x);
        if (ans[0] == -1) return 0;
        return (ans[1] - ans[0] + 1);
    }

    public static void main(String[] args) {
        int[] arr =  {2, 4, 6, 8, 8, 8, 11, 13};
        int n = 8, x = 8;
        int ans = count(arr, n, x);
        System.out.println("The number of occurrences is: " + ans);
    }
}
```

---

## 4. 🔹 Edge Cases
* **Element not present:** Both first and last occurrence functions will return $-1$. The logic returns $0$.
* **Element present only once:** First and last index will be the same. Formula `(i - i + 1)` correctly returns $1$.
* **All elements are the target:** First occurrence will be index $0$, last will be $n-1$. Formula returns $n$.
* **Empty Array:** The search bounds will be invalid, and the count will return $0$.

---

## 5. 🔹 Important Notes / Takeaways
* **Reusability:** This problem is a direct extension of finding the "First and Last Position of an Element." If you master that, you master this.
* **Interview Insight:** In interviews, always mention the $O(\log N)$ approach after the $O(N)$ approach to show your progression of thought and optimization skills.
* **Lower/Upper Bound:** You can also solve this using `Lower Bound` (first position) and `Upper Bound` (index after the last position). Count would be `UpperBound(X) - LowerBound(X)`.

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal Approach** | $O(\log N)$ | $O(1)$ |

---

Q8

# Search Element in a Rotated Sorted Array

---

## 1. 🔹 Problem Summary
Given an integer array `nums` that was originally sorted in ascending order but then rotated at an unknown pivot point, find the index of a target value `k`. If the target exists, return its index; otherwise, return `-1`. The array contains distinct values.

---

## 2. 🔹 Key Observations & Intuition
* **Partial Order:** Although the entire array is not sorted, if you pick any middle element, at least **one half** (either left or right) will always be perfectly sorted.
* **Binary Search Adaptability:** Since one side is always sorted, we can check if the target lies within the range of that sorted half. If it does, we eliminate the other half. If it doesn't, the target must be in the other (unsorted) half.
* **The Pivot:** The rotation creates a "break" in the sorted order, but the underlying binary search principle of halving the search space still applies.

---

## 3. 🔹 Approaches

### ➤ Brute Force Approach
**Idea:**
The simplest way is to perform a linear search. Traverse the array from left to right and compare each element with the target value.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code (exactly as given on the website):**
```java
import java.util.*;

class Solution {
    // Function to search target in rotated sorted array using brute force
    public int search(int[] nums, int target) {
        // Loop through each element in the array
        for (int i = 0; i < nums.length; i++) {
            // If current element matches target, return index
            if (nums[i] == target) {
                return i;
            }
        }
        // If not found, return -1
        return -1;
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        Solution obj = new Solution();
        int index = obj.search(nums, target);

        System.out.println(index);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
1.  Initialize `low = 0` and `high = n - 1`.
2.  While `low <= high`:
    * Find `mid`. If `nums[mid] == target`, return `mid`.
    * **Identify the sorted half:**
        * If `nums[low] <= nums[mid]`, the **left side** is sorted. Check if the target is between `nums[low]` and `nums[mid]`. If yes, search left (`high = mid - 1`), else search right (`low = mid + 1`).
        * Otherwise, the **right side** is sorted. Check if the target is between `nums[mid]` and `nums[high]`. If yes, search right (`low = mid + 1`), else search left (`high = mid - 1`).

**Why this approach is optimal:**
It utilizes the sorted property of the halves to achieve logarithmic time complexity, reducing the number of comparisons from $N$ to $\log_2 N$.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$
* **Space Complexity:** $O(1)$

**Java Code (exactly as given on the website):**
```java
import java.util.*;

class Solution {
    // Function to search target in rotated sorted array using binary search
    public int search(int[] nums, int target) {
        // Initialize search space
        int low = 0;
        int high = nums.length - 1;

        // Continue while there is still a valid search range
        while (low <= high) {
            // Calculate middle index
            int mid = (low + high) / 2;

            // If target found, return index
            if (nums[mid] == target)
                return mid;

            // If left part is sorted
            if (nums[low] <= nums[mid]) {
                // If target lies within sorted left part
                if (nums[low] <= target && target < nums[mid]) {
                    high = mid - 1;
                }
                // Else, search in right half
                else {
                    low = mid + 1;
                }
            }
            // Else, right part is sorted
            else {
                // If target lies within sorted right part
                if (nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                }
                // Else, search in left half
                else {
                    high = mid - 1;
                }
            }
        }
        // Target not found
        return -1;
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        Solution obj = new Solution();
        int result = obj.search(nums, target);

        System.out.println(result);
    }
}
```

---

## 4. 🔹 Edge Cases
* **Target is the Pivot:** The middle element could be the smallest or largest; the code handles this with `nums[mid] == target`.
* **Single Element Array:** If the target matches, it returns 0; otherwise -1.
* **Target Not Present:** The search space eventually becomes empty, and `-1` is returned.
* **Rotation at Index 0:** The array is essentially a standard sorted array; the logic still holds.

---

## 5. 🔹 Important Notes / Takeaways
* **Key Learning:** Binary search isn't just for fully sorted arrays; it works as long as you can reliably **discard half** of the search space based on a condition.
* **Interview Insight:** In rotated sorted array problems, the first step is almost always to identify which part of the split is sorted.
* **Distinct vs. Duplicates:** This specific solution is for **distinct** values. If duplicates are present, `nums[low] == nums[mid] == nums[high]` can occur, requiring a slightly modified approach (Search in Rotated Sorted Array II).

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

Q9

# Search Element in Rotated Sorted Array II

---

## 1. 🔹 Problem Summary
Given a sorted integer array `arr` that has been rotated at an unknown pivot, find if a target value `k` exists in it. Unlike the first version of this problem, the array **may contain duplicate values**. Return `true` if the element is found, otherwise return `false`.

---

## 2. 🔹 Key Observations & Intuition
* **The Duplicate Challenge:** In a rotated array without duplicates, we can always determine which half is sorted by comparing `arr[low]` and `arr[mid]`. However, with duplicates, a case like `arr[low] == arr[mid] == arr[high]` (e.g., `[3, 1, 2, 3, 3, 3, 3]`) makes it impossible to know which side is sorted.
* **Trimming the Search Space:** When the edge elements and the middle element are identical, we cannot decide where to go. The "trick" is to simply shrink the search space by moving the `low` and `high` pointers inward until this condition is broken.
* **Binary Search Still Applies:** Once the ambiguity of duplicates at the boundaries is removed, the logic remains the same as the standard "Search in Rotated Sorted Array": identify the sorted half and check if the target lies within it.

---

## 3. 🔹 Approaches

### ➤ Brute Force
**Idea:**
Traverse the entire array linearly and check if any element matches the target value `k`. This approach does not take advantage of the sorted or rotated nature of the array but works regardless of duplicates.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$, where $N$ is the size of the array.
* **Space Complexity:** $O(1)$, no extra space used.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Method to search for a target value in a rotated sorted array (with duplicates)
    public boolean searchInARotatedSortedArrayII(int [] arr, int k) {
        // Iterate through each element of the array
        for (int num : arr) {
            // If the target is found, return true
            if (num == k) return true;
        }
        // If loop completes and target not found, return false
        return false;
    }

    public static void main (String[] args) {
        // Sample rotated sorted array with duplicates
        int [] arr = {7, 8, 1, 2, 3, 3, 3, 4, 5, 6};
        int k = 3; // Target to search

        // Create object of the Solution class
        Solution obj = new Solution();

        // Call the search method
        boolean ans = obj.searchInARotatedSortedArrayII(arr, k);

        // Output result based on boolean answer
        if (!ans)
            System.out.println("Target is not present.");
        else
            System.out.println("Target is present in the array.");
    }
}
```

---

### ➤ Optimised Approach
**Detailed Explanation:**
1.  **Initialize:** Set `low = 0` and `high = n - 1`.
2.  **Handle Duplicates:** If `arr[low] == arr[mid] == arr[high]`, we cannot tell which side is sorted. Increment `low` and decrement `high` and `continue` to the next iteration.
3.  **Identify Sorted Half:**
    * If `arr[low] <= arr[mid]`, the left half is sorted. Check if `k` lies between `arr[low]` and `arr[mid]`. If so, search left; otherwise, search right.
    * Otherwise, the right half is sorted. Check if `k` lies between `arr[mid]` and `arr[high]`. If so, search right; otherwise, search left.

**Why this approach is optimal:**
It maintains a logarithmic time complexity for most cases by halving the search space, only reverting to linear-like behavior in the specific worst-case scenario where many duplicates exist at the boundaries.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$ for the best and average case. $O(N/2)$ for the worst case (when there are many duplicates).
* **Space Complexity:** $O(1)$, no extra space used.

**Java Code:**
```java
import java.util.*;

class Solution {
    public boolean searchInRotatedSortedArrayII(int [] arr, int k) {
        int low = 0, high = arr.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;

            // If mid element is the target
            if (arr[mid] == k) return true;

            // Handle duplicates: cannot determine sorted side
            if (arr[low] == arr[mid] && arr[mid] == arr[high]) {
                low++;
                high--;
                continue;
            }

            // Left half is sorted
            if (arr[low] <= arr[mid]) {
                if (arr[low] <= k && k <= arr[mid]) {
                    high = mid - 1; // Search left
                } else {
                    low = mid + 1; // Search right
                }
            }
            // Right half is sorted
            else {
                if (arr[mid] <= k && k <= arr[high]) {
                    low = mid + 1; // Search right
                } else {
                    high = mid - 1; // Search left
                }
            }
        }
        return false; // Not found
    }

    public static void main(String[] args) {
        int [] arr = {7, 8, 1, 2, 3, 3, 3, 4, 5, 6};
        int k = 3;
        Solution obj = new Solution();
        boolean ans = obj.searchInRotatedSortedArrayII(arr, k);
        if (ans)
            System.out.println("Target is present in the array.");
        else
            System.out.println("Target is not present.");
    }
}
```

---

## 4. 🔹 Edge Cases
* **All elements are the same:** E.g., `[1, 1, 1, 1]`, target `1` or `2`.
* **Target is at the pivot:** E.g., `[3, 1, 2, 3]`, target `1`.
* **Ambiguous Duplicates:** E.g., `[3, 3, 0, 3, 3, 3, 3]`, where `arr[low] == arr[mid] == arr[high]`.
* **Single Element Array:** E.g., `[1]`, target `1` or `0`.

---

## 5. 🔹 Important Notes / Takeaways
* **The "Duplicates" Caveat:** This is a classic interview follow-up. Always clarify if the rotated array has distinct or duplicate elements, as it changes the worst-case time complexity from $O(\log N)$ to $O(N)$.
* **Interview Insight:** The core of the problem is identifying the **sorted portion**. Even in a rotated array, at least one half must be sorted.
* **Logic Pattern:** Shrink boundaries when `arr[low] == arr[mid] == arr[high]` to restore the ability to identify the sorted half.

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimised (Binary Search)** | $O(\log N)$ (Avg), $O(N)$ (Worst) | $O(1)$ |

---

Q10

# Minimum in Rotated Sorted Array

---

## 1. 🔹 Problem Summary
Given an integer array `arr` of size `N`, which was originally sorted in ascending order but then rotated at some unknown pivot index, find the **minimum element** in the array. The array contains distinct values.

---

## 2. 🔹 Key Observations & Intuition
* **The Pivot Point:** In a rotated sorted array, the minimum element is the only element that is smaller than its previous element. It represents the point where the rotation occurred.
* **Two Sorted Segments:** The rotation splits the array into two sorted parts. Binary Search can be adapted to decide which part contains the "dip" (minimum element).
* **Sorted Half Logic:** If `arr[low] <= arr[mid]`, the left half is sorted. If the entire left half is sorted, the minimum *could* be `arr[low]`, but we must also check the unsorted right half.
* **Comparison with Rightmost:** By comparing `arr[mid]` with `arr[high]`, we can determine if the minimum lies in the right half (if `arr[mid] > arr[high]`) or in the left half including `mid` (if `arr[mid] <= arr[high]`).

---

## 3. 🔹 Approaches

### ➤ Brute-Force Approach
**Idea:**
Traverse the entire array using a linear search and maintain a variable to track the minimum value encountered so far.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$, as we check every element once.
* **Space Complexity:** $O(1)$, as only a constant amount of extra space is used.

**Java Code:**
```java
class Solution {
    // Function to find the minimum element using linear search
    public int findMin(int[] nums) {
        // Initialize answer with a large number
        int minVal = Integer.MAX_VALUE;
        // Traverse each element
        for (int i = 0; i < nums.length; i++) {
            // Update minimum value
            minVal = Math.min(minVal, nums[i]);
        }
        // Return the result
        return minVal;
    }
}
public class Main {
    public static void main(String[] args) {
        // Input array
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        // Create object of Solution
        Solution sol = new Solution();
        // Call function and store result
        int result = sol.findMin(nums);
        // Output the result
        System.out.println("Minimum element is " + result);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
1. Initialize `low = 0` and `high = n - 1`.
2. While `low < high`:
   - Calculate `mid`.
   - **Check which half to discard:**
     - If `nums[mid] > nums[high]`: The left half (including `mid`) is sorted and increasing, so the "pivot" (minimum) must be in the right half. Move `low = mid + 1`.
     - Else (`nums[mid] <= nums[high]`): The right half is sorted and the minimum is either at `mid` or to the left of `mid`. Move `high = mid`.
3. When `low == high`, the pointer points to the minimum element.

**Why this approach is optimal:**
It utilizes the sorted property of the segments to reduce the search space by half in each iteration, achieving logarithmic time complexity.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$, as the search space is halved at every step.
* **Space Complexity:** $O(1)$, constant additional space is used.

**Java Code:**
```java
class Solution {
    // Function to find the minimum element using binary search
    public int findMin(int[] nums) {
        // Initialize low and high pointers
        int low = 0, high = nums.length - 1;
        // Binary search loop
        while (low < high) {
            // Calculate mid index
            int mid = low + (high - low) / 2;
            // Check which half to discard
            if (nums[mid] > nums[high]) {
                // Minimum lies in right half
                low = mid + 1;

            } else {
                // Minimum lies in left half (including mid)
                high = mid;
            }
        }
        // Return the minimum element
        return nums[low];
    }
}
public class Main {
    public static void main(String[] args) {
        // Input array
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        // Create object of Solution
        Solution sol = new Solution();
        // Call function and store result
        int result = sol.findMin(nums);
        // Output the result
        System.out.println("Minimum element is " + result);
    }
}
```

---

## 4. 🔹 Edge Cases
* **Array is not rotated:** The array is already sorted (e.g., `[1, 2, 3, 4]`). `nums[low]` will be the minimum.
* **Array rotated $N$ times:** Essentially the same as not being rotated.
* **Single element array:** `low` and `high` start equal, the loop doesn't run, and it correctly returns `nums[0]`.
* **Minimum at the very end or very beginning:** Binary Search pointers will correctly converge to these boundaries.

---

## 5. 🔹 Important Notes / Takeaways
* **Smallest = Pivot:** In this problem, the minimum element is synonymous with the pivot point of rotation.
* **Binary Search Property:** Binary search works here because we can always identify a sorted half and an "unsorted" half (which contains the minimum).
* **Template Tip:** Notice the `while (low < high)` and `high = mid` logic. This is a common template to find a specific boundary element without getting stuck in infinite loops.

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

Q11

# Find out how many times the array has been rotated

---

## 1. 🔹 Problem Summary
Given an integer array `arr` of size `N`, sorted in ascending order with distinct values, the array has been rotated between 1 to `N` times. The goal is to determine exactly how many times the array was rotated. 

* **Logic:** The number of rotations is equal to the **index of the minimum element** in the array.

---

## 2. 🔹 Key Observations & Intuition
* **The Minimum Element Rule:** In a sorted array `[0, 1, 2, 3]`, if you rotate it 1 time, it becomes `[3, 0, 1, 2]`. Notice the minimum element `0` moved to index `1`. If you rotate it 2 times, it becomes `[2, 3, 0, 1]`, and `0` is at index `2`. Thus, the **rotation count = index of the minimum element**.
* **The "Break" Point:** In a rotated sorted array, there is exactly one point where an element is greater than the next element (`arr[i] > arr[i+1]`). This "break" marks the start of the original sorted sequence.
* **Binary Search Potential:** Since the original array was sorted, we can use the properties of rotated sorted arrays to find the minimum element in logarithmic time instead of linear time.

---

## 3. 🔹 Approaches

### ➤ Brute Force Approach
**Idea:**
Iterate through the entire array to find the smallest element. Keep track of the minimum value and its index. Once the traversal is complete, the index of that minimum value represents the number of rotations.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the number of rotations in a rotated sorted array
    public int findRotations(int [] arr) {
        // Store size of array
        int n = arr.length;
        // Assume the first element is the smallest
        int minVal = arr[0];
        // Index of the smallest element
        int minIndex = 0;

        // Traverse the array
        for (int i = 1; i < n; i++) {
            // If current element is smaller than minVal, update
            if (arr[i] < minVal) {
                minVal = arr[i];
                minIndex = i;
            }
        }
        // The index of smallest element = number of rotations
        return minIndex;
    }
}

public class Main {
    public static void main (String[] args) {
        Solution obj = new Solution ();
        // Example input
        int [] arr = {4, 5, 6, 7, 0, 1, 2, 3};
        // Call the function and store result
        int rotations = obj.findRotations(arr);
        // Print result
        System.out.println(rotations);
    }
}
```

---

### ➤ Better Approach
**Idea:**
Instead of tracking a running minimum, simply look for the "break" in the ascending order. In a rotated sorted array, the first element `arr[i+1]` that is smaller than its predecessor `arr[i]` is the minimum element. The index `i + 1` is the rotation count.

**Improvement over brute force:**
It can potentially stop early as soon as the pivot (the break) is found, rather than always scanning the full array.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find rotation count using one-pass scan
    public int findRotationCount(int [] arr) {
        // Get size of array
        int n = arr.length;
        // Traverse till second-last element
        for (int i = 0; i < n - 1; i++) {
            // If break in ascending order found
            if (arr[i] > arr[i + 1]) {
                // Index of next element is rotation count
                return i + 1;
            }
        }
        // No rotation found
        return 0;
    }
}

public class Main {
    public static void main (String[] args) {
        // Example input
        int [] arr = {3, 4, 5, 1, 2};
        // Create object of Solution
        Solution sol = new Solution ();
        // Call the function
        int rotations = sol.findRotationCount(arr);
        // Output the result
        System.out.println(rotations);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
This approach uses **Binary Search**. We compare the middle element with the rightmost element:
1.  If `arr[mid] > arr[high]`, it means the rotation point (and thus the minimum element) must lie to the right of `mid`. So, we set `low = mid + 1`.
2.  Otherwise, the rotation point is either at `mid` or to the left of `mid`. So, we set `high = mid`.
3.  The loop continues until `low` meets `high`, which will be the index of the smallest element.

**Why this approach is optimal:**
It reduces the search space by half in each step, resulting in logarithmic time complexity, which is the most efficient way to search in sorted/rotated structures.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find rotation count using binary search
    public int findRotations(int [] arr) {
        int low = 0;
        int high = arr.length - 1;

        // Loop until low meets high
        while (low < high) {
            int mid = low + (high - low) / 2;

            // If mid element is greater than element at high,
            // smallest element lies to the right of mid
            if (arr[mid] > arr[high]) {
                low = mid + 1;
            } else {
                // Else smallest element is at mid or to the left
                high = mid;
            }
        }
        // When low == high, we found the smallest element
        return low;
    }
}

public class Main {
    public static void main (String[] args) {
        Solution sol = new Solution ();
        int [] arr = {4, 5, 6, 7, 0, 1, 2, 3};
        int rotations = sol.findRotations(arr);

        System.out.println(rotations);
    }
}
```

---

## 4. 🔹 Edge Cases
* **No Rotation (0 or N times):** If the array is `[1, 2, 3, 4, 5]`, the minimum is at index `0`. The algorithm returns `0`.
* **Single Element:** If the array is `[1]`, the loop condition `low < high` is false initially, returning index `0`.
* **Rotation at the last element:** If the minimum is at the very end, binary search correctly converges there.

---

## 5. 🔹 Important Notes / Takeaways
* **Core Equivalence:** Finding the rotation count is exactly the same problem as finding the **index of the minimum element** in a rotated sorted array.
* **Binary Search Condition:** Notice the `while (low < high)` loop and `high = mid` logic. This is a common pattern to find a specific pivot point without overshooting.
* **Distinct Values:** These approaches assume distinct values. If duplicates were present, the binary search would need refinement (similar to Search in Rotated Sorted Array II).

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Better (One-pass)** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

Q12

# Search Single Element in a sorted array

These notes are based on the [Search Single Element in a sorted array](https://takeuforward.org/data-structure/search-single-element-in-a-sorted-array?mode=track&sheet=a2z-dsa) tutorial.

---

## 1. 🔹 Problem Summary
Given a sorted array of $N$ integers where every number appears exactly twice except for one specific number, find that single unique number.

---

## 2. 🔹 Key Observations & Intuition
* **Neighbor Comparison:** In a sorted array, duplicates are always adjacent. If an element is not equal to its left or right neighbor, it must be the unique one.
* **XOR Property:** XORing a number with itself results in 0 ($a \oplus a = 0$), and XORing with 0 results in the number itself ($a \oplus 0 = a$).
* **Index Pattern (Binary Search):** * Before the single element: Pairs start at an **even index** and end at an **odd index** $(even, odd)$.
    * After the single element: The pattern shifts; pairs start at an **odd index** and end at an **even index** $(odd, even)$.
    * This shift allows us to use **Binary Search** to find the exact point where the pattern breaks.

---

## 3. 🔹 Approaches

### ➤ Brute force Approach 1
**Idea:**
Traverse the array and compare each element with its neighbors. If an element is not equal to the one before it and the one after it, it is the single element. Special checks are required for the first and last elements.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;
public class Solution {
    // Function to find the single non-duplicate element
    public int singleNonDuplicate(int [] arr) {
        // Get the size of the array
        int n = arr.length;
        // If array has only one element, return it
        if (n == 1) return arr[0];
        // Loop through the array
        for (int i = 0; i < n; i++) {
            // Check if it's the first element and not equal to the next
            if (i == 0) {
                if (arr[i] != arr[i + 1]) return arr[i];
            }
            // Check if it's the last element and not equal to the previous
            else if (i == n - 1) {
                if (arr[i] != arr[i - 1]) return arr[i];
            }
            // Check if the current element is not equal to both neighbors
            else {
                if (arr[i] != arr[i - 1] && arr[i] != arr[i + 1]) return arr[i];
            }
        }
        // Dummy return if no element found
        return -1;
    }
}
// Driver class with main method
class Main {
    public static void main (String[] args) {
        // Input array with one unique element
        int [] arr = {1, 1, 2, 2, 3, 3, 4, 5, 5, 6, 6};
        // Create an object of Solution class
        Solution obj = new Solution ();
        // Call the function and store result
        int ans = obj.singleNonDuplicate(arr);
        // Print the result
        System.out.println("The single element is: " + ans);
    }
}
```

---

### ➤ Brute Approach 2
**Idea:**
Utilize the XOR operation. Since $a \oplus a = 0$, all pairs will cancel each other out, leaving only the single element in the result.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;
public class Solution {
    // Function to find the single non-duplicate element using XOR
    public int singleNonDuplicate(int [] arr) {
        // Get the size of the array
        int n = arr.length;
        // Initialize the result variable with 0
        int ans = 0;
        // Traverse the array and XOR all elements
        for (int i = 0; i < n; i++) {
            ans = ans ^ arr[i];
        }
        // Return the unique element found using XOR
        return ans;
    }
}
// Separate Main class to run the driver code
class Main {
    public static void main (String[] args) {
        // Input array with all elements occurring twice except one
        int [] arr = {1, 1, 2, 2, 3, 3, 4, 5, 5, 6, 6};
        // Create an object of Solution class
        Solution obj = new Solution ();
        // Call the function and store the result
        int ans = obj.singleNonDuplicate(arr);
        // Print the result
        System.out.println("The single element is: " + ans);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
Since the array is sorted, we use **Binary Search**. We check if `mid` is part of a valid $(even, odd)$ pair:
* If `mid` is **even** and `arr[mid] == arr[mid+1]`, or `mid` is **odd** and `arr[mid] == arr[mid-1]`, we are in the **left half** (before the unique element). Move `low = mid + 1`.
* Otherwise, we are in the **right half**. Move `high = mid - 1`.

**Why this approach is optimal:**
It reduces the search space by half in each iteration, achieving logarithmic time complexity, which is significantly faster than linear approaches for large datasets.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;
public class Solution {
    // Function to find the single non-duplicate element using binary search
    public int singleNonDuplicate(int [] arr) {
        // Get the size of the array
        int n = arr.length;
        // Edge case: only one element in the array
        if (n == 1) return arr[0];
        // Edge case: first element is the unique one
        if (arr[0] != arr[1]) return arr[0];
        // Edge case: last element is the unique one
        if (arr[n - 1] != arr[n - 2]) return arr[n - 1];
        // Initialize binary search bounds (exclude first and last index)
        int low = 1, high = n - 2;
        // Perform binary search
        while (low <= high) {
            // Calculate middle index
            int mid = (low + high) / 2;
            // Check if middle element is the unique one
            if (arr[mid] != arr[mid + 1] && arr[mid] != arr[mid - 1]) {
                return arr[mid];
            }
            // If mid is in the left half (pairing is valid)
            if ((mid % 2 == 1 && arr[mid] == arr[mid - 1]) ||
                (mid % 2 == 0 && arr[mid] == arr[mid + 1])) {
                // Move to the right half
                low = mid + 1;
            }
            // If mid is in the right half (pairing broken earlier)
            else {
                // Move to the left half
                high = mid - 1;
            }
        }
        // Dummy return (not reachable if input is valid)
        return -1;
    }
}
// Driver code
class Main {
    public static void main (String[] args) {
        // Input array with all elements appearing twice except one
        int [] arr = {1, 1, 2, 2, 3, 3, 4, 5, 5, 6, 6};
        // Create an object of Solution class
        Solution obj = new Solution ();
        // Call the function and store the result
        int ans = obj.singleNonDuplicate(arr);
        // Print the result
        System.out.println("The single element is: " + ans);
    }
}
```

---

## 4. 🔹 Edge Cases
* **Array size is 1:** Return the only element.
* **Unique element at index 0:** Handled by checking `arr[0] != arr[1]`.
* **Unique element at the last index:** Handled by checking `arr[n-1] != arr[n-2]`.
* **Binary Search range:** By starting `low` at 1 and `high` at `n-2`, we prevent index out-of-bounds errors when checking `mid-1` and `mid+1`.

---

## 5. 🔹 Important Notes / Takeaways
* The **XOR approach** is brilliant and works even if the array is **not sorted**.
* The **Binary Search approach** is required if the interviewer insists on $O(\log N)$ time, which is only possible because the array is **sorted**.
* Remember the pairing logic: $(even, odd)$ is the state before the single element appears.

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force 1 (Neighbors)** | $O(N)$ | $O(1)$ |
| **Brute Force 2 (XOR)** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

Q13

# Peak element in Array

Based on the [Peak element in Array](https://takeuforward.org/data-structure/peak-element-in-array?mode=track&sheet=a2z-dsa) tutorial, here are your structured revision notes.

---

## 1. 🔹 Problem Summary
A **peak element** is an element that is strictly greater than its neighbors. 
- For an element `arr[i]`, it is a peak if `arr[i-1] < arr[i]` and `arr[i+1] < arr[i]`.
- For boundary elements, we only check the available neighbor (the first element is a peak if it's greater than the second; the last is a peak if it's greater than the second-to-last).
- The task is to return the **index** of any one peak element if multiple exist.

---

## 2. 🔹 Key Observations & Intuition
* **Visualizing the Array:** Imagine the array as a mountain range. A peak can occur at the very start (increasing then decreasing), at the very end (continually increasing), or anywhere in the middle.
* **The "Slope" Property:** To find a peak, we need to find a point where the sequence changes from increasing to decreasing. 
* **Binary Search Logic:** We can determine which way to move by looking at the slope. If `arr[mid] < arr[mid+1]`, we are on an upward slope, and a peak must exist to the right. If `arr[mid] > arr[mid+1]`, we are on a downward slope (or at the peak), so we look to the left.

---

## 3. 🔹 Approaches

### ➤ Brute Force Approach
**Idea:**
Traverse the entire array and compare each element with its neighbors. For the first and last indices, since both neighbors aren't available, we check their only available neighbor.

**Time & Space Complexity:**
* **Time Complexity:** $O(N)$, as we traverse the entire array once.
* **Space Complexity:** $O(1)$, as constant additional space is used.

**Java Code (as given on the website):**
```java
class Solution {
    // Function to find a peak element in the array
    public int findPeakElement(int[] nums) {
        int n = nums.length;
        // Traverse the array
        for (int i = 0; i < n; i++) {
            // Check left neighbor if exists
            boolean left = (i == 0) || (nums[i] >= nums[i - 1]);
            // Check right neighbor if exists
            boolean right = (i == n - 1) || (nums[i] >= nums[i + 1]);
            // If both conditions are true
            if (left && right) return i;
        }
        // In case no peak found
        return -1;
    }
}
// Driver
public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {1, 3, 20, 4, 1, 0};
        int index = sol.findPeakElement(nums);
        System.out.println("Peak at index: " + index + " with value: " + nums[index]);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation:**
We use **Binary Search** to eliminate halves of the array. 
1. Initialize `low = 0` and `high = n - 1`.
2. Find `mid`. 
3. Compare `nums[mid]` with `nums[mid + 1]`.
4. If `nums[mid] > nums[mid + 1]`, the current `mid` could be a peak or the peak is to the left. So, we shrink the right bound: `high = mid`.
5. Otherwise, the peak must be to the right of `mid`. We shift the left bound: `low = mid + 1`.
6. When `low` and `high` converge, we have found the index of a peak element.

**Why this approach is optimal:**
It reduces the search space by half at every step, allowing us to find a peak in logarithmic time, which is significantly faster for large arrays.

**Time & Space Complexity:**
* **Time Complexity:** $O(\log N)$, as we reduce the search space to half at every step.
* **Space Complexity:** $O(1)$, as constant additional space is used.

**Java Code (as given on the website):**
```java
class Solution {
    // Function to find a peak element using binary search
    public int findPeakElement(int[] nums) {
        // Set left and right bounds
        int low = 0, high = nums.length - 1;
        // Binary search loop
        while (low < high) {
            // Find mid point
            int mid = (low + high) / 2;
            // If mid element is greater than next
            if (nums[mid] > nums[mid + 1]) {
                // Move to left half
                high = mid;
            } else {
                // Move to right half
                low = mid + 1;
            }
        }
        // Return peak index
        return low;
    }
}
public class Main {
    public static void main(String[] args) {
        // Input array
        int[] nums = {1, 2, 1, 3, 5, 6, 4};
        // Create object
        Solution obj = new Solution();
        // Output result
        System.out.println(obj.findPeakElement(nums));
    }
}
```

---

## 4. 🔹 Edge Cases
* **Array size is 1:** The only element is technically a peak.
* **Strictly increasing array:** The last element is the peak.
* **Strictly decreasing array:** The first element is the peak.
* **Multiple peaks:** The Binary Search approach will return the index of *one* of the peaks, which is acceptable per the problem statement.

---

## 5. 🔹 Important Notes / Takeaways
* **Non-sorted Binary Search:** This is a classic example showing that Binary Search can be applied to unsorted arrays if there is a clear condition to eliminate half of the search space.
* **Slope Logic:** Always look at the neighbor to determine if you are ascending or descending.
* **Guaranteed Peak:** In any array where the boundaries are treated as negative infinity (or just checked separately), at least one peak is mathematically guaranteed to exist.

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

# Binary Search on Answers

