
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
...
# Binary Search on Answers
Q1
# Finding Sqrt of a number using Binary Search

1. 🔹 **Problem Summary**
Given a positive integer `n`, find its square root. If `n` is not a perfect square, return the **floor value** of the square root (the largest integer $x$ such that $x^2 \le n$).

---

2. 🔹 **Key Observations & Intuition**
* **Search Space:** The square root of a number `n` will always reside in the range $[1, n]$.
* **Monotonicity:** The values in our search space are sorted. If $x^2 > n$, then for any $y > x$, $y^2$ will also be $> n$. This property allows us to use **Binary Search** to find the threshold where the condition $x^2 \le n$ is last satisfied.
* **Integer Overflow:** When calculating $i \times i$ or $mid \times mid$, the result can exceed the range of a standard 32-bit integer. Using `long` for these calculations is essential.

---

3. 🔹 **Approaches**

### ➤ Brute-Force Approach
**Idea**
The idea is that the square root of a number n will always lie between 1 and n. So, we can linearly search in this range to find the largest integer x such that square of x is less than or equal to number n.
* Start by creating a variable called `ans` to hold the result and run a loop from 1 up to n.
* While the square of the current number is less than or equal to n, keep updating `ans` with that number.
* As soon as the square of the number becomes greater than n, stop the loop because no bigger number can be the answer.

**Time & Space Complexity**
* **Time Complexity:** $O(N)$, we check for every number from 1 to $N$.
* **Space Complexity:** $O(1)$, since the algorithm does not use any additional space or data structures.

**Java Code**
```java
class Solution {
    // Function to find floor of square root using linear search
    public int floorSqrt ( int n) {
        // Variable to store answer
        int ans = 0 ;
        // Run loop from 1 to n
        for ( int i = 1 ; i <= n; i++) {
            // Check if i*i <= n
            if (( long )(i) * i <= n) {
                // Update answer
                ans = i;
            } else {
                // Break when i*i > n
                break ;
            }
        }
        // Return final answer
        return ans;
    }
}
public class Main {
    public static void main (String[] args) {
        // Example input
        int n = 27 ;
        // Create object of Solution
        Solution sol = new Solution ();
        // Call function and print result
        System.out.println(sol.floorSqrt(n));
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
The naive method tries every number, which is slow when n is large. But our possible answer space (from 1 to n) is sorted, meaning if a certain number squared is less than or equal to n, then all smaller numbers will also work. This allows us to apply Binary Search on the answer space to efficiently find the largest number whose square is less than or equal to n.
* Set the search range with the smallest value as 1 and the largest value as n.
* Use binary search within this range to test possible numbers.
* At each step, take the middle number (`mid`) and check if `mid * mid <= n`.
* If it is, record `mid` as a candidate (`ans`) and move **right** (`left = mid + 1`) to check for a larger number.
* If the square is greater than n, move **left** (`right = mid - 1`) to check smaller numbers.

**Why this approach is optimal**
By using Binary Search, we reduce the search operations from $N$ to $\log_2(N)$, which is significantly faster for large values of $n$.

**Time & Space Complexity**
* **Time Complexity:** $O(\log N)$, we apply binary search on our search space to reduce it into half at every step.
* **Space Complexity:** $O(1)$, since the algorithm does not use any additional space or data structures.

**Java Code**
```java
class Solution {
    // This function returns the floor value of the square root of a number
    public int mySqrt ( int x) {
        // Handle small numbers directly
        if (x < 2 ) return x;
        // Initialize binary search range
        int left = 1 , right = x / 2 , ans = 0 ;
        // Perform binary search
        while (left <= right) {
            // Find middle point
            long mid = left + (right - left) / 2 ;
            // Check if mid*mid is less than or equal to x
            if (mid * mid <= x) {
                // Store mid as potential answer
                ans = ( int ) mid;
                // Move to right half
                left = ( int ) mid + 1 ;
            } else {
                // Move to left half
                right = ( int ) mid - 1 ;
            }
        }
        // Return final answer
        return ans;
    }
}
public class Main {
    public static void main (String[] args) {
        Solution s = new Solution ();
        System.out.println(s.mySqrt( 8 ));
    }
}
```

---

4. 🔹 **Edge Cases**
* **n = 0 or n = 1:** The square root is the number itself.
* **Perfect Squares:** The algorithm should return the exact integer root (e.g., `sqrt(36) = 6`).
* **Non-Perfect Squares:** The algorithm must return the floor value (e.g., `sqrt(28) = 5`).
* **Large Input:** When `n` is near `Integer.MAX_VALUE`, `mid * mid` will overflow if calculated as an `int`.

---

5. 🔹 **Important Notes / Takeaways**
* **Binary Search on Answers:** This problem is a classic example of applying Binary Search not on an array, but on a range of possible answers (Search Space).
* **Integer Overflow Tip:** Always use `long` for intermediate product calculations like `mid * mid` in square root or power problems.
* **Floor vs. Ceil:** By updating `ans` only when `mid * mid <= n`, we naturally capture the floor value.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---
Q2
# Nth Root of a Number using Binary Search

1. 🔹 **Problem Summary**
Given two numbers **N** and **M**, find the **Nth root of M**. The Nth root of a number $M$ is a value $X$ such that $X^N = M$. If the Nth root is an integer, return it; otherwise, return **-1**.

---

2. 🔹 **Key Observations & Intuition**
* **Monotonicity:** The function $f(X) = X^N$ is monotonically increasing. As $X$ increases, $X^N$ also increases. This property makes the problem suitable for **Binary Search**.
* **Search Space:** Since we are looking for an integer root of $M$, our potential answer must lie in the range $[1, M]$.
* **Overflow Handling:** When calculating $mid^N$, the value can quickly exceed the limits of a `long`. A crucial trick is to stop the multiplication loop as soon as the product exceeds $M$ to prevent overflow and save time.

---

3. 🔹 **Approaches**

### ➤ Brute-Force Approach
**Idea**
To find the nth root of a number m, we want to find a number x such that x^n = m. The naive approach to solve this is to linearly search for every possible number. Using linear search, we start from 1 and gradually try increasing values, checking if raising them to the power n gets us close to or exactly equals m.
* Start a loop from 1 to m for linear search.
* For each value in the loop, compute the value raised to power n.
* If the result equals m, return that value.
* If the result exceeds m, break the loop as the nth root does not exist as an integer.

**Time & Space Complexity**
* **Time Complexity:** $O(M)$, we search for every possible number from 1 to $M$ to check if it is the Nth root.
* **Space Complexity:** $O(1)$, constant additional space is used.

**Java Code**
```java
class Solution {
    // Function to find Nth root of M
    public int nthRoot ( int n, int m) {
        // Loop from 1 to m
        for ( int i = 1 ; i <= m; i++) {
            // Compute i^n
            long power = ( long ) Math.pow(i, n);
            // If equal to m, return i
            if (power == m) return i;
            // If exceeds m, break
            if (power > m) break ;
        }
        // If not found, return -1
        return - 1 ;
    }
}
// Main class
public class Main {
    public static void main (String[] args) {
        Solution sol = new Solution ();
        int n = 3 , m = 27 ;
        // Find nth root
        System.out.println( "Nth Root: " + sol.nthRoot(n, m));
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
To find the N-th root of a number M, instead of checking every number from 1 to M (which is inefficient), we use binary search to efficiently reduce the search space. Since the N-th root lies between 1 and M, we start with a search range from 1 to M. For each middle value in this range, we compute its N-th power by multiplying it with itself N times, without using built-in power functions (to avoid integer overflow). During this multiplication, if the result exceeds M, we stop early to save time. If the final result equals M, we’ve found the N-th root. Otherwise, we adjust our search range accordingly to continue the binary search.

**Why this approach is optimal**
This method significantly speeds up the process by halving the range at each step, moving from a linear time complexity to a logarithmic one ($O(\log M)$).

**Time & Space Complexity**
* **Time Complexity:** $O(\log M)$, we search for every possible number from 1 to $M$ to check if it is the Nth root.
* **Space Complexity:** $O(1)$, constant additional space is used.

**Java Code**
```java
class Solution {
    // Function to find N-th root of M using binary search
    public int nthRoot ( int n, int m) {
        // Set low and high for binary search
        int low = 1 , high = m;
        // Start binary search
        while (low <= high) {
            // Calculate mid
            int mid = (low + high) / 2 ;
            // Store result of mid^n
            long ans = 1 ;
            for ( int i = 0 ; i < n; i++) {
                ans *= mid;
                if (ans > m) break ;
            }
            // If mid^n equals m
            if (ans == m) return mid;
            // If mid^n is less than m
            if (ans < m) low = mid + 1 ;
            // If mid^n is more than m
            else high = mid - 1 ;
        }
        // Return -1 if not found
        return - 1 ;
    }
}
// Main class
public class Main {
    public static void main (String[] args) {
        Solution obj = new Solution ();
        int result = obj.nthRoot( 3 , 27 );
    }
}
```

---

4. 🔹 **Edge Cases**
* **$M = 1$:** The Nth root of 1 is always 1.
* **$N = 1$:** The 1st root of $M$ is $M$ itself.
* **Non-existent Integer Root:** For example, $N=4, M=69$. The algorithm should return -1 correctly.
* **Large $N$ and $M$:** Handled by the manual multiplication loop with an early `break` to avoid `long` overflow.

---

5. 🔹 **Important Notes / Takeaways**
* **Binary Search on Answers:** This is a classic example of searching within a value range rather than an array index.
* **Avoid Built-in `pow`:** In the optimal approach, manual multiplication is preferred to control overflow and performance by stopping early.
* **Interview Insight:** When asked for a "root" or "square root," always check if the search space is sorted to apply Binary Search.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute-Force** | $O(M)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log M)$ | $O(1)$ |

---
Q3
# Koko Eating Bananas

1. 🔹 **Problem Summary**
Koko is given `n` piles of bananas, where the $i^{th}$ pile has `a[i]` bananas. She has `h` hours to eat all of them. Each hour, she chooses a pile and eats `k` bananas. If the pile has fewer than `k` bananas, she eats the whole pile and stops for that hour. The goal is to find the **minimum integer eating speed `k`** such that she can finish all the bananas within `h` hours.

---

2. 🔹 **Key Observations & Intuition**
* **Search Space:** The minimum speed Koko can have is **1** banana/hr. The maximum speed she would ever need is **max(a[])** (the size of the largest pile), because eating faster than the largest pile still requires at least 1 hour per pile.
* **Monotonicity:** If Koko can finish all bananas at speed $k$, she can also finish them at any speed $> k$. If she cannot finish at speed $k$, she won't be able to finish at any speed $< k$. This "True/False" transition point is the classic indicator for **Binary Search on Answers**.
* **The Hour Calculation:** For each pile, the time taken is calculated as $\lceil \text{pile} / \text{speed} \rceil$. In programming, this is effectively `(pile + speed - 1) / speed` or `Math.ceil((double)pile / speed)`.

---

3. 🔹 **Approaches**

### ➤ Brute-Force Approach
**Idea**
The problem is about finding the minimum eating speed such that Koko can finish all bananas within h hours. The extremely naive approach is to check all possible answers from 1 to max(a[]). The minimum number for which the required time is less than or equal to h is our answer.
- Find the largest pile size (max of the array).
- Loop through all possible speeds from 1 to this maximum value.
- For each speed, calculate the total hours needed. For each pile, compute the time as ceil(pile / speed).
- Sum up the hours for all piles.
- If the total hours is less than or equal to the allowed hours, return this speed as the answer.

**Time & Space Complexity**
* **Time Complexity:** $O(n \times \max(a[]))$, since for each possible speed we go through all the piles.
* **Space Complexity:** $O(1)$, since the algorithm does not use any additional space or data structures.

**Java Code**
```java
import java.util.*;

class Solution {
    // Function to calculate total hours for given speed
    public int calculateTotalHours ( int [] a, int hourly) {
        int totalHours = 0 ;
        for ( int pile : a) {
            // Add hours using ceil
            totalHours += ( int )Math.ceil(( double )pile / hourly);
        }
        return totalHours;
    }

    // Function to find minimum eating speed
    public int minEatingSpeed ( int [] a, int h) {
        // Find maximum pile size
        int maxVal = Arrays.stream(a).max().getAsInt();

        // Try every possible speed
        for ( int i = 1 ; i <= maxVal; i++) {
            int hours = calculateTotalHours(a, i);
            // If hours fit within h
            if (hours <= h) {
                return i;
            }
        }
        return maxVal;
    }
}

public class Main {
    public static void main (String[] args) {
        // Input array
        int [] a = { 3 , 6 , 7 , 11 };
        // Hours allowed
        int h = 8 ;
        Solution obj = new Solution ();
        System.out.println(obj.minEatingSpeed(a, h));
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
The naive method checks every speed, which is slow if the piles are large. But the possible answer space (from 1 to the maximum pile size) is sorted, meaning if a certain speed works, then all higher speeds will also work. This allows us to apply Binary Search on the answer space to efficiently find the minimum speed at which Koko can finish the bananas within the given hours.
- First, identify the largest pile size since the eating speed cannot be more than that.
- Set the search range with the lowest speed as 1 and the highest speed as the maximum pile size.
- Use binary search within this range to check possible speeds.
- At each step, take the middle value as the current speed and calculate how many hours it would take to finish all piles at this speed.
- If the total hours are less than or equal to the allowed hours, this speed is a candidate, so try to see if a smaller speed also works by moving left.
- If the total hours exceed the allowed hours, then the speed is too slow, so move right to try higher speeds.
- Continue this process until the range closes, and the smallest valid speed found will be the answer.

**Why this approach is optimal**
Instead of checking every speed linearly, we use Binary Search to find the threshold speed in logarithmic time relative to the maximum pile size.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times \log(\max(a[])))$, we apply binary search on our search space to reduce it into half at every step.
* **Space Complexity:** $O(1)$, since the algorithm does not use any additional space or data structures.

**Java Code**
```java
import java.util.*;

class Solution {
    // Function to calculate total hours at given speed
    private int calculateTotalHours ( int [] piles, int speed) {
        int totalH = 0 ;
        for ( int bananas : piles) {
            totalH += ( int )Math.ceil(( double )bananas / speed);
        }
        return totalH;
    }

    // Function to find minimum eating speed
    public int minEatingSpeed ( int [] piles, int h) {
        // Find maximum element
        int maxPile = Arrays.stream(piles).max().getAsInt();

        // Initialize low and high pointers
        int low = 1 , high = maxPile;
        int ans = maxPile;

        // Binary search on answer space
        while (low <= high) {
            int mid = (low + high) / 2 ;
            int totalH = calculateTotalHours(piles, mid);
            // If possible, try smaller speed
            if (totalH <= h) {
                ans = mid;
                high = mid - 1 ;
            }
            // Otherwise, try larger speed
            else {
                low = mid + 1 ;
            }
        }
        return ans;
    }
}

public class Main {
    public static void main (String[] args) {
        int [] piles = { 3 , 6 , 7 , 11 };
        int h = 8 ;
        Solution obj = new Solution ();
        System.out.println(obj.minEatingSpeed(piles, h));
    }
}
```

---

4. 🔹 **Edge Cases**
* **h == n:** Koko must eat at least at the speed of the largest pile to finish each pile in exactly 1 hour.
* **h is very large:** If `h` is much larger than the total number of bananas, the answer will likely be 1.
* **Large pile values:** If piles have bananas up to $10^9$, ensure `totalHours` is stored in a `long` to prevent overflow (though the editorial uses `int`, in many competitive platforms `long` is safer).
* **All piles are the same size:** The speed will simply be the value that satisfies $\lceil \text{size} / \text{speed} \rceil \times n \le h$.

---

5. 🔹 **Important Notes / Takeaways**
* **Pattern:** This is a classic "Binary Search on Answer" problem. Look for a range of possible answers and a monotonic condition.
* **Math Trick:** Using `Math.ceil((double)bananas / speed)` is fine, but in interviews, you can also use `(bananas + speed - 1) / speed` for integer-only division to avoid precision issues.
* **Range:** Always identify your `low` and `high` carefully. Here, `low = 1` and `high = max(piles)`.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N \times \max(a[]))$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(N \times \log(\max(a[])))$ | $O(1)$ |

---
Q4
# Minimum days to make M bouquets

1. 🔹 **Problem Summary**
You are given $N$ roses and an array `bloomDays[]` where `bloomDays[i]` is the day the $i^{th}$ rose blooms. To make one bouquet, you need exactly $k$ **adjacent** bloomed roses. Your task is to find the **minimum number of days** required to make at least $m$ bouquets. If it is impossible to make $m$ bouquets even after all roses have bloomed, return -1.

---

2. 🔹 **Key Observations & Intuition**
* **Total Flowers Needed:** To make $m$ bouquets of $k$ flowers each, you need at least $m \times k$ flowers. if $m \times k > N$, it's immediately impossible.
* **Search Space:** The answer must lie between the minimum bloom day and the maximum bloom day in the array.
* **Monotonicity:** If it is possible to make $m$ bouquets on day $D$, it will definitely be possible on any day $> D$. If it's impossible on day $D$, it's impossible on any day $< D$. This "step-function" property indicates that the search space is monotonic, making **Binary Search** the optimal choice.
* **Adjacency Constraint:** When counting flowers on a specific day, you must count consecutive flowers. If a flower hasn't bloomed yet, it breaks the current streak.

---

3. 🔹 **Approaches**

### ➤ Brute Force Approach
**Idea**
* If the total number of flowers required to make all bouquets is more than the flowers available, it is not possible to make the bouquets. So, return -1.
* Loop through each day starting from the earliest bloom day to the latest bloom day to test all possible answers.
* For each day, check if it's possible to make the required number of bouquets using the flowers that have bloomed by that day. If yes, return that day as the answer.
* If no suitable day is found after checking all possibilities, it means it's impossible to make the bouquets. So, return -1.

**Time & Space Complexity**
* **Time Complexity:** $O((\max(arr[])-\min(arr[])+1) * N)$, where $\max(arr[])$ is the maximum element, $\min(arr[])$ is the minimum, and $N$ is the size of the array.
* **Space Complexity:** $O(1)$ as we are not using any extra space.

**Java Code**
```java
import java.util.*;

public class RoseGarden {
    // Function to check if it's possible to make 'm' bouquets on 'day'
    public boolean isPossible(int[] bloomDays, int day, int m, int k) {
        int count = 0; // count of consecutive bloomed flowers
        int bouquets = 0;
        for (int bloom : bloomDays) {
            if (bloom <= day) {
                count++;
                if (count == k) {
                    bouquets++;
                    count = 0;
                }
            } else {
                count = 0;
            }
        }
        return bouquets >= m;
    }

    // Main function to return minimum day to make 'm' bouquets
    public int minDaysToMakeBouquets(int[] bloomDays, int m, int k) {
        long totalFlowers = (long) m * k;
        if (totalFlowers > bloomDays.length) return -1;
        int min = Arrays.stream(bloomDays).min().getAsInt();
        int max = Arrays.stream(bloomDays).max().getAsInt();

        for (int day = min; day <= max; day++) {
            if (isPossible(bloomDays, day, m, k)) {
                return day;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] bloomDays = {7, 7, 7, 7, 13, 11, 12, 7};
        int k = 3;
        int m = 2;
        RoseGarden garden = new RoseGarden();
        int result = garden.minDaysToMakeBouquets(bloomDays, m, k);
        if (result == -1)
            System.out.println("We cannot make m bouquets.");
        else
            System.out.println("We can make bouquets on day " + result);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
The brute force checks every single day, which is inefficient. Since the "possibility" of making bouquets increases as days pass, we can use Binary Search.
* Define `low` as the minimum bloom day and `high` as the maximum bloom day.
* Calculate `mid` day and use the `isPossible` function.
* If `isPossible` is true for `mid`, it might be our answer, but we look for a smaller (minimum) day by moving `high = mid - 1`.
* If `isPossible` is false, we need more days, so move `low = mid + 1`.

**Why this approach is optimal**
It reduces the search space logarithmically ($O(\log(\text{Range}))$) instead of checking every day linearly, making it much faster for large bloom day values.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times \log(\max(arr[]) - \min(arr[]) + 1))$, where $N$ is the size of the array.
* **Space Complexity:** $O(1)$ as we are not using any extra space.

**Java Code**
```java
import java.util.*;

public class RoseGarden {
    // Function to check if it's possible to make m bouquets on or before 'day'
    public static boolean isPossible(int[] bloomDays, int day, int m, int k) {
        int count = 0; // counts consecutive flowers that bloomed on or before 'day'
        int bouquets = 0; // number of bouquets made
        for (int bloom : bloomDays) {
            if (bloom <= day) {
                count++; // flower is ready
                if (count == k) {
                    bouquets++; // form one bouquet
                    count = 0; // reset count for next bouquet
                }
            } else {
                count = 0; // break in consecutive flowers
            }
        }
        return bouquets >= m; // check if required bouquets can be made
    }

    // Main function to find minimum day to make m bouquets
    public static int roseGarden(int[] bloomDays, int k, int m) {
        long required = (long) m * k;
        if (required > bloomDays.length) return -1; // not enough flowers

        int minDay = Integer.MAX_VALUE;
        int maxDay = Integer.MIN_VALUE;
        // Find the minimum and maximum bloom day
        for (int bloom : bloomDays) {
            minDay = Math.min(minDay, bloom);
            maxDay = Math.max(maxDay, bloom);
        }

        // Binary search between minDay and maxDay
        int low = minDay, high = maxDay, result = -1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (isPossible(bloomDays, mid, m, k)) {
                result = mid; // possible to form bouquets, try earlier
                high = mid - 1;
            } else {
                low = mid + 1; // need more days
            }
        }
        return result;
    }

    public static void main(String[] args) {
        int[] bloomDays = {7, 7, 7, 7, 13, 11, 12, 7};
        int k = 3;
        int m = 2;
        int result = roseGarden(bloomDays, k, m);
        if (result == -1)
            System.out.println("We cannot make m bouquets.");
        else
            System.out.println("We can make bouquets on day " + result);
    }
}
```

---

4. 🔹 **Edge Cases**
* **Insufficient Flowers:** If $m \times k > bloomDays.length$, return -1.
* **$k=1$:** Every bloomed flower can be a bouquet.
* **All bloom days are the same:** The answer will be that specific day (if $m \times k \le N$).
* **$m=1$:** Just need $k$ consecutive bloomed flowers.

---

5. 🔹 **Important Notes / Takeaways**
* **Binary Search on Answer:** This is a classic pattern. When the answer has a range and a clear "Yes/No" threshold, use Binary Search.
* **Long for Multiplication:** When checking $m \times k$, always cast to `long` to avoid integer overflow in languages like Java/C++.
* **Adjacency Logic:** The `count = 0` inside the `else` block is the crucial part of checking adjacency.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N \times (\text{Max Day} - \text{Min Day}))$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(N \times \log(\text{Max Day} - \text{Min Day}))$ | $O(1)$ |

---
Q5
# Find the Smallest Divisor Given a Threshold

1. 🔹 **Problem Summary**
You are given an array of integers `arr` and a threshold value `limit`. You need to find the **smallest positive integer divisor** such that when every element in the array is divided by it (and the result is rounded up to the nearest integer), the **sum** of these results is less than or equal to the `limit`.

---

2. 🔹 **Key Observations & Intuition**
* **Ceiling Division:** The problem requires the ceiling of the division ($\lceil arr[i] / d \rceil$).
* **Range of Divisors:** The smallest possible divisor is **1** (yielding the maximum sum), and the largest effective divisor is the **maximum element in the array** (yielding a sum equal to the number of elements, as each division results in 1).
* **Monotonicity:** As the divisor increases, the sum of the divisions decreases or stays the same. This inverse relationship between the divisor and the sum allows us to use **Binary Search on Answers**.
* **Impossible Case:** If the number of elements in the array is greater than the limit, it's impossible to find a divisor because even with the largest possible divisor, each element results in at least 1, making the minimum sum equal to the array length.

---

3. 🔹 **Approaches**

### ➤ Brute Force
**Idea**
* We will run a loop from 1 to max element of the array to check all possible divisors.
* To calculate the result, we will iterate over the given array using a loop. Within this loop, we will divide each element in the array by the current divisor, and sum up the obtained ceiling values.
* Inside the outer loop, If result <= threshold: We will return d as our answer.
* Finally, if we are outside the nested loops, we will return -1.

**Time & Space Complexity**
* **Time Complexity:** $O(\max(arr[]) \times N)$, where $\max(arr[])$ is the maximum element in the array and $N$ is the size of the array.
* **Space Complexity:** $O(1)$. No extra space used.

**Java Code**
```java
class Solution {
    // Method to find the smallest divisor such that the sum of ceiling divisions <= limit
    public int smallestDivisor ( int [] arr, int limit) {
        int n = arr.length;
        // Find the maximum element in the array
        int max = Integer.MIN_VALUE;
        for ( int num : arr) {
            max = Math.max(max, num);
        }
        // Try all possible divisors from 1 to max
        for ( int d = 1 ; d <= max; d++) {
            int sum = 0 ;
            for ( int i = 0 ; i < n; i++) {
                // Divide each number by d and take the ceiling
                sum += ( int ) Math.ceil(( double ) arr[i] / d);
            }
            // If the total sum is within the limit, return this divisor
            if (sum <= limit) {
                return d;
            }
        }
        return - 1 ; // No valid divisor found
    }
}
public class Main {
    public static void main (String[] args) {
        int [] arr = { 1 , 2 , 3 , 4 , 5 };
        int limit = 8 ;
        Solution obj = new Solution ();
        int ans = obj.smallestDivisor(arr, limit);
        System.out.println( "The minimum divisor is: " + ans);
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
We use the **Binary Search** algorithm to optimize the search for the divisor. Since the sum changes monotonically with the divisor, we don't need to check every single value.
* First, check if the number of elements is already greater than the allowed limit. If so, return -1.
* Identify the search range: `low = 1` and `high = max(arr)`.
* In each step of binary search, calculate `mid`.
* Calculate the sum of ceiling divisions using `mid`.
* If `sum <= limit`, then `mid` is a possible answer, but we look for a **smaller** one in the left half (`high = mid - 1`).
* If `sum > limit`, the divisor is too small, so we look in the right half (`low = mid + 1`).

**Why this approach is optimal**
It reduces the search space from linear ($O(M)$) to logarithmic ($O(\log M)$), significantly speeding up the process for large arrays and large values.

**Time & Space Complexity**
* **Time Complexity:** $O(\log(\max(arr[])) \times N)$.
* **Space Complexity:** $O(1)$, no extra space is used.

**Java Code**
```java
import java.util.*;

class SmallestDivisorFinder {
    // Helper method to calculate sum by divisor
    private int sumByD ( int [] arr, int div) {
        int sum = 0 ;
        for ( int num : arr) {
            sum += Math.ceil(( double ) num / div);
        }
        return sum;
    }
    // Method to find the smallest divisor using binary search
    public int smallestDivisor ( int [] arr, int limit) {
        if (arr.length > limit) return - 1 ;
        int low = 1 ;
        int high = Arrays.stream(arr).max().getAsInt();
        while (low <= high) {
            int mid = (low + high) / 2 ;
            if (sumByD(arr, mid) <= limit) {
                high = mid - 1 ; // Try smaller divisor
            } else {
                low = mid + 1 ; // Try larger divisor
            }
        }
        return low;
    }
    public static void main (String[] args) {
        SmallestDivisorFinder solver = new SmallestDivisorFinder ();
        int [] arr = { 1 , 2 , 3 , 4 , 5 };
        int limit = 8 ;
        int result = solver.smallestDivisor(arr, limit);
        System.out.println( "The minimum divisor is: " + result);
    }
}
```

---

4. 🔹 **Edge Cases**
* **limit < arr.length:** Impossible to satisfy, returns -1.
* **limit == arr.length:** The divisor will be the maximum element in the array.
* **Array with all identical elements:** The divisor will be determined by the ceiling of the threshold division.
* **Maximum limit:** If the limit is very high, the smallest divisor will be 1.

---

5. 🔹 **Important Notes / Takeaways**
* **Binary Search on Answers:** This is a core pattern in DSA where you search for a value that satisfies a condition within a known range.
* **Ceiling Function Trick:** In interviews, you can also compute the ceiling as `(num + div - 1) / div` using integer arithmetic to avoid `double` precision issues.
* **Range Identification:** Always pick the tightest possible range (`low` and `high`) to make the search efficient.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(\max(arr[]) \times N)$ | $O(1)$ |
| **Optimal Approach** | $O(\log(\max(arr[])) \times N)$ | $O(1)$ |

---

Q6 
# Capacity to Ship Packages within D Days

1. 🔹 **Problem Summary**
You own a shipment company and need to transport packages of various weights across a conveyor belt within a specific number of days ($d$). The packages must be loaded in the exact order they appear in the array. You need to find the **minimum weight capacity** of the ship required to ensure all packages are delivered within the $d$-day deadline.

---

2. 🔹 **Key Observations & Intuition**
* **Minimum Possible Capacity:** The ship must be able to carry the heaviest single package. Therefore, the minimum capacity is $\max(weights)$.
* **Maximum Possible Capacity:** If you ship all packages in exactly one day, the capacity would be $\sum weights$.
* **Monotonicity:** If a capacity $C$ allows you to ship everything within $d$ days, any capacity greater than $C$ will also work. If capacity $C$ fails, any capacity less than $C$ will also fail. This allows us to use **Binary Search on the Answer Space** $[ \max(weights), \sum weights ]$.
* **Order Constraint:** You cannot sort the weights because they must be loaded in the given order.

---

3. 🔹 **Approaches**

### ➤ Brute Force Approach
**Idea**
The problem asks to find the minimum capacity of the ship such that all packages can be shipped within d days. A brute force way is to check every capacity starting from the maximum single package weight (since capacity can't be less than the heaviest package) up to the sum of all package weights (which guarantees all packages shipped in one day). For each capacity, simulate the shipping process day by day. The smallest capacity that ships all packages in ≤ d days is the answer.
* Find the maximum weight in the array (minimum capacity possible).
* Calculate the sum of all weights (maximum capacity possible).
* For each capacity from max weight to sum:
    * Simulate shipping: load packages one by one until capacity is reached, then move to next day.
    * If total days used is ≤ d, return that capacity.

**Time & Space Complexity**
* **Time Complexity:** $O((\text{sum\_weights} - \text{max\_weight}) \times N)$, where $N$ is the number of packages.
* **Space Complexity:** $O(1)$, only constant extra space is used.

**Java Code**
```java
import java.util.*;

class Solution {
    // Function to check how many days needed for given capacity
    int daysNeeded ( int [] weights, int capacity) {
        // Initialize day count to 1
        int days = 1 ;
        // Current load for the day
        int currentLoad = 0 ;
        // Iterate over all package weights
        for ( int w : weights) {
            // If adding weight exceeds capacity
            if (currentLoad + w > capacity) {
                // Increase day count and reset load
                days++;
                currentLoad = w;
            } else {
                // Otherwise, add weight to current load
                currentLoad += w;
            }
        }
        // Return total days needed
        return days;
    }

    // Function to find minimum ship capacity to ship in d days
    int shipWithinDays ( int [] weights, int d) {
        // Find maximum weight as minimum capacity
        int left = Arrays.stream(weights).max().getAsInt();
        // Find total sum as maximum capacity
        int right = Arrays.stream(weights).sum();

        // Iterate from minimum to maximum capacity
        for ( int capacity = left; capacity <= right; capacity++) {
            // Calculate days needed for current capacity
            int needed = daysNeeded(weights, capacity);
            // If days needed are less than or equal to d, return capacity
            if (needed <= d) {
                return capacity;
            }
        }
        // Should never reach here given constraints
        return right;
    }
}

public class Main {
    public static void main (String[] args) {
        // Input weights
        int [] weights = { 5 , 4 , 5 , 2 , 3 , 4 , 5 , 6 };
        // Days to ship
        int d = 5 ;
        // Create Solution instance
        Solution sol = new Solution ();
        // Call the function and print result
        System.out.println(sol.shipWithinDays(weights, d));
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
We want to find the minimum ship capacity that allows shipping all packages within the given number of days. The capacity must be at least the heaviest package because you can’t split a package. At the same time, the capacity can be at most the sum of all packages (if you ship everything in one day). So the answer lies between these two extremes.

Using binary search on this range lets us efficiently find the smallest capacity that works. For each candidate capacity, we check if it’s possible to ship all packages within the given days by greedily accumulating package weights until we reach capacity, then moving to the next day.
* Set the lower bound as the maximum weight in the packages.
* Set the upper bound as the sum of all package weights.
* While the lower bound is less than or equal to the upper bound, do:
    * Pick the middle value as the candidate capacity.
    * Simulate shipping: if the number of days used is within the allowed days, move the upper bound down to try smaller capacities.
    * Otherwise, increase the lower bound to try larger capacities.

**Why this approach is optimal**
Instead of a linear search through the capacity range, Binary Search reduces the number of checks to logarithmic time ($O(\log(\text{Sum} - \text{Max}))$, making it significantly faster for large weight sums.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times \log(\text{sum\_weights} - \text{max\_weight}))$, where $N$ is the number of packages.
* **Space Complexity:** $O(1)$, constant extra space used.

**Java Code**
```java
import java.util.*;

class Solution {
    // Function to calculate how many days are needed to ship
    // all packages with the given ship capacity
    int daysNeeded ( int [] weights, int capacity) {
        // Initialize count of days to 1
        int days = 1 ;
        // Initialize current load on ship to 0
        int currentLoad = 0 ;
        // Iterate over all package weights
        for ( int w : weights) {
            // Check if adding current package exceeds capacity
            if (currentLoad + w > capacity) {
                // If yes, increase days count since we start a new day
                days++;
                // Reset current load to current package weight
                currentLoad = w;
            } else {
                // Else, add current package weight to current load
                currentLoad += w;
            }
        }
        // Return total days required
        return days;
    }

    // Function to find minimum ship capacity to ship all packages within d days
    int shipWithinDays ( int [] weights, int d) {
        // Calculate minimum capacity as max weight in packages
        int left = Arrays.stream(weights).max().getAsInt();
        // Calculate maximum capacity as sum of all weights
        int right = Arrays.stream(weights).sum();

        // Binary search between left and right capacity values
        while (left < right) {
            // Calculate mid value to test
            int mid = left + (right - left) / 2 ;
            // Calculate how many days needed for capacity mid
            int needed = daysNeeded(weights, mid);
            // If days needed is less or equal to allowed days,
            // try to find smaller capacity on left side
            if (needed <= d) {
                right = mid;
            } else {
                // Else, need more capacity, search on right side
                left = mid + 1 ;
            }
        }
        // Return minimum capacity found
        return left;
    }
}

public class Main {
    public static void main (String[] args) {
        // Define array of package weights
        int [] weights = { 5 , 4 , 5 , 2 , 3 , 4 , 5 , 6 };
        // Define number of days allowed for shipping
        int d = 5 ;
        // Create Solution object
        Solution sol = new Solution ();
        // Print minimum capacity required to ship within d days
        System.out.println(sol.shipWithinDays(weights, d));
    }
}
```

---

4. 🔹 **Edge Cases**
* **$d = 1$:** The capacity must be the sum of all weights.
* **$d = \text{weights.length}$:** The capacity must be at least the maximum single weight in the array.
* **All weights are the same:** The capacity will be a multiple of the weight based on $d$.
* **Single package:** The capacity is just the weight of that package.

---

5. 🔹 **Important Notes / Takeaways**
* **Binary Search on Answers:** Whenever the answer space is bounded and monotonic (if $x$ works, $x+1$ also works), think Binary Search.
* **Range Selection:** A common mistake is starting `left` at $0$ or $1$. It must start at $\max(weights)$ because you cannot ship a package that is heavier than the ship's total capacity.
* **Greedy Simulation:** The helper function `daysNeeded` uses a greedy approach, which works because we must ship packages in the order they appear.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O((\sum W - \max W) \times N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(N \times \log(\sum W - \max W))$ | $O(1)$ |

---

Q7 

# Kth Missing Positive Number

1. 🔹 **Problem Summary**
Given a strictly increasing array `vec` of positive integers and an integer `k`, find the $k^{th}$ positive integer that is missing from the array.

---

2. 🔹 **Key Observations & Intuition**
* **The "Ideal" Array:** In an array with no missing numbers, the value at index `i` should be `i + 1`.
* **Counting Missing Numbers:** For any index `mid`, the number of missing integers before it can be calculated as: 
  `missing = vec[mid] - (mid + 1)`.
* **Monotonicity:** As we move right in the array, the count of missing numbers only stays the same or increases. This sorted property of "missing counts" allows us to use **Binary Search**.
* **Relationship at the End:** After Binary Search, the $k^{th}$ missing number lies between `vec[high]` and `vec[low]`. The formula for the result simplifies to `k + high + 1` (or `k + low`).

---

3. 🔹 **Approaches**

### ➤ Brute Force Approach
**Idea**
- We will use a loop to traverse the array.
- Inside the loop,
- If vec[i] <= k: we will simply increase the value of k by 1.
- Otherwise, we will break out of the loop.
- Finally, we will return the value of k.

**Time & Space Complexity**
* **Time Complexity:** $O(N)$, where $N =$ size of the given array.
* **Space Complexity:** $O(1)$, no extra space used.

**Java Code**
```java
import java.util.*;

class MissingKFinder {
    // Method to find the k-th missing number
    public int missingK ( int [] vec, int k) {
        for ( int i = 0 ; i < vec.length; i++) {
            if (vec[i] <= k) {
                k++; // Skip current number and adjust k
            } else {
                break ; // Stop if current number is greater than k
            }
        }
        return k;
    }

    public static void main (String[] args) {
        int [] vec = { 4 , 7 , 9 , 10 }; // Sorted array
        int k = 4 ; // We want the 4th missing number
        MissingKFinder finder = new MissingKFinder ();
        int ans = finder.missingK(vec, k); // Call method
        System.out.println( "The missing number is: " + ans); // Output result
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
We cannot apply binary search on the answer space here as we cannot assure which missing number has the possibility of being the kth missing number. That is why, we will do something different here. We will try to find the closest neighbors (i.e. Present in the array) for the kth missing number by counting the number of missing numbers for each element in the given array.
- Start by setting two markers: one at the beginning and one at the end of the list.
- Keep checking the middle position between the two markers by taking their average.
- Count how many numbers are missing up to that middle position by subtracting the expected number from the actual number found at that point.
- If the number of missing values is less than the desired position, move your focus to the right side of the list by shifting the beginning marker ahead.
- If not, move your focus to the left side by shifting the end marker backward.
- Once you've narrowed down the search and exited the loop, return the final answer by adding the desired position to the last marker you checked (plus one).

**Why this approach is optimal**
Instead of a linear scan, Binary Search allows us to find the gap where the $k^{th}$ missing number resides in $O(\log N)$ time, making it highly efficient for large datasets.

**Time & Space Complexity**
* **Time Complexity:** $O(\log N)$, used for typical binary search.
* **Space Complexity:** $O(1)$, no extra space used.

**Java Code**
```java
import java.util.*;

class MissingKFinder {
    // Function to return the k-th missing number
    public int missingK ( int [] vec, int k) {
        int low = 0 , high = vec.length - 1 ;
        // Binary search loop
        while (low <= high) {
            int mid = (low + high) / 2 ;
            // Number of missing elements before index mid
            int missing = vec[mid] - (mid + 1 );
            if (missing < k) {
                low = mid + 1 ; // Move right
            } else {
                high = mid - 1 ; // Move left
            }
        }
        // Final result after binary search
        return k + high + 1 ;
    }

    public static void main (String[] args) {
        int [] vec = { 4 , 7 , 9 , 10 };
        int k = 4 ;
        MissingKFinder finder = new MissingKFinder ();
        int ans = finder.missingK(vec, k);

        System.out.println( "The missing number is: " + ans);
    }
}
```

---

4. 🔹 **Edge Cases**
* **k is smaller than the first element:** If `vec = [5, 6, 7]` and `k = 2`, the answer is 2. (Handled: loop breaks immediately or `high` stays -1).
* **k is larger than all missing numbers within the range:** If `vec = [1, 2, 3]` and `k = 2`, the answer is 5. (Handled: `low` moves past the end of the array).
* **Empty Array:** (Though the problem usually specifies a non-empty array).
* **Array with no gaps:** `vec = [1, 2, 3, 4]`.

---

5. 🔹 **Important Notes / Takeaways**
* **The "Shift" Logic:** In the Brute Force, we shift `k` for every number we encounter that is $\le$ current `k`. This is a very clever way to solve it linearly.
* **Binary Search Criterion:** The key is to binary search on the **index** based on the **number of missing elements** before that index.
* **Final Formula:** `ans = vec[high] + (k - missing_at_high)`. This simplifies mathematically to `k + high + 1`.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log N)$ | $O(1)$ |

---

# [Aggressive Cows : Detailed Solution](https://takeuforward.org/data-structure/aggressive-cows-detailed-solution?mode=track&sheet=a2z-dsa)

1. 🔹 **Problem Summary**
You are given an array `arr` of size `n` which denotes the position of stalls. You are also given an integer `k` which denotes the number of aggressive cows. You need to assign stalls to these `k` cows such that the **minimum distance between any two of them is the maximum possible**.

---

2. 🔹 **Key Observations & Intuition**
* **The Goal:** We need to maximize the minimum distance. This is a classic "Min-Max" problem frequently solved using Binary Search on the answer space.
* **Sorting:** To easily calculate distances and place cows greedily, the stall positions must be sorted.
* **Monotonicity:** If we can place cows with a minimum distance of $d$, we can also place them with any distance $< d$. If we cannot place them with distance $d$, we certainly cannot place them with any distance $> d$.
* **Search Space:**
    * **Minimum possible distance:** 1.
    * **Maximum possible distance:** (Max stall position - Min stall position).

---

3. 🔹 **Approaches**

### ➤ Brute Force Approach
**Idea**
The basic idea is to test every possible distance between 1 and the difference between the farthest and nearest stalls. The largest distance for which `canWePlace()` returns true will be our answer.
1.  Sort the stalls array in increasing order.
2.  Use a loop to check every possible distance one by one.
3.  For each distance, call the `canWePlace()` function to see if all cows can be placed:
    * If `canWePlace()` returns false for a distance, return the previous distance (current distance - 1).
    * If the loop finishes without failure, return the largest possible distance.

**Time & Space Complexity**
* **Time Complexity:** $O(N\log N) + O(N \times (\max(stalls[]) - \min(stalls[])))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*; // Class to solve the Aggressive Cows problem 
class Solution { // Function to check if cows can be placed with min distance d 
public boolean canPlace ( int [] stalls, int cows, int d) { // Place the first cow at the first stall 
int count = 1 ; int lastPos = stalls[ 0 ]; // Try placing the remaining cows 
for ( int i = 1 ; i < stalls.length; i++) { // If current stall is at least 'd' away from last cow 
if (stalls[i] - lastPos >= d) { // Place a cow here 
count++;
                lastPos = stalls[i];
            } // If all cows placed, return true 
if (count >= cows) return true ;
        } // Not possible to place all cows 
return false ;
    } // Function to find maximum minimum distance using brute force 
public int aggressiveCows ( int [] stalls, int cows) { // Step 1: Sort stall positions 
Arrays.sort(stalls); // Step 2: Get the maximum possible distance 
int maxDist = stalls[stalls.length - 1 ] - stalls[ 0 ]; // Step 3: Variable to store answer 
int ans = 0 ; // Step 4: Try all possible distances 
for ( int d = 1 ; d <= maxDist; d++) { // If cows can be placed with distance d 
if (canPlace(stalls, cows, d)) { // Update answer 
ans = d;
            }
        } // Step 5: Return the maximum valid distance 
return ans;
    }
} // Driver class 
public class Main { public static void main (String[] args) { // Example input 
int [] stalls = { 1 , 2 , 8 , 4 , 9 }; int cows = 3 ; // Create object and call function 
Solution obj = new Solution ();
        System.out.println(obj.aggressiveCows(stalls, cows));
    }
}
```

---

### ➤ Optimal Approach
**Detailed Explanation**
We use **Binary Search** to optimize the solution by reducing the answer space in half each time. The main idea of Binary Search is to determine which half of the search space can be eliminated based on a specific condition, thus minimizing unnecessary checks.
* **Sort the stalls:** Arrange positions in ascending order.
* **Set the range:** `low = 1`, `high = stalls[n-1] - stalls[0]`.
* **Binary Search:**
    * Pick `mid` as a potential minimum distance.
    * **If `canPlace(mid)` is true:** It means we can achieve at least this distance. We store `mid` as a potential answer and try for a larger distance by moving `low = mid + 1`.
    * **If `canPlace(mid)` is false:** The distance is too large to accommodate `k` cows. We try smaller distances by moving `high = mid - 1`.

**Why this approach is optimal**
Instead of a linear scan of the distance range, we use the logarithmic efficiency of Binary Search. This is essential when the coordinate range (max distance) is very large.

**Time & Space Complexity**
* **Time Complexity:** $O(N\log N) + O(N \times \log(\max(stalls[]) - \min(stalls[])))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*; // Class to solve Aggressive Cows 
class Solution { // Function to check if cows can be placed with distance d 
public boolean canPlace ( int [] stalls, int cows, int d) { // Place first cow at first stall 
int count = 1 ; int lastPos = stalls[ 0 ]; // Loop through stalls 
for ( int i = 1 ; i < stalls.length; i++) { // If stall is at least d away from last placed cow 
if (stalls[i] - lastPos >= d) { // Place cow here 
count++; // Update last position 
lastPos = stalls[i];
            } // If all cows are placed successfully 
if (count >= cows) return true ;
        } // Could not place all cows 
return false ;
    } // Function to maximize minimum distance 
public int aggressiveCows ( int [] stalls, int cows) { // Sort stalls 
Arrays.sort(stalls); // Define search space 
int low = 1 ; int high = stalls[stalls.length - 1 ] - stalls[ 0 ]; int ans = 0 ; // Binary search 
while (low <= high) { // Find mid distance 
int mid = low + (high - low) / 2 ; // If placement possible 
if (canPlace(stalls, cows, mid)) { // Store answer 
ans = mid; // Try bigger distance 
low = mid + 1 ;
            } else { // Try smaller distance 
high = mid - 1 ;
            }
        } // Return result 
return ans;
    }
} // Driver class 
public class Main { public static void main (String[] args) { // Input stalls 
int [] stalls = { 1 , 2 , 8 , 4 , 9 }; // Number of cows 
int cows = 3 ; // Create object 
Solution obj = new Solution (); // Print result 
System.out.println(obj.aggressiveCows(stalls, cows));
    }
}
```

---

4. 🔹 **Edge Cases**
* **$k=2$:** The answer is simply the maximum distance (distance between the two ends).
* **Cows = Stalls:** The answer is the minimum distance between any two adjacent stalls in the sorted array.
* **Large Coordinates:** Coordinates can be up to $10^9$, making the brute force $O(N \times 10^9)$ impossible; Binary Search is required.

---

5. 🔹 **Important Notes / Takeaways**
* **Maximize the Minimum:** This phrasing is a huge hint for Binary Search on Answers.
* **Greedy Placement:** In `canPlace()`, we always place the first cow at the first available stall to maximize the remaining space.
* **Range Definition:** The `high` value of the search space can be simplified to `stalls[n-1] - stalls[0]`.

---

6. 🔹 **Complexity Summary Table**

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N\log N) + O(N \times \text{Range})$ | $O(1)$ |
| **Optimal Approach** | $O(N\log N) + O(N \times \log(\text{Range}))$ | $O(1)$ |

--- 

Q8

# Aggressive Cows

### 1. 🔹 Problem Summary
You are given an array of stall positions and a specific number of cows ($k$). The goal is to place all $k$ cows in the available stalls such that the **minimum distance between any two cows is as large as possible**. Essentially, you are maximizing the minimum gap.

---

### 2. 🔹 Key Observations & Intuition
* **Sorting is Essential:** To easily calculate distances between cows, the stall positions must be in increasing order.
* **The Search Space:** The smallest possible "minimum distance" is **1**, and the largest possible is the distance between the first and last stall (**max - min**).
* **Monotonicity:** If it is possible to place cows with a minimum distance of $d$, it is also possible for any distance less than $d$. If it's impossible for $d$, it's impossible for any distance greater than $d$. This "Yes/No" pattern allows us to use Binary Search.
* **Greedy Placement:** To check if a distance $d$ is feasible, always place the first cow in the first stall and then place the next cow in the first available stall that is at least $d$ units away.

---

### 3. 🔹 Approaches

#### ➤ Brute Force
**Idea**
The basic idea is to test every possible distance between 1 and the difference between the farthest and nearest stalls. The largest distance for which `canWePlace()` returns true will be our answer.

**Time & Space Complexity**
* **Time Complexity:** $O(N \log N) + O(N \times (\max(stalls[]) - \min(stalls[])))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*; // Class to solve the Aggressive Cows problem 
class Solution { // Function to check if cows can be placed with min distance d 
    public boolean canPlace ( int [] stalls, int cows, int d) { // Place the first cow at the first stall 
        int count = 1 ; int lastPos = stalls[ 0 ]; // Try placing the remaining cows 
        for ( int i = 1 ; i < stalls.length; i++) { // If current stall is at least 'd' away from last cow 
            if (stalls[i] - lastPos >= d) { // Place a cow here 
                count++;
                lastPos = stalls[i];
            } // If all cows placed, return true 
            if (count >= cows) return true ;
        } // Not possible to place all cows 
        return false ;
    } // Function to find maximum minimum distance using brute force 
    public int aggressiveCows ( int [] stalls, int cows) { // Step 1: Sort stall positions 
        Arrays.sort(stalls); // Step 2: Get the maximum possible distance 
        int maxDist = stalls[stalls.length - 1 ] - stalls[ 0 ]; // Step 3: Variable to store answer 
        int ans = 0 ; // Step 4: Try all possible distances 
        for ( int d = 1 ; d <= maxDist; d++) { // If cows can be placed with distance d 
            if (canPlace(stalls, cows, d)) { // Update answer 
                ans = d;
            }
        } // Step 5: Return the maximum valid distance 
        return ans;
    }
} // Driver class 
public class Main { public static void main (String[] args) { // Example input 
        int [] stalls = { 1 , 2 , 8 , 4 , 9 }; int cows = 3 ; // Create object and call function 
        Solution obj = new Solution ();
        System.out.println(obj.aggressiveCows(stalls, cows));
    }
}
```

---

#### ➤ Optimal Approach
**Detailed Explanation**
We use **Binary Search** to optimize the solution by reducing the answer space in half each time. The answer space is sorted (from 1 to the max possible distance). By picking a middle distance (`mid`), we check if it's possible to place the cows. If it is, we discard the smaller half and try for a larger distance; otherwise, we search in the smaller half.

**Why this approach is optimal**
Instead of checking every single distance linearly (which could be very large), Binary Search reduces the number of checks to $\log(\text{range})$.

**Time & Space Complexity**
* **Time Complexity:** $O(N \log N) + O(N \times \log(\max(stalls[]) - \min(stalls[])))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*; // Class to solve Aggressive Cows 
class Solution { // Function to check if cows can be placed with distance d 
    public boolean canPlace ( int [] stalls, int cows, int d) { // Place first cow at first stall 
        int count = 1 ; int lastPos = stalls[ 0 ]; // Loop through stalls 
        for ( int i = 1 ; i < stalls.length; i++) { // If stall is at least d away from last placed cow 
            if (stalls[i] - lastPos >= d) { // Place cow here 
                count++; // Update last position 
                lastPos = stalls[i];
            } // If all cows are placed successfully 
            if (count >= cows) return true ;
        } // Could not place all cows 
        return false ;
    } // Function to maximize minimum distance 
    public int aggressiveCows ( int [] stalls, int cows) { // Sort stalls 
        Arrays.sort(stalls); // Define search space 
        int low = 1 ; int high = stalls[stalls.length - 1 ] - stalls[ 0 ]; int ans = 0 ; // Binary search 
        while (low <= high) { // Find mid distance 
            int mid = low + (high - low) / 2 ; // If placement possible 
            if (canPlace(stalls, cows, mid)) { // Store answer 
                ans = mid; // Try bigger distance 
                low = mid + 1 ;
            } else { // Try smaller distance 
                high = mid - 1 ;
            }
        } // Return result 
        return ans;
    }
} // Driver class 
public class Main { public static void main (String[] args) { // Input stalls 
        int [] stalls = { 1 , 2 , 8 , 4 , 9 }; // Number of cows 
        int cows = 3 ; // Create object 
        Solution obj = new Solution (); // Print result 
        System.out.println(obj.aggressiveCows(stalls, cows));
    }
}
```

---

### 4. 🔹 Edge Cases
* **$k = 2$:** The answer will always be the distance between the first and last stall after sorting.
* **Stalls with same coordinates:** Though usually distinct, if coordinates repeat, the minimum distance could be 0.
* **Number of cows equals number of stalls:** Each cow must be placed in exactly one stall; the answer is the minimum gap between any two adjacent stalls.

---

### 5. 🔹 Important Notes / Takeaways
* **Binary Search on Answer:** This problem is a classic example of applying Binary Search not on the array itself, but on the *result space*.
* **Pattern Recognition:** Whenever a problem asks to "Maximize the Minimum" or "Minimize the Maximum," Binary Search on Answer should be your first thought.
* **Greedy Helper:** The `canPlace` function uses a greedy approach, which is a common helper pattern for BS on Answer problems.

---

### 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N \log N) + O(N \times \text{range})$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(N \log N) + O(N \log(\text{range}))$ | $O(1)$ |

--- 

Q9 

# Allocate Minimum Number of Pages

### 1. 🔹 Problem Summary
Given an array `arr` where `arr[i]` represents the number of pages in the $i^{th}$ book and $m$ students, you need to allocate all books to students such that:
* Each student gets at least one book.
* Each book is allocated to exactly one student.
* Book allocation must be **contiguous**.
* The goal is to **minimize the maximum number of pages** assigned to any student.

---

### 2. 🔹 Key Observations & Intuition
* **Search Space:** The minimum possible answer is the maximum element in the array (since one student must read the largest book). The maximum possible answer is the sum of all pages (if one student reads every book).
* **Contiguous Constraint:** This is the "killer" constraint that makes the problem solvable via Binary Search on Answer. We cannot pick books randomly; they must be in a sequence.
* **Monotonicity:** If it is possible to allocate books such that no student reads more than $X$ pages, it is also possible for any value $Y > X$. This creates a range of $[Possible, Possible, ..., Impossible, Impossible]$ which allows us to use Binary Search.
* **Student Count vs. Pages:** As the maximum pages allowed per student increases, the number of students required decreases.

---

### 3. 🔹 Approaches

#### ➤ Brute Force
**Idea**
We iterate through all possible values for the "maximum pages per student" starting from the maximum element in the array up to the total sum of pages. For each value, we check if it's possible to distribute the books within the given $m$ students using a helper function `countStudents`.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times (\text{sum}(arr) - \max(arr) + 1))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

public class Solution {
    public static int countStudents(ArrayList<Integer> arr, int pages) {
        int n = arr.size(); // size of array
        int students = 1;
        long pagesStudent = 0;
        for (int i = 0; i < n; i++) {
            if (pagesStudent + arr.get(i) <= pages) {
                // add pages to current student
                pagesStudent += arr.get(i);
            } else {
                // add pages to next student
                students++;
                pagesStudent = arr.get(i);
            }
        }
        return students;
    }

    public static int findPages(ArrayList<Integer> arr, int n, int m) {
        // book allocation impossible
        if (m > n)
            return -1;

        int low = Collections.max(arr);
        int high = arr.stream().mapToInt(Integer::intValue).sum();

        for (int pages = low; pages <= high; pages++) {
            if (countStudents(arr, pages) == m) {
                return pages;
            }
        }
        return low;
    }

    public static void main(String[] args) {
        ArrayList<Integer> arr = new ArrayList<>(Arrays.asList(25, 46, 28, 49, 24));
        int n = 5;
        int m = 4;
        int ans = findPages(arr, n, m);
        System.out.println("The answer is: " + ans);
    }
}
```

---

#### ➤ Optimal Approach
**Detailed Explanation**
The optimal approach uses **Binary Search** on the answer space. Instead of checking every value linearly, we pick a `mid` value. If `countStudents(mid)` returns a number of students greater than $m$, it means our `mid` is too small, so we move the `low` pointer. Otherwise, if it's less than or equal to $m$, it could be a potential answer, so we move the `high` pointer to find a smaller maximum.

**Why this approach is optimal**
It drastically reduces the number of checks from a linear range to a logarithmic range ($\log(\text{Sum} - \text{Max})$), which is highly efficient for large page counts.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times \log(\text{sum}(arr) - \max(arr) + 1))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

public class Solution {
    public static int countStudents(ArrayList<Integer> arr, int pages) {
        int n = arr.size(); // size of array
        int students = 1; //Students are initially 1
        long pagesStudent = 0;
        for (int i = 0; i < n; i++) {
            if (pagesStudent + arr.get(i) <= pages) {
                // add pages to current student
                pagesStudent += arr.get(i);
            } else {
                // add pages to next student
                students++;
                pagesStudent = arr.get(i);
            }
        }
        return students;
    }

    public static int findPages(ArrayList<Integer> arr, int n, int m) {
        // book allocation impossible
        if (m > n)
            return -1;

        int low = Collections.max(arr);
        int high = arr.stream().mapToInt(Integer::intValue).sum();

        while (low <= high) {
            int mid = (low + high) / 2;
            int students = countStudents(arr, mid);
            if (students > m) {
                low = mid + 1; //Trim down the left part of the arry
            } else {
                high = mid - 1; //Trim down the right part of the array
            }
        }
        return low;
    }

    public static void main(String[] args) {
        ArrayList<Integer> arr = new ArrayList<>(Arrays.asList(25, 46, 28, 49, 24));
        int n = 5;
        int m = 4;
        int ans = findPages(arr, n, m);
        System.out.println("The answer is: " + ans);
    }
}
```

---

### 4. 🔹 Edge Cases
* **$m > n$:** If there are more students than books, it's impossible to give at least one book to each student. Return **-1**.
* **$m = 1$:** One student must read all books. The answer is the **sum of all elements**.
* **$m = n$:** Each student gets exactly one book. The answer is the **maximum element** in the array.

---

### 5. 🔹 Important Notes / Takeaways
* **Binary Search on Answer Pattern:** Recognizable when you need to "Minimize the Maximum" or "Maximize the Minimum."
* **Contiguous Allocation:** This is the key difference between this and problems that can be solved with a Priority Queue (Heaps).
* **Similar Problems:** This logic applies to *Aggressive Cows*, *Split Array Largest Sum*, and *Painter's Partition Problem*.

---

### 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N \times (\text{sum} - \text{max}))$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(N \times \log(\text{sum} - \text{max}))$ | $O(1)$ |

---

Q10

# Split Array - Largest Sum

### 1. 🔹 Problem Summary
Given an array `A` of size `N` and an integer `K`, you need to split the array into `K` non-empty **contiguous** subarrays. The goal is to minimize the **largest sum** among these `K` subarrays.

---

### 2. 🔹 Key Observations & Intuition
* **The Goal:** We want to distribute the numbers into $K$ groups such that the "heaviest" group is as light as possible.
* **The Range of the Answer:**
    * **Lower Bound (`low`):** The largest single element in the array. A subarray cannot have a sum smaller than its largest element.
    * **Upper Bound (`high`):** The sum of all elements in the array (this happens if $K=1$).
* **Contiguous Nature:** Because the subarrays must be contiguous, the problem mirrors the "Allocate Minimum Number of Pages" or "Painter's Partition" problems.
* **Monotonicity:** If we can split the array such that the maximum sum is $X$, then we can also split it for any maximum sum $Y > X$. This allows us to use Binary Search to find the minimum possible $X$.

---

### 3. 🔹 Approaches

#### ➤ Brute Force
**Idea**
Check every possible value for the "largest sum" starting from the maximum element in the array up to the total sum of all elements. For each value, use a helper function to count how many partitions are required. The first value that allows us to partition the array into $K$ (or fewer) subarrays is our answer.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times (\text{sum}(arr[]) - \max(arr[]) + 1))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

class SubarrayPartitioner {
    // Counts how many partitions are needed for a given maxSum limit
    public int countPartitions ( int [] a, int maxSum) {
        int n = a.length; // size of array
        int partitions = 1 ; // at least one partition
        long subarraySum = 0 ; // sum of current subarray
        for ( int i = 0 ; i < n; i++) {
            // Add to current subarray if possible
            if (subarraySum + a[i] <= maxSum) {
                subarraySum += a[i];
            } else {
                // Start new subarray
                partitions++;
                subarraySum = a[i];
            }
        }
        return partitions;
    }

    // Finds the smallest possible largest subarray sum to get exactly k partitions
    public int largestSubarraySumMinimized ( int [] a, int k) {
        int low = Arrays.stream(a).max().getAsInt(); // max element
        int high = Arrays.stream(a).sum(); // sum of all elements

        // Brute-force from low to high
        for ( int maxSum = low; maxSum <= high; maxSum++) {
            if (countPartitions(a, maxSum) == k) {
                return maxSum;
            }
        }
        return low; // fallback
    }

    public static void main (String[] args) {
        int [] a = { 10 , 20 , 30 , 40 };
        int k = 2 ;
        SubarrayPartitioner sp = new SubarrayPartitioner ();
        int ans = sp.largestSubarraySumMinimized(a, k);
        System.out.println( "The answer is: " + ans);
    }
}
```

---

#### ➤ Optimised Approach
**Detailed Explanation**
Instead of a linear search through the possible sums, we use **Binary Search**. 
1.  Initialize `low = max(arr)` and `high = sum(arr)`.
2.  Calculate `mid`.
3.  Check how many partitions are needed if the maximum allowed sum is `mid`.
4.  If `partitions > k`, it means our `mid` is too small (we need more partitions than allowed), so we increase the limit: `low = mid + 1`.
5.  If `partitions <= k`, it means `mid` is a possible answer, but we want the minimum, so we check smaller values: `high = mid - 1`.

**Why this approach is optimal**
It reduces the search space logarithmically rather than linearly, making it significantly faster for large arrays and large sum ranges.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times \log(\text{sum}(arr[]) - \max(arr[]) + 1))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

class SubarrayPartitioner {
    // Counts how many partitions are needed for a given maxSum
    public int countPartitions ( int [] a, int maxSum) {
        int partitions = 1 ; // at least one partition
        long subarraySum = 0 ; // sum of current subarray
        for ( int num : a) {
            if (subarraySum + num <= maxSum) {
                subarraySum += num;
            } else {
                partitions++;
                subarraySum = num;
            }
        }
        return partitions;
    }

    // Finds the minimum largest subarray sum possible for at most k partitions
    public int largestSubarraySumMinimized ( int [] a, int k) {
        int low = Arrays.stream(a).max().getAsInt(); // largest element
        int high = Arrays.stream(a).sum(); // sum of all elements

        // Binary search for the smallest maxSum
        while (low <= high) {
            int mid = (low + high) / 2 ;
            int partitions = countPartitions(a, mid);
            if (partitions > k) {
                low = mid + 1 ; // too many partitions → increase maxSum
            } else {
                high = mid - 1 ; // valid but try smaller maxSum
            }
        }
        return low;
    }

    public static void main (String[] args) {
        int [] a = { 10 , 20 , 30 , 40 };
        int k = 2 ;
        SubarrayPartitioner sp = new SubarrayPartitioner ();
        int ans = sp.largestSubarraySumMinimized(a, k);
        System.out.println( "The answer is: " + ans);
    }
}
```

---

### 4. 🔹 Edge Cases
* **$K = 1$:** The answer is the sum of all elements.
* **$K = N$:** Every element is its own subarray; the answer is the maximum element in the array.
* **Array with all identical elements:** Testing if the partition logic handles equal values correctly.
* **$K > N$:** (Technically not possible per "non-empty" constraint, but worth noting for robust code).

---

### 5. 🔹 Important Notes / Takeaways
* **Standard Pattern:** This is a classic "Binary Search on Answers" problem.
* **Equivalence:** This problem is identical to **Book Allocation** and **Painter's Partition**. Learning one solves all three.
* **Check Function:** The `countPartitions` function is the core logic. It uses a greedy approach: keep adding elements to a subarray as long as the sum doesn't exceed the limit.

---

### 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N \times (\text{sum} - \text{max}))$ | $O(1)$ |
| **Optimised (Binary Search)** | $O(N \times \log(\text{sum} - \text{max}))$ | $O(1)$ |

---

Q11

# Painter's Partition Problem

### 1. 🔹 Problem Summary
Given an array representing the lengths of $N$ boards and $K$ painters, you need to paint all boards. Each unit of a board takes 1 unit of time to paint. The constraint is that a painter can only paint **continuous sections** of boards. You need to find the **minimum possible maximum time** taken to complete the job.

---

### 2. 🔹 Key Observations & Intuition
* **Minimize the Maximum:** This is a classic indicator for **Binary Search on Answer**. We are looking for the smallest possible value of a "maximum limit."
* **Contiguous Constraint:** Since painters must pick continuous boards, we cannot sort the boards or pick them randomly. This makes the problem identical in logic to the [Book Allocation Problem](https://takeuforward.org/data-structure/allocate-minimum-number-of-pages/) and [Split Array Largest Sum](https://takeuforward.org/arrays/split-array-largest-sum/).
* **Range of Answer:** * The **minimum possible time** is the length of the longest board (since at least one painter has to paint it).
    * The **maximum possible time** is the sum of all board lengths (if only one painter does all the work).
* **Monotonicity:** If it is possible to paint all boards within time $T$, it is also possible for any time $> T$. If it's impossible for time $T$, it's impossible for any time $< T$.

---

### 3. 🔹 Approaches

#### ➤ Brute Force
**Idea**
Check every possible time starting from the maximum element in the array up to the total sum of the array. For each "time" limit, calculate how many painters are required. The first time limit that requires $\le K$ painters is our answer.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times (\text{sum}(\text{arr}[]) - \max(\text{arr}[]) + 1))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

public class PainterPartition {
    // Function to count how many painters are required if each painter paints at most 'time' units
    public int countPainters(int[] boards, int time) {
        int painters = 1; // Start with one painter
        int boardsPainter = 0; // Time consumed by current painter
        for (int board : boards) {
            if (boardsPainter + board <= time) {
                // Assign board to current painter
                boardsPainter += board;
            } else {
                // Assign board to next painter
                painters++;
                boardsPainter = board;
            }
        }
        return painters;
    }

    // Function to find the minimum possible maximum time to paint all boards using k painters
    public int findLargestMinDistance(int[] boards, int k) {
        int low = Arrays.stream(boards).max().getAsInt(); // Largest single board
        int high = Arrays.stream(boards).sum(); // Sum of all boards

        for (int time = low; time <= high; time++) {
            if (countPainters(boards, time) <= k) {
                return time; // Found a valid minimum time
            }
        }
        return low; // Fallback (shouldn't usually reach here)
    }

    public static void main(String[] args) {
        int[] boards = {10, 20, 30, 40}; // Length of boards
        int k = 2; // Number of painters
        PainterPartition pp = new PainterPartition();
        int ans = pp.findLargestMinDistance(boards, k);

        System.out.println("The answer is: " + ans); // Expected: 60
    }
}
```

---

#### ➤ Optimal Approach
**Detailed Explanation**
Instead of checking linearly, use **Binary Search** on the range `[low, high]`. 
1. Calculate `mid` (a potential maximum time).
2. Use `countPainters(mid)` to see how many painters are needed.
3. If `painters > k`, the time `mid` is too small. We need more time per painter, so move `low = mid + 1`.
4. If `painters <= k`, the time `mid` is a possible answer. Try to find an even smaller maximum time by moving `high = mid - 1`.

**Why this approach is optimal**
Binary search reduces the number of checks from a linear range to a logarithmic one, making it highly efficient for large board lengths or many boards.

**Time & Space Complexity**
* **Time Complexity:** $O(N \times \log(\text{sum}(\text{arr}[]) - \max(\text{arr}[]) + 1))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

public class PainterPartition {
    // Count how many painters are needed for a given max time
    public int countPainters(int[] boards, int time) {
        int painters = 1;
        int boardsPainter = 0;
        for (int board : boards) {
            if (boardsPainter + board <= time) {
                boardsPainter += board;
            } else {
                painters++;
                boardsPainter = board;
            }
        }
        return painters;
    }

    // Binary search to find minimum possible time to paint all boards
    public int findLargestMinDistance(int[] boards, int k) {
        int low = Arrays.stream(boards).max().getAsInt();
        int high = Arrays.stream(boards).sum();
        int result = high;
        while (low <= high) {
            int mid = (low + high) / 2;
            int painters = countPainters(boards, mid);
            if (painters > k) {
                low = mid + 1; // Too few painters → increase allowed time
            } else {
                result = mid; // Valid time → try to reduce it
                high = mid - 1;
            }
        }
        return result;
    }

    public static void main(String[] args) {
        int[] boards = {10, 20, 30, 40};
        int k = 2;
        PainterPartition pp = new PainterPartition();
        int ans = pp.findLargestMinDistance(boards, k);
        System.out.println("The answer is: " + ans); // Expected: 60
    }
}
```

---

### 4. 🔹 Edge Cases
* **$K = 1$:** One painter must do everything; answer is the sum of the array.
* **$K \ge N$:** Every board can have its own painter; answer is the maximum element in the array.
* **All boards are same length:** The problem becomes a simple division.
* **Single board:** The only painter must paint it; answer is that board's length.

---

### 5. 🔹 Important Notes / Takeaways
* **Pattern Identity:** The "Painter's Partition," "Book Allocation," and "Split Array Largest Sum" are essentially the same problem with different stories.
* **Greedy Helper:** The `countPainters` function uses a greedy strategy to pack as many boards as possible for one painter before moving to the next.
* **Interview Insight:** Always clarify if the segments must be contiguous. If not, the problem might shift toward a Heap/Greedy or DP approach (like the Partition Problem).

---

### 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N \times (\text{sum} - \text{max}))$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(N \times \log(\text{sum} - \text{max}))$ | $O(1)$ |

---

Q12

# Minimise Maximum Distance between Gas Stations

### 1. 🔹 Problem Summary
You are given a sorted array of gas station positions on the X-axis and an integer $k$. Your task is to place $k$ new gas stations anywhere on the X-axis (even at non-integer positions) such that the **maximum distance** between any two adjacent gas stations is **minimized**.

---

### 2. 🔹 Key Observations & Intuition
* **The Objective:** We are trying to "Minimise the Maximum," which often suggests Binary Search on Answer or a Greedy approach with a Priority Queue.
* **Segment Logic:** If we have a distance $D$ between two existing stations and we place $n$ new stations between them, the original segment is divided into $n+1$ smaller segments. Each smaller segment will have a length of $D / (n+1)$.
* **Floating Point Answer:** Unlike previous problems in the sheet, the answer here can be a decimal. This requires a different termination condition for Binary Search (using a small epsilon like $10^{-6}$).

---

### 3. 🔹 Approaches

#### ➤ Brute Force
**Idea**
Keep track of how many gas stations are placed in each existing gap using an array `howMany[]`. In each of the $k$ iterations, find the gap that currently has the maximum section length and place a new station there to reduce that specific distance.

**Time & Space Complexity**
* **Time Complexity:** $O(k \times n) + O(n)$
* **Space Complexity:** $O(n-1)$

**Java Code**
```java
import java.util.*;

class GasStationSolver {
    public double minimiseMaxDistance(int[] arr, int k) {
        int n = arr.length;
        int[] howMany = new int[n - 1]; // Number of gas stations in each segment

        // Place each gas station
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            double maxSection = -1;
            int maxInd = -1;

            // Find the segment with the maximum distance
            for (int i = 0; i < n - 1; i++) {
                double diff = arr[i + 1] - arr[i];
                double sectionLength = diff / (howMany[i] + 1.0);
                if (sectionLength > maxSection) {
                    maxSection = sectionLength;
                    maxInd = i;
                }
            }
            // Add gas station to the selected segment
            howMany[maxInd]++;
        }

        // Find the final max section length after placing all gas stations
        double maxAns = -1;
        for (int i = 0; i < n - 1; i++) {
            double diff = arr[i + 1] - arr[i];
            double sectionLength = diff / (howMany[i] + 1.0);
            maxAns = Math.max(maxAns, sectionLength);
        }
        return maxAns;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int k = 4;
        GasStationSolver solver = new GasStationSolver();
        double ans = solver.minimiseMaxDistance(arr, k);

        System.out.println("The answer is: " + ans);
    }
}
```

#### ➤ Better Approach
**Idea**
Instead of using a nested loop to find the maximum distance gap in every iteration, use a **Priority Queue (Max-Heap)** to store the gaps. This allows us to retrieve the largest gap in $O(\log n)$ time.

**Improvement over brute force**
Reduces the time taken to find the maximum gap from $O(n)$ to $O(\log n)$ for each of the $k$ stations.

**Time & Space Complexity**
* **Time Complexity:** $O(n \log n + k \log n)$
* **Space Complexity:** $O(n-1) + O(n-1)$ (Array + Priority Queue)

**Java Code**
```java
import java.util.*;

class Pair {
    double distance;
    int index;

    Pair(double distance, int index) {
        this.distance = distance;
        this.index = index;
    }
}

class Solution {
    public double minimiseMaxDistance(int[] arr, int k) {
        int n = arr.length;
        int[] howMany = new int[n - 1];

        // Priority queue (max-heap) to store the largest segment first
        PriorityQueue<Pair> pq = new PriorityQueue<>(
            (a, b) -> Double.compare(b.distance, a.distance)
        );

        // Add initial segments
        for (int i = 0; i < n - 1; i++) {
            pq.add(new Pair(arr[i + 1] - arr[i], i));
        }

        // Place k additional gas stations
        for (int gasStations = 1; gasStations <= k; gasStations++) {
            Pair top = pq.poll();
            int idx = top.index;
            howMany[idx]++;

            double totalDist = arr[idx + 1] - arr[idx];
            double newDist = totalDist / (howMany[idx] + 1);
            pq.add(new Pair(newDist, idx));
        }

        // Return max distance after placing k stations
        return pq.peek().distance;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int k = 4;
        Solution sol = new Solution();
        System.out.println("The answer is: " + sol.minimiseMaxDistance(arr, k));
    }
}
```

#### ➤ Optimal Approach
**Detailed Explanation**
Apply **Binary Search on the answer space**. The possible answer lies between $0$ and the initial maximum gap. For a chosen `mid` (potential max distance), we check how many stations are required to ensure no gap exceeds `mid`. If the required stations $\le k$, then `mid` is possible, and we try smaller values.

**Why this approach is optimal**
It completely bypasses the need to place stations one by one ($k$ iterations). It focuses on the distance itself, making it much faster when $k$ is large.

**Time & Space Complexity**
* **Time Complexity:** $O(n \times \log(\text{Len})) + O(n)$ (where Len is range/precision)
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

public class GasStationOptimizer {
    // Method to calculate required number of gas stations
    public int numberOfGasStationsRequired(double dist, int[] arr) {
        int n = arr.length;
        int count = 0;
        for (int i = 1; i < n; i++) {
            int numberInBetween = (int) ((arr[i] - arr[i - 1]) / dist);
            if ((arr[i] - arr[i - 1]) == (dist * numberInBetween)) {
                numberInBetween--;
            }
            count += numberInBetween; //total number of additional gas stations required
        }
        return count; //total number of additional gas stations required
    }

    // Method to minimize the maximum distance between gas stations
    public double minimiseMaxDistance(int[] arr, int k) {
        int n = arr.length;
        double low = 0, high = 0;
        for (int i = 0; i < n - 1; i++) {
            high = Math.max(high, arr[i + 1] - arr[i]);
        }

        double diff = 1e-6;
        while (high - low > diff) {
            double mid = (low + high) / 2.0;
            int count = numberOfGasStationsRequired(mid, arr);
            if (count > k) {
                low = mid;
            } else {
                high = mid;
            }
        }
        return high;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int k = 4;
        GasStationOptimizer optimizer = new GasStationOptimizer();
        double result = optimizer.minimiseMaxDistance(arr, k);

        System.out.println("The answer is: " + result);
    }
}
```

---

### 4. 🔹 Edge Cases
* **$k=1$:** Only one station to place; find the single largest gap and bisect it.
* **All stations initially at same distance:** Distributing $k$ stations evenly across gaps.
* **Large $k$ small $n$:** Many stations will be placed in the same small segments.
* **Non-integer positions:** Handled by the `double` types and precision logic in the optimal approach.

---

### 5. 🔹 Important Notes / Takeaways
* **Precision Matters:** In BS for decimals, instead of `low <= high`, use `while(high - low > 10^-6)` or a fixed number of iterations (e.g., 100 loops) for high accuracy.
* **Comparison:** The Priority Queue approach is better if $k$ is small, while the Binary Search approach is superior if $k$ is very large (since it doesn't depend on $k$).
* **Formula Tip:** `numberInBetween = (int)(gap / dist)` handles how many stations fit in a gap to keep the sub-gaps $\le dist$.

---

### 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(k \times n)$ | $O(n)$ |
| **Better (Priority Queue)** | $O(n \log n + k \log n)$ | $O(n)$ |
| **Optimal (Binary Search)** | $O(n \log(\text{Range}/\text{Precision}))$ | $O(1)$ |

---

Q13

# Median of 2 sorted arrays 
(hard problem)

---

Q14 

# K-th Element of two sorted arrays

### 1. 🔹 Problem Summary
Given two sorted arrays `a` and `b` of size `m` and `n` respectively, find the element that would be at the **k-th position** if both arrays were merged into a single sorted array.

---

### 2. 🔹 Key Observations & Intuition
* **Partitioning Logic:** This problem is an extension of the "Median of Two Sorted Arrays" logic. Instead of finding the middle, we are looking for a specific cut that places exactly `k` elements in the combined left partition.
* **Search Space Optimization:** We always perform the binary search on the **smaller array** to minimize the number of iterations.
* **Constraints on `low` and `high`:** * `low` cannot simply be 0 if $k$ is larger than the size of the second array (we must take at least some elements from the first array). Formula: `Math.max(0, k - n)`.
    * `high` cannot exceed the size of the first array or $k$. Formula: `Math.min(k, m)`.
* **The "Cut" Condition:** We find a `mid1` in array `a` and `mid2` (which is `k - mid1`) in array `b` such that all elements in the left partitions are smaller than or equal to all elements in the right partitions ($l1 \le r2$ and $l2 \le r1$).

---

### 3. 🔹 Approaches

*(Note: The [provided page](https://takeuforward.org/data-structure/k-th-element-of-two-sorted-arrays?mode=track&sheet=a2z-dsa) focuses on the Optimal Binary Search approach. While Brute Force involves merging and Better involves a counter, only the Optimal Code is explicitly provided in the Java section of this specific tutorial page.)*

#### ➤ Optimal Approach
**Detailed Explanation**
The optimal approach uses **Binary Search on partitions**. We try to pick `x` elements from the first array and `k - x` elements from the second array. By ensuring the boundary elements cross-verify ($l1 \le r2$ and $l2 \le r1$), we can identify the k-th element as `max(l1, l2)` without ever merging the arrays.

**Why this approach is optimal**
It achieves a logarithmic time complexity relative to the size of the smaller array, $O(\log(\min(m, n)))$, which is significantly faster than the linear $O(m+n)$ required for merging.

**Time & Space Complexity**
* **Time Complexity:** $O(\log(\min(m, n)))$
* **Space Complexity:** $O(1)$

**Java Code**
```java
import java.util.*;

class Solution {
    public int kthElement(int[] a, int[] b, int k) {
        int m = a.length;
        int n = b.length;

        // Ensure 'a' is the smaller array for optimization
        if (m > n) {
            return kthElement(b, a, k);
        }

        int left = k; // Number of elements in the left partition
        int low = Math.max(0, k - n), high = Math.min(k, m);
        while (low <= high) {
            int mid1 = (low + high) >> 1;
            int mid2 = left - mid1;
            int l1 = (mid1 > 0) ? a[mid1 - 1] : Integer.MIN_VALUE;
            int l2 = (mid2 > 0) ? b[mid2 - 1] : Integer.MIN_VALUE;
            int r1 = (mid1 < m) ? a[mid1] : Integer.MAX_VALUE;
            int r2 = (mid2 < n) ? b[mid2] : Integer.MAX_VALUE;

            if (l1 <= r2 && l2 <= r1) {
                return Math.max(l1, l2);
            } else if (l1 > r2) {
                high = mid1 - 1; // Move left
            } else {
                low = mid1 + 1; // Move right
            }
        }
        return -1; // Should never reach here if inputs are valid
    }
}

public class Main {
    public static void main(String[] args) {
        int[] a = {2, 3, 6, 7, 9};
        int[] b = {1, 4, 8, 10};
        int k = 5;
        Solution solution = new Solution();
        System.out.println("The " + k + "-th element of two sorted arrays is: " +
                solution.kthElement(a, b, k));
    }
}
```

---

### 4. 🔹 Edge Cases
* **k is small ($k < \min(m, n)$):** `low` can be 0.
* **k is large ($k > n$):** `low` must be at least `k - n` because even if we take all elements from array `b`, we still need more from array `a`.
* **k equals total elements ($k = m + n$):** The answer is the maximum of the last elements of both arrays.
* **One array is empty:** Handled by the initialization of `l1/l2` to `MIN_VALUE` and `r1/r2` to `MAX_VALUE`.

---

### 5. 🔹 Important Notes / Takeaways
* **Symmetry:** This is the exact same logic as [Median of Two Sorted Arrays](https://takeuforward.org/data-structure/median-of-two-sorted-arrays-of-different-sizes/), but instead of a fixed partition at $(m+n)/2$, we partition at $k$.
* **Boundary Handling:** Using `Integer.MIN_VALUE` and `Integer.MAX_VALUE` simplifies the logic for when a partition takes zero elements or all elements from an array.
* **Optimization:** Always Binary Search on the smaller array to ensure the fastest possible runtime.

---

### 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force (Merge)** | $O(m + n)$ | $O(m + n)$ |
| **Better (Counter)** | $O(k)$ | $O(1)$ |
| **Optimal (Binary Search)** | $O(\log(\min(m, n)))$ | $O(1)$ |

--- 
...
# Binary Search on 2D Arrays

