...
# Easy Problems 

1q
# Find the Largest Element in an Array

## 🔹 Problem Summary  
The goal is to identify the maximum value present within a given array of integers. Given an input array like `{2, 5, 1, 3, 0}`, the output should be `5`.

---

## 🔹 Key Observations & Intuition  
* **The Array Structure:** Since the array is unsorted, the largest element could be anywhere.
* **Sorting Benefit:** Sorting naturally places the largest element at the end of the array.
* **Linear Scan:** We can find the maximum in a single pass by keeping track of the largest value seen so far.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** The simplest way to find the largest element is to sort the array in ascending order. Once sorted, the element at the last index (`n-1`) will be the largest.

* **Time Complexity:** $O(N \log N)$ due to the sorting process.
* **Space Complexity:** $O(1)$ (ignoring the space used by the sorting algorithm itself).

**Java Code:**
```java
import java.util.Arrays;

class Solution {
    // Function to sort the array and return the largest element
    public static int sortArr ( int [] arr) {
        // Sort the array in ascending order
        Arrays.sort(arr);
        // Return the last element (largest element) after sorting
        return arr[arr.length - 1 ];
    }
}

public class Main {
    public static void main (String[] args) {
        // Initialize arrays
        int [] arr1 = { 2 , 5 , 1 , 3 , 0 };
        int [] arr2 = { 8 , 10 , 5 , 7 , 9 };
        // Find and output the largest element in both arrays
        System.out.println( "The Largest element in the array is: " + Solution.sortArr(arr1));
        System.out.println( "The Largest element in the array is: " + Solution.sortArr(arr2));
    }
}
```

### 2. Optimal Approach  
**Detailed Explanation:** Instead of sorting, we use a "greedy" approach. We initialize a variable `max` with the first element of the array. We then iterate through the rest of the array, comparing each element with `max`. If an element is found to be larger than `max`, we update `max` with that element.

**Why it is optimal:** This approach is optimal because it only visits each element exactly once. Since we must look at every element at least once to ensure we haven't missed the largest one, $O(N)$ is the theoretical lower bound for time complexity.

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
class Solution {
    // Function to find the largest element in the array
    public static int findLargestElement ( int [] arr, int n) {
        int max = arr[ 0 ]; // Initialize max with the first element in the array
        // Iterate through the array to find the maximum element
        for ( int i = 1 ; i < n; i++) {
            if (arr[i] > max) {
                // If the current element is greater than max, update max
                max = arr[i];
            }
        }
        return max; // Return the largest element found
    }
}

public class Main {
    public static void main (String[] args) {
        // Array 1
        int [] arr1 = { 2 , 5 , 1 , 3 , 0 };
        int n = arr1.length; // Size of the array
        int max = Solution.findLargestElement(arr1, n); // Call the function to find the largest element
        System.out.println( "The largest element in the array is: " + max); // Output the result
        
        // Array 2
        int [] arr2 = { 8 , 10 , 5 , 7 , 9 };
        n = arr2.length; // Size of the array
        max = Solution.findLargestElement(arr2, n); // Call the function to find the largest element
        System.out.println( "The largest element in the array is: " + max); // Output the result
    }
}
```

---

## 🔹 Edge Cases  
* **Array with one element:** The single element is both the maximum and minimum.
* **All elements are identical:** The logic should return that repeated value.
* **Array contains negative numbers:** Initializing `max = arr[0]` is safer than `max = 0`, as it handles cases where all numbers are negative.

---

## 🔹 Important Notes / Takeaways  
* **Sorting is Overkill:** While sorting works, it's inefficient for just finding a single maximum value.
* **Standard Pattern:** The "Initialize and Compare" pattern is a fundamental building block for many array-based problems in interviews.
* **Library Functions:** In a real interview, you might be asked if you know `Math.max()`, but writing the loop manually demonstrates your understanding of basic algorithms.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Recommendation |
| :--- | :--- | :--- | :--- |
| **Brute Force (Sorting)** | $O(N \log N)$ | $O(1)$ | Easy to implement, but slow. |
| **Optimal (Linear Scan)** | $O(N)$ | $O(1)$ | **Best for Interviews.** |

--- 
2q
# Find Second Smallest and Second Largest Element in an array

## 🔹 Problem Summary  
Given an array of integers, the task is to find the **second smallest** and the **second largest** elements. If the array has fewer than two unique elements such that a second smallest or largest cannot exist, return or print -1.

---

## 🔹 Key Observations & Intuition  
* **Duplicates Matter:** The "second largest" is not necessarily the element at `index n-2` if there are duplicate maximum values. We need the second *distinct* largest/smallest.
* **Single Pass Potential:** While sorting is the easiest way to visualize the order, we can actually find these values in a single traversal by maintaining two variables for each (e.g., `small` and `second_small`).
* **Initialization:** To avoid errors with arrays containing negative numbers or zeros, initialize "small" variables to the maximum possible integer and "large" variables to the minimum possible integer.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Sort the array in ascending order. The second element (`index 1`) will be the second smallest, and the element at `index n-2` will be the second largest.  
*Note: This specific brute force logic assumes there are no duplicates of the absolute maximum/minimum.*

* **Time Complexity:** $O(N \log N)$ for sorting the array.
* **Space Complexity:** $O(1)$ (ignoring sorting overhead).

**Java Code:**
```java
import java.util.Arrays;

class Solution {
    // Method to find the second smallest and second largest elements in the array
    public static void getElements ( int [] arr, int n) {
        // Edge case: when the array has less than 2 elements
        if (n == 0 || n == 1 ) {
            System.out.println(- 1 + " " + - 1 ); // Print -1 for both second smallest and second largest
            return ;
        }
        // Sort the array to easily find the second smallest and second largest elements
        Arrays.sort(arr);
        // Second smallest element is at index 1 after sorting
        int small = arr[ 1 ];
        // Second largest element is at index n-2 after sorting
        int large = arr[n - 2 ];
        // Output the second smallest and second largest elements
        System.out.println( "Second smallest is " + small);
        System.out.println( "Second largest is " + large);
    }
}

public class Main {
    public static void main (String[] args) {
        // Initialize the array with elements
        int [] arr = { 1 , 2 , 4 , 6 , 7 , 5 };
        // Calculate the size of the array
        int n = arr.length;
        // Call the method to find and print the second smallest and second largest elements
        Solution.getElements(arr, n);
    }
}
```

---

### 2. Better Approach  
**Idea:** Instead of sorting, perform two linear traversals. In the first pass, find the absolute `small` and `large` elements. In the second pass, find the elements that are strictly greater than `small` but the smallest among the rest, and strictly smaller than `large` but the largest among the rest.

* **Improvements over brute:** Reduces time complexity from $O(N \log N)$ to $O(N)$.
* **Complexity:** * **Time:** $O(N) + O(N) = O(N)$ (two passes).  
    * **Space:** $O(1)$.

**Java Code:**
```java
import java.util.*;

// Class to solve the problem of finding the second smallest and second largest elements
class Solution {
    // Method to find the second smallest and second largest elements in the array
    public static void getElements ( int [] arr, int n) {
        // Edge case: when the array has less than 2 elements
        if (n == 0 || n == 1 ) {
            System.out.println(- 1 + " " + - 1 ); // Print -1 for both second smallest and second largest
            return ;
        }
        // Initialize variables to track the smallest, second smallest, largest, and second largest elements
        int small = Integer.MAX_VALUE, second_small = Integer.MAX_VALUE;
        int large = Integer.MIN_VALUE, second_large = Integer.MIN_VALUE;
        // Find the smallest and largest elements in the array
        for ( int i = 0 ; i < n; i++) {
            small = Math.min(small, arr[i]); // Update the smallest element
            large = Math.max(large, arr[i]); // Update the largest element
        }
        // Find the second smallest and second largest elements
        for ( int i = 0 ; i < n; i++) {
            if (arr[i] < second_small && arr[i] != small) {
                second_small = arr[i]; // Update second smallest if a smaller element is found
            }
            if (arr[i] > second_large && arr[i] != large) {
                second_large = arr[i]; // Update second largest if a larger element is found
            }
        }
        // Output the second smallest and second largest elements
        System.out.println( "Second smallest is " + second_small);
        System.out.println( "Second largest is " + second_large);
    }
}

public class Main {
    public static void main (String[] args) {
        // Driver code
        int n = 6 ;
        int [] arr = { 1 , 2 , 4 , 6 , 7 , 5 }; // Array of elements
        // Call the function to find and print the second smallest and second largest elements
        Solution.getElements(arr, n);
    }
}
```

---

### 3. Optimal Approach  
**Detailed Explanation:** We can find the second smallest and second largest in **one single pass**.  
* **For Second Largest:** As we traverse, if the current element is larger than the current `large`, the old `large` becomes the `second_large`, and the current element becomes the new `large`. If the current element is not larger than `large` but is larger than `second_large` (and not equal to `large`), update `second_large`.  
* **For Second Smallest:** Similar logic applies—if the current element is smaller than `small`, update `second_small` to the old `small` and set the current element as the new `small`.

**Why it is optimal:** It achieves the result in a single traversal ($O(N)$) with minimal comparisons and no extra space.

* **Complexity:** * **Time:** $O(N)$ (single pass).  
    * **Space:** $O(1)$.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the second smallest element in the array
    public static int secondSmallest ( int [] arr, int n) {
        // Edge case: if the array has fewer than 2 elements
        if (n < 2 ) return - 1 ;
        int small = Integer.MAX_VALUE;
        int second_small = Integer.MAX_VALUE;
        // Loop through the array to find the second smallest element
        for ( int i = 0 ; i < n; i++) {
            // Update the smallest and second smallest values
            if (arr[i] < small) {
                second_small = small;
                small = arr[i];
            } else if (arr[i] < second_small && arr[i] != small) {
                second_small = arr[i];
            }
        }
        return second_small; // Return the second smallest element
    }

    // Function to find the second largest element in the array
    public static int secondLargest ( int [] arr, int n) {
        // Edge case: if the array has fewer than 2 elements
        if (n < 2 ) return - 1 ;
        int large = Integer.MIN_VALUE, second_large = Integer.MIN_VALUE;
        // Loop through the array to find the second largest element
        for ( int i = 0 ; i < n; i++) {
            // Update the largest and second largest values
            if (arr[i] > large) {
                second_large = large;
                large = arr[i];
            } else if (arr[i] > second_large && arr[i] != large) {
                second_large = arr[i];
            }
        }
        return second_large; // Return the second largest element
    }
}

public class Main {
    public static void main (String[] args) {
        // Array of elements
        int [] arr = { 1 , 2 , 4 , 7 , 7 , 5 };
        // Calculate the size of the array
        int n = arr.length;
        // Find the second smallest and second largest elements
        int sS = Solution.secondSmallest(arr, n);
        int sL = Solution.secondLargest(arr, n);
        // Output the results
        System.out.println( "Second smallest is " + sS);
        System.out.println( "Second largest is " + sL);
    }
}
```

---

## 🔹 Edge Cases  
* **Array Size < 2:** If the array has 0 or 1 elements, return -1.
* **All Elements are Same:** If the array is `[7, 7, 7]`, there is no "second" distinct element. The code handles this with the `!= small` or `!= large` check.
* **Duplicate Max/Min:** If the array is `[1, 2, 7, 7, 5]`, the second largest is 5, not the second 7. The optimal logic correctly identifies 5 by checking `arr[i] != large`.

---

## 🔹 Important Notes / Takeaways  
* **Interview Tip:** Always clarify if "second largest" means the second *distinct* value or simply the value at the second position in a sorted list. Most interviewers mean distinct.
* **Initialization Trap:** Never initialize `small` to 0 if the array could contain positive numbers, and never initialize `large` to 0 if the array could contain negative numbers. Use `Integer.MAX_VALUE` and `Integer.MIN_VALUE`.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Pass Count |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N \log N)$ | $O(1)$ | N/A (Sorting) |
| **Better** | $O(N)$ | $O(1)$ | Two Passes |
| **Optimal** | $O(N)$ | $O(1)$ | **Single Pass** |
---
3q

# Check if an Array is Sorted

## 🔹 Problem Summary  
Given an array of size $n$, determine if it is sorted in non-decreasing (ascending) order. The function should return `True` if every element is smaller than or equal to the elements following it, and `False` otherwise.

---

## 🔹 Key Observations & Intuition  
* **Sorted Definition:** In a non-decreasing array, for any index $i$, the condition $arr[i] \ge arr[i-1]$ must hold true.
* **Early Exit:** As soon as we find a single instance where a preceding element is greater than a succeeding element, we can immediately conclude the array is not sorted.
* **Small Arrays:** An array with 0 or 1 element is vacuously sorted.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Pick each element one by one and compare it with all the elements to its right. If any element to the right is smaller than the current element, the array is not sorted.

* **Time Complexity:** $O(N^2)$ because of the nested loops comparing every pair.
* **Space Complexity:** $O(1)$ as no extra data structures are used.

**Java Code:**
```java
class Solution {
    // Function to check if the array is sorted
    public boolean isSorted(int[] arr, int n) {
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                // If any element is smaller than the previous one, return false
                if (arr[j] < arr[i])
                    return false;
            }
        }

        return true; // Return true if no unsorted elements are found
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int n = 5;
        Solution obj = new Solution();
        boolean ans = obj.isSorted(arr, n);
        // Output result
        if (ans)
            System.out.println("True");
        else
            System.out.println("False");
    }
}
```

---

### 2. Optimal Approach  
**Detailed Explanation:** Instead of comparing an element with every other element, we only need to compare each element with its immediate predecessor. If $arr[i] < arr[i-1]$ for any $i$, the array is not sorted. We start the check from the second element (index 1).

**Why it is optimal:** It processes the array in a single pass. Since we must examine every element at least once to confirm the order, $O(N)$ is the best possible time complexity.

* **Complexity:** * **Time Complexity:** $O(N)$  
  * **Space Complexity:** $O(1)$  

**Java Code:**
```java
class Solution {
    // Function to check if the array is sorted
    public boolean isSorted(int[] arr, int n) {
        for (int i = 1; i < n; i++) {
            if (arr[i] < arr[i - 1])
                // If any element is smaller than the previous one, return false
                return false;
        }

        return true; // Return true if the array is sorted
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int n = arr.length;
        Solution obj = new Solution();
        // Output result
        System.out.println(obj.isSorted(arr, n) ? "True" : "False");
    }
}
```

---

## 🔹 Edge Cases  
* **Empty Array ($N=0$):** Should return `True`.
* **Single Element ($N=1$):** Should return `True`.
* **Array with Duplicates:** `{1, 2, 2, 3}` is considered sorted because it is non-decreasing ($2 \le 2$).
* **Strictly Decreasing:** `{5, 4, 3, 2, 1}` should return `False`.

---

## 🔹 Important Notes / Takeaways  
* **Single Pass Logic:** Many array problems can be optimized from $O(N^2)$ to $O(N)$ by checking adjacent elements rather than all pairs.
* **Non-decreasing vs. Strictly Increasing:** "Sorted" in many DSA problems implies non-decreasing ($arr[i] \ge arr[i-1]$). Always clarify if duplicates are allowed.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Improvement |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Basic pair-wise comparison. |
| **Optimal** | $O(N)$ | $O(1)$ | **Reduces comparisons to a single pass.** |
---
4q 
# Remove Duplicates in-place from Sorted Array

## 🔹 Problem Summary  
Given an integer array sorted in non-decreasing order, remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements must be preserved. You need to return the number of unique elements ($k$), and the first $k$ elements of the original array should contain these unique values.

---

## 🔹 Key Observations & Intuition  
* **Sorted Property:** Since the array is already sorted, all identical elements are guaranteed to be adjacent.
* **In-Place Requirement:** We cannot use extra space for a new array; we must modify the input `nums` directly.
* **Two-Pointer Logic:** We can use one pointer to keep track of the position of the last unique element found and another pointer to scan through the array.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Use a `HashSet` to store unique elements. Since a set only allows one occurrence of each element, it automatically filters duplicates. We then iterate through the set and overwrite the beginning of the original array.

* **Time Complexity:** $O(N)$ — We traverse the array once to insert into the set and once to overwrite the array.
* **Space Complexity:** $O(N)$ — In the worst case (all elements unique), the set stores $N$ elements.

**Java Code:**
```java
import java.util.HashSet;

// Solution class containing removeDuplicates method
class Solution {
    // Removes duplicates using HashSet and returns count of unique elements
    public int removeDuplicates(int[] nums) {
        // HashSet to store unique elements we have seen
        HashSet<Integer> seen = new HashSet<>();
        // Position to overwrite next unique element
        int index = 0;
        // Loop over each number in nums
        for (int num : nums) {
            // If num is not in the set, it is unique
            if (!seen.contains(num)) {
                // Add num to the set
                seen.add(num);
                // Write num at current index position
                nums[index] = num;
                // Move index forward
                index++;
            }
        }
        // Return number of unique elements
        return index;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] nums = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};
        Solution sol = new Solution();
        int k = sol.removeDuplicates(nums);

        System.out.println("k = " + k);
        System.out.print("Array after removing duplicates: ");
        for (int i = 0; i < k; i++) {
            System.out.print(nums[i] + " ");
        }
    }
}
```

---

### 2. Optimal Approach  
**Detailed Explanation:** Use a two-pointer approach ($i$ and $j$). 
1.  Initialize $i = 0$ (the first element is always unique).
2.  Iterate with $j$ from $1$ to $n-1$.
3.  If `nums[j]` is different from `nums[i]`, it means we found a new unique element.
4.  Increment $i$ and update `nums[i] = nums[j]`.

**Why it is optimal:** It exploits the sorted nature of the array to avoid using extra memory ($O(1)$ space) while still finishing in a single linear pass.

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
// Class to hold the solution logic
class Solution {
    // Function to remove duplicates from sorted array in-place
    public int removeDuplicates(int[] nums) {
        // If array is empty, return 0
        if (nums.length == 0) return 0;
        
        // Pointer for last unique element
        int i = 0;
        
        // Start from second element
        for (int j = 1; j < nums.length; j++) {
            // If new unique element is found
            if (nums[j] != nums[i]) {
                // Move unique position forward
                i++;
                // Place new unique element
                nums[i] = nums[j];
            }
        }
        // i is last index of unique element, count = i + 1
        return i + 1;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] nums = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};
        Solution sol = new Solution();
        int k = sol.removeDuplicates(nums);

        System.out.println("Unique count = " + k);
        System.out.print("Array after removing duplicates: ");
        for (int x = 0; x < k; x++) {
            System.out.print(nums[x] + " ");
        }
    }
}
```

---

## 🔹 Edge Cases  
* **Empty Array:** Return 0.
* **All Elements Unique:** The pointers will move, but the array remains unchanged.
* **All Elements Same:** $i$ will stay at 0, and the function will return 1.

---

## 🔹 Important Notes / Takeaways  
* **Two-Pointer Strategy:** This is a classic example of using two pointers to modify an array in-place without extra space.
* **Result Interpretation:** The value returned ($k$) is just as important as the modification of the array, as it tells the caller how much of the array is valid.
* **Interview Insight:** Always check if the input array is sorted. If it wasn't, you would likely need to sort it first or use the Brute Force (Set) approach.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(N)$ | HashSet for uniqueness |
| **Optimal** | $O(N)$ | $O(1)$ | **Two Pointers ($i, j$)** |
---
5q
# Left Rotate the Array by One

## 🔹 Problem Summary  
Given an integer array, rotate its elements to the left by one position. This means the element at the first index moves to the last index, and all other elements shift one position to the left. The modification should be done **in-place**.

---

## 🔹 Key Observations & Intuition  
* **Shift Pattern:** Every element at index $i$ (where $i > 0$) moves to index $i-1$.
* **The "Wrap Around":** The element at index $0$ has no index $-1$ to move to, so it "wraps around" to the very end of the array ($n-1$).
* **Data Preservation:** To avoid losing the first element when the second element overwrites it, we must store the first element in a temporary variable before starting the shift.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Create a temporary "dummy" array of the same size. Iterate through the original array starting from the second element, placing them into the dummy array at one position shifted left. Finally, place the original first element into the last slot of the dummy array.

* **Time Complexity:** $O(N)$, where $N$ is the size of the array.
* **Space Complexity:** $O(N)$, as we use an extra array to store the results.

**Java Code:**
```java
// Class containing the solve method
class Solution {
    // Function to solve and shift array elements left by one position
    public static void solve ( int [] arr, int n) {
        int [] temp = new int [n]; // Temporary array to store shifted elements
        // Shift elements to the left by one position
        for ( int i = 1 ; i < n; i++) {
            temp[i - 1 ] = arr[i];
        }
        temp[n - 1 ] = arr[ 0 ]; // First element moves to the last position
        // Print the rotated array
        for ( int i = 0 ; i < n; i++) {
            System.out.print(temp[i] + " " );
        }
        System.out.println();
    }
}

// Main class
public class Main {
    public static void main (String[] args) {
        int n = 5 ; // Size of the array
        int [] arr = { 1 , 2 , 3 , 4 , 5 }; // Original array
        Solution.solve(arr, n); // Call the solve function from Solution class
    }
}
```

---

### 2. Optimal Approach  
**Detailed Explanation:** 1. Store the first element of the array in a `temp` variable.
2. Use a loop to iterate from the second element to the end of the array.
3. In each iteration, move `arr[i]` to `arr[i-1]`.
4. After the loop, assign the `temp` value to the last index of the array.

**Why it is optimal:** It modifies the original array directly without requiring a second array, reducing space usage from linear to constant while maintaining the best possible time complexity.

* **Complexity:** * **Time Complexity:** $O(N)$
    * **Space Complexity:** $O(1)$

**Java Code:**
```java
class Solution {
    public void rotateArrayByOne ( int [] nums) {
        // Store the first element in a temporary variable
        int temp = nums[ 0 ];
        // Shift elements to the left
        for ( int i = 1 ; i < nums.length; i++) {
            nums[i - 1 ] = nums[i];
        }
        // Place the first element at the end
        nums[nums.length - 1 ] = temp;
    }
}

class Main {
    public static void main (String[] args) {
        Solution solution = new Solution ();
        int [] nums = { 1 , 2 , 3 , 4 , 5 };

        solution.rotateArrayByOne(nums);
        // Output the rotated array
        for ( int num : nums) {
            System.out.print(num + " " );
        }
    }
}
```

---

## 🔹 Edge Cases  
* **Array with 1 element:** The element is stored in `temp`, the loop doesn't run, and it's placed back in the same spot. Result remains the same (correct).
* **Array with 2 elements:** `arr[0]` is stored, `arr[1]` moves to `arr[0]`, then `temp` moves to `arr[1]`. Effectively a swap.
* **Empty Array:** The code should include a check for `nums.length == 0` to avoid an `ArrayIndexOutOfBoundsException`.

---

## 🔹 Important Notes / Takeaways  
* **In-place modification:** Always prefer $O(1)$ space solutions for rotation problems unless the original data must be preserved.
* **Foundation for K-rotation:** This logic is the base for "Rotate by K places." However, while repeating this $K$ times gives $O(N \cdot K)$, there are better ways (like the Reversal Algorithm) for rotating by $K$.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Key Feature |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(N)$ | Uses extra space/dummy array. |
| **Optimal** | $O(N)$ | $O(1)$ | **Modifies the original array in-place.** |
---
6q
# Rotate Array by K Elements

## 🔹 Problem Summary  
Given an array of integers, rotate the array by **k** elements. The rotation can be either to the **left** or to the **right**. 
* **Right Rotation:** Elements shift right; the last $k$ elements move to the front.
* **Left Rotation:** Elements shift left; the first $k$ elements move to the back.

---

## 🔹 Key Observations & Intuition  
* **Modulo Arithmetic:** If $k$ is greater than the array size $n$, rotating $k$ times is equivalent to rotating $k \pmod n$ times. For example, if $n=5$ and $k=6$, it’s the same as rotating once.
* **Section Reversal:** A key insight for the optimal approach is that rotation is essentially a rearrangement of two blocks of the array. Reversing these blocks in a specific order achieves the desired rotation without extra space.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** * **For Right Rotation:** Store the last $k$ elements in a temporary array. Shift the remaining $(n-k)$ elements to the right. Copy the temporary array elements back to the beginning.
* **For Left Rotation:** Store the first $k$ elements in a temporary array. Shift the remaining $(n-k)$ elements to the left. Copy the temporary array elements to the end.

* **Time Complexity:** $O(n)$
* **Space Complexity:** $O(k)$ due to the temporary array.

**Java Code:**
```java
import java.util.Arrays;

class Solution {
    // Rotate the array to the right by k positions
    public void rotateRight(int[] arr, int k) {
        int n = arr.length;
        if (n == 0) return;

        k = k % n;
        // Store last k elements
        int[] temp = Arrays.copyOfRange(arr, n - k, n);
        // Shift the remaining elements to the right
        for (int i = n - k - 1; i >= 0; i--) {
            arr[i + k] = arr[i];
        }
        // Copy the stored elements to the front
        for (int i = 0; i < k; i++) {
            arr[i] = temp[i];
        }
    }

    // Rotate the array to the left by k positions
    public void rotateLeft(int[] arr, int k) {
        int n = arr.length;
        if (n == 0) return;

        k = k % n;
        // Store first k elements
        int[] temp = Arrays.copyOfRange(arr, 0, k);
        // Shift remaining elements to the left
        for (int i = k; i < n; i++) {
            arr[i - k] = arr[i];
        }
        // Copy stored elements to the end
        for (int i = 0; i < k; i++) {
            arr[n - k + i] = temp[i];
        }
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        int k = 2;

        sol.rotateRight(arr, k);
        System.out.println("Array after right rotation: " + Arrays.toString(arr));

        int[] arr2 = {1, 2, 3, 4, 5, 6, 7};
        sol.rotateLeft(arr2, k);
        System.out.println("Array after left rotation: " + Arrays.toString(arr2));
    }
}
```

---

### 2. Optimal Approach (Reversal Algorithm)
**Detailed Explanation:** Instead of using extra space, we use the property of reversals:
* **For Right Rotation:**
  1. Reverse the entire array.
  2. Reverse the first $k$ elements.
  3. Reverse the remaining $n-k$ elements.
* **For Left Rotation:**
  1. Reverse the first $k$ elements.
  2. Reverse the remaining $n-k$ elements.
  3. Reverse the entire array.

**Why it is optimal:** It achieves the rotation in $O(n)$ time while using $O(1)$ extra space, as all modifications happen within the original array boundaries.

* **Time Complexity:** $O(n)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to reverse part of the array between given indices
    void reverseArray(int[] nums, int start, int end) {
        // Swap elements until start meets end
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }

    // Function to rotate array left or right by k steps
    public int[] rotateArray(int[] nums, int k, String direction) {
        // Get array length
        int n = nums.length;
        // Edge case: do nothing if array is empty or k is 0
        if (n == 0 || k == 0) return nums;
        // Normalize k if greater than n
        k = k % n;

        // If rotation is to the right
        if (direction.equals("right")) {
            // Step 1: reverse entire array
            reverseArray(nums, 0, n - 1);
            // Step 2: reverse first k elements
            reverseArray(nums, 0, k - 1);
            // Step 3: reverse remaining n-k elements
            reverseArray(nums, k, n - 1);
        }
        // If rotation is to the left
        else if (direction.equals("left")) {
            // Step 1: reverse first k elements
            reverseArray(nums, 0, k - 1);
            // Step 2: reverse remaining n-k elements
            reverseArray(nums, k, n - 1);
            // Step 3: reverse entire array
            reverseArray(nums, 0, n - 1);
        }
        // Return the rotated array
        return nums;
    }
}

// Driver code
public class Main {
    public static void main(String[] args) {
        // Create instance of Solution
        Solution sol = new Solution();
        // Input array and parameters
        int[] nums = {1, 2, 3, 4, 5, 6, 7};
        int k = 2;
        String direction = "right";

        // Call rotateArray and store result
        int[] result = sol.rotateArray(nums, k, direction);

        // Print rotated array
        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 🔹 Edge Cases  
* **$k=0$ or $k=n$:** The array remains unchanged.
* **Empty array:** The function should return without errors.
* **$k > n$:** Handled by $k = k \pmod n$.
* **Negative $k$:** Usually not required by the problem, but a left rotation by $k$ is equivalent to a right rotation by $n-k$.

---

## 🔹 Important Notes / Takeaways  
* **In-place Reversal:** This is a very common technique in string and array manipulation (e.g., "Reverse words in a sentence").
* **Normalization:** Always perform `k = k % n` to avoid unnecessary work and index out of bounds errors.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(n)$ | $O(k)$ | Temporary array and shifting |
| **Optimal** | $O(n)$ | $O(1)$ | **Reversal Algorithm** |
---
7q
# Move all Zeros to the end of the array

## 🔹 Problem Summary  
You are given an array of integers. Your task is to move all the zeros in the array to the end while maintaining the relative order of the non-zero integers at the front.

---

## 🔹 Key Observations & Intuition  
* **Relative Order:** We cannot simply sort the array, as sorting would change the order of the non-zero elements.
* **In-place vs. Extra Space:** A naive solution uses an extra array to separate zeros, but an optimal solution uses pointers to swap elements in-place.
* **The "Zero Hole":** Think of the first zero encountered as a "hole" that needs to be filled by the next available non-zero element.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** 1. Create a temporary array.
2. Iterate through the original array and copy all non-zero elements into the temporary array.
3. Fill the remaining spots in the temporary array with zeros.
4. Copy everything back to the original array.

* **Time Complexity:** $O(N) + O(N) = O(2N) \approx O(N)$ (Two passes: one for non-zeros, one to copy back).
* **Space Complexity:** $O(N)$ because we use an additional `temp` array.

**Java Code:**
```java
import java.util.*;

// Solution class
class Solution {
    // Function to move all zeroes to end
    public int[] moveZeroes(int[] arr) {
        // Create temp array
        int[] temp = new int[arr.length];
        // Pointer for temp
        int index = 0;
        // Traverse input array
        for (int i = 0; i < arr.length; i++) {
            // If non-zero, copy to temp
            if (arr[i] != 0) {
                temp[index] = arr[i];
                index++;
            }
        }
        // Copy temp back to original
        for (int i = 0; i < arr.length; i++) {
            arr[i] = temp[i];
        }
        // Return updated array
        return arr;
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        // Input array
        int[] arr = {0, 1, 0, 3, 12};
        // Solution object
        Solution sol = new Solution();
        // Call the function
        int[] result = sol.moveZeroes(arr);
        // Print the result
        System.out.print("Array after moving zeroes: ");
        for (int num : result) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}
```

---

### 2. Optimal Approach  
**Detailed Explanation:** We use a **Two-Pointer** technique:
1. Find the first zero in the array and let a pointer `j` point to it.
2. Iterate through the array with another pointer `i` starting from `j + 1`.
3. Whenever `arr[i]` is a non-zero element, swap `arr[i]` with `arr[j]`.
4. Increment `j` to point to the next available spot (which will now be a zero after the swap).

**Why it is optimal:** It solves the problem in a single pass (after finding the first zero) and, most importantly, uses $O(1)$ extra space by modifying the array in-place.

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to move zeroes to the end
    public void moveZeroes(int[] nums) {
        // Pointer to the first zero
        int j = -1;
        // Find the first zero
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                j = i;
                break;
            }
        }
        // If no zero found, return
        if (j == -1) return;

        // Start from the next index of first zero
        for (int i = j + 1; i < nums.length; i++) {
            // If current element is non-zero
            if (nums[i] != 0) {
                // Swap with nums[j]
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
                // Move j to next zero
                j++;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {0, 1, 0, 3, 12};
        sol.moveZeroes(nums);
        // Print the result
        for (int num : nums)
            System.out.print(num + " ");
        System.out.println();
    }
}
```

---

## 🔹 Edge Cases  
* **No Zeros:** The code finds `j = -1` and returns immediately (correct).
* **All Zeros:** The first loop sets `j = 0`, and the second loop finds no non-zero elements to swap.
* **Array already "Correct":** (e.g., `{1, 2, 0, 0}`) The logic handles this gracefully by swapping the zero with itself or not triggering swaps.

---

## 🔹 Important Notes / Takeaways  
* **Two-Pointer Pattern:** This is a classic "Partitioning" problem similar to the logic used in QuickSort (partitioning around a pivot, which in this case is zero).
* **Efficiency:** In interviews, always aim for the in-place $O(1)$ space complexity once you've explained the brute force.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N)$ | $O(N)$ | Temporary array |
| **Optimal** | $O(N)$ | $O(1)$ | **Two Pointers / In-place Swap** |
---
8q
# Linear Search

## 🔹 Problem Summary  
Given an array and an element `num`, the goal is to determine if `num` is present in the array. If it exists, return the **index** of its first occurrence; otherwise, return **-1**.

---

## 🔹 Key Observations & Intuition  
* **Unsorted Nature:** Since the problem doesn't specify that the array is sorted, we cannot use Binary Search. We must check elements one by one.
* **Sequential Access:** We start from the beginning (index 0) and move toward the end.
* **Early Exit:** As soon as we find the target element, we can stop the search and return the index.

---

## 🔹 Approaches  

### 1. Optimal Approach (Linear Search)
**Detailed Explanation:** 1. Traverse the array from the first element to the last using a loop.
2. In every iteration, check if the current element `arr[i]` is equal to the target `num`.
3. If a match is found, return the current index `i`.
4. If the loop finishes and the element hasn't been found, return -1.

**Why it is optimal:** For a general unsorted array, you must examine every element at least once in the worst case to be sure the element isn't there. Therefore, $O(N)$ is the best possible time complexity.

* **Time Complexity:** $O(N)$, where $N$ is the number of elements in the array.
* **Space Complexity:** $O(1)$, as no extra memory is used.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to search for a number in the array
    public static int search(int arr[], int n, int num) {
        int i;
        // Loop through the array to find the number
        for (i = 0; i < n; i++) {
            // If the current element matches the number, return its index
            if (arr[i] == num)
                return i;
        }
        // If the number is not found, return -1
        return -1;
    }

    public static void main(String args[]) {
        // Declare and initialize the array
        int arr[] = {1, 2, 3, 4, 5};
        // Number to search for
        int num = 4;
        // Calculate the number of elements in the array
        int n = arr.length;
        // Call the search function and store the result
        int val = search(arr, n, num);
        // Print the index of the found number or -1 if not found
        System.out.println(val);
    }
}
```

---

## 🔹 Edge Cases  
* **Element at the Start:** The loop exits after the first comparison (Best case: $O(1)$).
* **Element at the End:** The loop runs $N$ times.
* **Element Not Present:** The loop runs $N$ times and returns -1.
* **Empty Array:** The loop condition `i < n` fails immediately, and the function returns -1.

---

## 🔹 Important Notes / Takeaways  
* **Linear Search vs. Binary Search:** Use Linear Search for unsorted arrays or linked lists. Use Binary Search only when the data is sorted.
* **First Occurrence:** This standard implementation returns the *first* index where the number appears. If you needed the *last* occurrence, you would traverse the array backward.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Best Case |
| :--- | :--- | :--- | :--- |
| **Linear Search** | $O(N)$ | $O(1)$ | $O(1)$ (Element at index 0) |
---
9q
# Union of Two Sorted Arrays

## 🔹 Problem Summary  
The task is to find the **union** of two sorted arrays, `arr1` and `arr2`. The union consists of all common and distinct elements from both arrays, returned in **ascending order** without any duplicates.

---

## 🔹 Key Observations & Intuition  
* **Sorted Nature:** Since both input arrays are already sorted, we can leverage this to avoid expensive sorting operations.
* **Uniqueness:** A union by definition contains only unique elements.
* **Ordered Output:** The result must be in non-decreasing order. Using a `Map` or `Set` (which are ordered in Java/C++) or a **Two-Pointer** approach naturally maintains this order.

---

## 🔹 Approaches  

### 1. Brute Force (Using Map)  
**Idea:** Use a Map to store the frequency of elements from both arrays. Since Map keys are unique, duplicates are automatically handled. By using a `TreeMap` in Java, the keys are kept in sorted order.

* **Time Complexity:** $O((m+n) \log(m+n))$ — Inserting each element into the map takes logarithmic time.
* **Space Complexity:** $O(m+n)$ — To store the elements in the map and the result list.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to return a list containing the union of the two arrays.
    public static ArrayList<Integer> findUnion(int arr1[], int arr2[], int n, int m) {
        // TreeMap stores elements in sorted order and handles duplicates
        TreeMap<Integer, Integer> freq = new TreeMap<>();
        ArrayList<Integer> Union = new ArrayList<>();

        // Add elements of arr1 to map
        for (int i = 0; i < n; i++)
            freq.put(arr1[i], freq.getOrDefault(arr1[i], 0) + 1);

        // Add elements of arr2 to map
        for (int i = 0; i < m; i++)
            freq.put(arr2[i], freq.getOrDefault(arr2[i], 0) + 1);

        // Extract keys from map (they are already sorted)
        for (int it : freq.keySet())
            Union.add(it);

        return Union;
    }
}
```

---

### 2. Better Approach (Using Set)  
**Idea:** Similar to the Map approach, a `Set` handles duplicates. Using a `TreeSet` ensures that the elements are stored in ascending order.

* **Improvements over brute:** Slightly cleaner logic as we don't need to track frequencies, just the presence of elements.
* **Complexity:** Same as Map approach, $O((m+n) \log(m+n))$ for time and $O(m+n)$ for space.

**Java Code:**
```java
import java.util.*;

class Solution {
    static ArrayList<Integer> FindUnion(int arr1[], int arr2[], int n, int m) {
        // TreeSet maintains unique elements in sorted order
        TreeSet<Integer> s = new TreeSet<>();
        ArrayList<Integer> Union = new ArrayList<>();

        // Insert all elements of arr1
        for (int i = 0; i < n; i++)
            s.add(arr1[i]);

        // Insert all elements of arr2
        for (int i = 0; i < m; i++)
            s.add(arr2[i]);

        // Add set elements to result list
        for (int it : s)
            Union.add(it);

        return Union;
    }
}
```

---

### 3. Optimal Approach (Two Pointers)  
**Detailed Explanation:** 1.  Initialize two pointers, `i = 0` and `j = 0`.
2.  Compare `arr1[i]` and `arr2[j]`.
3.  Add the smaller element to the result list **if** it is not the same as the last element added (to maintain uniqueness).
4.  If both elements are equal, add one and increment both pointers.
5.  After one array is exhausted, add the remaining elements of the other array to the result, again checking for duplicates.

**Why it is optimal:** It takes advantage of the fact that arrays are already sorted. It only visits each element once, avoiding the $O(\log N)$ overhead of a Set or Map.

* **Time Complexity:** $O(m+n)$ — Single pass through both arrays.
* **Space Complexity:** $O(m+n)$ — To store the result list ($O(1)$ extra space if not counting the output).

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to return a list containing the union of the two arrays.
    public static ArrayList<Integer> findUnion(int arr1[], int arr2[], int n, int m) {
        int i = 0, j = 0; // Pointers
        ArrayList<Integer> Union = new ArrayList<>(); // Result list

        while (i < n && j < m) {
            if (arr1[i] <= arr2[j]) { // Case 1 and 2
                if (Union.size() == 0 || Union.get(Union.size() - 1) != arr1[i])
                    Union.add(arr1[i]);
                i++;
            } else { // Case 3
                if (Union.size() == 0 || Union.get(Union.size() - 1) != arr2[j])
                    Union.add(arr2[j]);
                j++;
            }
        }

        // Add remaining elements of arr1
        while (i < n) {
            if (Union.get(Union.size() - 1) != arr1[i])
                Union.add(arr1[i]);
            i++;
        }

        // Add remaining elements of arr2
        while (j < m) {
            if (Union.get(Union.size() - 1) != arr2[j])
                Union.add(arr2[j]);
            j++;
        }

        return Union;
    }
}
```

---

## 🔹 Edge Cases  
* **Duplicate elements within an array:** (e.g., `arr1 = {1, 1, 2}`). Handled by checking the last element in the result list.
* **One array is empty:** The pointers logic will immediately jump to the "remaining elements" loop for the non-empty array.
* **All elements common:** The pointers will move together, adding each unique element only once.

---

## 🔹 Important Notes / Takeaways  
* **Merge Sort Connection:** This approach is almost identical to the "Merge" step in Merge Sort, but with an added condition to ignore duplicates.
* **Space Complexity Clarification:** In interviews, clarify if the result array counts toward space complexity. Usually, it is considered $O(1)$ extra space if only auxiliary memory is measured.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Key Feature |
| :--- | :--- | :--- | :--- |
| **Using Map** | $O((m+n) \log(m+n))$ | $O(m+n)$ | Handles duplicates & sorting automatically. |
| **Using Set** | $O((m+n) \log(m+n))$ | $O(m+n)$ | Cleanest syntax, same complexity as Map. |
| **Two Pointers** | $O(m+n)$ | $O(m+n)$ | **Most efficient; uses sorted property.** |
---
10q
# The Missing Number - gfg

## 🔹 Problem Summary
Given an array `arr[]` of size $n-1$ containing distinct integers in the range $[1, n]$, find the one number that is missing from the sequence. Essentially, the array is a permutation of numbers from 1 to $n$ with one hole.

---

## 🔹 Key Observations & Intuition
* **Range Awareness:** The numbers are strictly between $1$ and $n$.
* **Distinct Elements:** There are no duplicates, which simplifies the logic—we only need to identify what is absent.
* **Mathematical Property:** The sum of the first $n$ natural numbers is a constant, which can be compared against the actual sum of the array.
* **Bitwise Property:** XORing a number with itself results in 0. This can be used to "cancel out" all numbers that appear in both the complete range and the given array.

---

## 🔹 Approaches

### 1. Brute Force (Linear Search)
**Idea:** Iterate through every number from $1$ to $n$. For each number, perform a nested scan of the array to see if it exists. If a number is not found after checking the entire array, that is the missing number.

* **Time Complexity:** $O(n^2)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
// Java program to find the missing number using brute force
import java.util.*;

class GfG {
    static int missingNum(int[] arr) {
        int n = arr.length + 1;

        // Iterate from 1 to n and check
        // if the current number is present
        for (int i = 1; i <= n; i++) {
            boolean found = false;
            for (int j = 0; j < n - 1; j++) {
                if (arr[j] == i) {
                    found = true;
                    break;
                }
            }

            // If the current number is not present
            if (!found) return i;
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] arr = { 8, 2, 4, 5, 3, 7, 1 };
        System.out.println(missingNum(arr));
    }
}
```

---

### 2. Better Approach (Hashing)
**Idea:** Use a frequency array (hash array) of size $n+1$. Mark the presence of each element from the input array in this hash array. Finally, iterate through the hash array from index 1 to $n$; the index with a value of 0 is the missing number.

* **Improvements:** Reduces time complexity significantly by using extra space.
* **Time Complexity:** $O(n)$
* **Space Complexity:** $O(n)$

**Java Code:**
```java
// Java program to find the missing number using hashing
import java.util.*;

class GfG {
    static int missingNum(int[] arr) {
        int n = arr.length + 1;

        // Create hash array of size n+1
        int[] hash = new int[n + 1];

        // Store frequencies of elements
        for (int i = 0; i < n - 1; i++) {
            hash[arr[i]]++;
        }

        // Find the missing number
        for (int i = 1; i <= n; i++) {
            if (hash[i] == 0) {
                return i;
            }
        }
        return -1;
    }

    public static void main(String[] args) {
        int[] arr = { 8, 2, 4, 5, 3, 7, 1 };
        System.out.println(missingNum(arr));
    }
}
```

---

### 3. Optimal Approach 1 (Sum Formula)
**Idea:** Calculate the expected sum of the first $n$ natural numbers using the formula $S = \frac{n(n+1)}{2}$. Then, calculate the actual sum of the elements in the array. The difference between the expected sum and the actual sum is the missing number.

* **Why Optimal:** It achieves $O(n)$ time with $O(1)$ extra space.
* **Time Complexity:** $O(n)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
// Java program to find the missing number using sum formula
import java.util.*;

class GfG {
    static int missingNum(int[] arr) {
        int n = arr.length + 1;

        // Calculate the sum of array elements
        int sum = 0;
        for (int i = 0; i < n - 1; i++) {
            sum += arr[i];
        }

        // Calculate the expected sum
        long expSum = (long)n * (n + 1) / 2;

        // Return the missing number
        return (int)(expSum - sum);
    }

    public static void main(String[] args) {
        int[] arr = { 8, 2, 4, 5, 3, 7, 1 };
        System.out.println(missingNum(arr));
    }
}
```

---

### 4. Optimal Approach 2 (XOR Operation)
**Idea:** XOR all numbers from $1$ to $n$ (let's call this `xor1`). Then XOR all elements present in the array (let's call this `xor2`). When you XOR `xor1` and `xor2` together, all numbers present in both will cancel out to 0, leaving only the missing number.

* **Why Optimal:** Like the sum formula, it is $O(n)$ time and $O(1)$ space, but it prevents potential integer overflow issues that can occur with large $n$ in the sum method.
* **Time Complexity:** $O(n)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
// Java program to find the missing number using XOR
import java.util.*;

class GfG {
    static int missingNum(int[] arr) {
        int n = arr.length + 1;
        int xor1 = 0, xor2 = 0;

        // XOR all array elements
        for (int i = 0; i < n - 1; i++) {
            xor2 ^= arr[i];
        }

        // XOR all numbers from 1 to n
        for (int i = 1; i <= n; i++) {
            xor1 ^= i;
        }

        // Missing number is the XOR of xor1 and xor2
        return xor1 ^ xor2;
    }

    public static void main(String[] args) {
        int[] arr = { 8, 2, 4, 5, 3, 7, 1 };
        System.out.println(missingNum(arr));
    }
}
```

---

## 🔹 Edge Cases
* **Array size is 1:** If `arr = [1]`, the range is `[1, 2]`, so the missing number is 2.
* **Missing number is the first (1) or last (n):** The logic should handle the boundaries of the range correctly.
* **Large $n$:** Ensure the sum approach uses `long` to avoid overflow (as seen in the provided code).

---

## 🔹 Important Notes / Takeaways
* **Sum vs. XOR:** Interviewers often prefer the **XOR approach** because it is more robust against overflow errors.
* **Hashing:** Good to mention if you have space to spare and need a very simple implementation, but usually not the "final" answer expected.
* **Pattern Recognition:** This problem is a gateway to "Find the Duplicate Number" or "Find the two missing numbers," which use similar XOR or mathematical tricks.

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity | Recommendation |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(n^2)$ | $O(1)$ | Too slow for large $n$. |
| **Hashing** | $O(n)$ | $O(n)$ | Fast, but uses extra memory. |
| **Sum Formula** | $O(n)$ | $O(1)$ | Optimal, but watch for overflow. |
| **XOR Operation** | $O(n)$ | $O(1)$ | **Most Optimal** (No overflow risk). |
---

11q
# Count Maximum Consecutive One's in the array

## 🔹 Problem Summary  
Given a binary array (containing only 0s and 1s), the goal is to find and return the maximum number of consecutive 1s present in the array. For example, in `{1, 1, 0, 1, 1, 1}`, the maximum consecutive 1s is **3**.

---

## 🔹 Key Observations & Intuition  
* **Streak Tracking:** We need a way to count the "current" streak of 1s and a way to remember the "best" streak seen so far.
* **The Reset:** Whenever we encounter a 0, the current streak is broken, and our counter must reset to zero.
* **Comparison:** Every time we increment our current streak, we should check if it has surpassed our previously recorded maximum.

---

## 🔹 Approaches  

### 1. Optimal Approach (Single Pass)
**Detailed Explanation:** 1.  Initialize two variables: `cnt` (to track the current streak) and `maxi` (to store the maximum streak found).
2.  Traverse the array from left to right.
3.  If the current element is `1`, increment `cnt`.
4.  If the current element is `0`, reset `cnt` to `0`.
5.  After each update to `cnt`, update `maxi = Math.max(maxi, cnt)`.
6.  Return `maxi`.

**Why it is optimal:** The algorithm only requires a single traversal of the array, making it $O(N)$. Since every element must be checked at least once to determine the maximum streak, this is the most efficient time complexity possible. It also uses only a constant amount of extra space ($O(1)$).

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum consecutive 1's in an array
    public int findMaxConsecutiveOnes(int[] nums) {
        // Variable to store current count of consecutive 1's
        int cnt = 0;
        // Variable to store maximum consecutive 1's
        int maxi = 0;
        // Traverse the array
        for (int i = 0; i < nums.length; i++) {
            // If current element is 1, increment count
            if (nums[i] == 1) {
                cnt++;
            } else {
                // If element is 0, reset count
                cnt = 0;
            }

            // Update maximum if current count is greater
            maxi = Math.max(maxi, cnt);
        }
        // Return maximum consecutive 1's
        return maxi;
    }
}

public class Main {
    public static void main(String[] args) {
        // Input array
        int nums[] = {1, 1, 0, 1, 1, 1};
        // Create Solution object
        Solution obj = new Solution();
        // Get answer
        int ans = obj.findMaxConsecutiveOnes(nums);
        // Print result
        System.out.println("The maximum consecutive 1's are " + ans);
    }
}
```

---

## 🔹 Edge Cases  
* **All Zeros:** `cnt` will always reset, and `maxi` will remain 0.
* **All Ones:** `cnt` will increment until the end of the array, and `maxi` will equal the array length.
* **Single Element:** If it's 1, returns 1; if it's 0, returns 0.
* **Alternating 0s and 1s:** The streak will never exceed 1.

---

## 🔹 Important Notes / Takeaways  
* **Greedy Comparison:** Updating `maxi` inside the loop ensures we don't miss the streak if the array ends with 1s (though some implementations do it only when encountering a 0, which requires an extra check after the loop).
* **Interview Tip:** This problem is often a warm-up for "Sliding Window" problems, such as "Max Consecutive Ones III" (where you can flip $k$ zeros).

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Optimal (Single Pass)** | $O(N)$ | $O(1)$ | Use a counter and a global maximum variable. |
---
12q
# Find the number that appears once, and the other numbers twice

## 🔹 Problem Summary  
Given a non-empty array of integers, every element appears twice except for one. Your task is to find and return that single element. For example, in the array `{4, 1, 2, 1, 2}`, the result is `4`.

---

## 🔹 Key Observations & Intuition  
* **Frequency Counting:** The most straightforward way to solve this is to count how many times each number appears.
* **XOR Magic:** A bitwise property allows us to cancel out numbers that appear in pairs. Since $a \oplus a = 0$ and $a \oplus 0 = a$, XORing all elements together will leave only the single element.
* **Hashing:** Using a hash table or frequency array allows for faster lookups compared to nested loops.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** For every element in the array, perform a linear search across the entire array to count its occurrences. If the count for any element is 1, that is our answer.

* **Time Complexity:** $O(N^2)$ due to nested loops.
* **Space Complexity:** $O(1)$ as no extra data structures are used.

**Java Code:**
```java
import java.util.*;

public class Solution {
    public static int getSingleElement(int []arr) {
        // Size of the array:
        int n = arr.length;

        // Run a loop for selecting elements:
        for (int i = 0; i < n; i++) {
            int num = arr[i]; // selected element
            int cnt = 0;

            // Iterating the entire array to find occurrences:
            for (int j = 0; j < n; j++) {
                if (arr[j] == num)
                    cnt++;
            }

            // If occurrences is 1, return the number:
            if (cnt == 1) return num;
        }

        // The following line will never execute 
        // if the condition is guaranteed:
        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {4, 1, 2, 1, 2};
        int ans = getSingleElement(arr);
        System.out.println("The single element is: " + ans);
    }
}
```

---

### 2. Better Approach (Hashing)  
**Idea:** Optimize the search by using an array to store frequencies. First, find the maximum element to determine the size of the hash array. Then, count frequencies in one pass and find the element with frequency 1 in another.

* **Improvements over brute:** Reduces time complexity by using more space.
* **Complexity:** * **Time:** $O(N) + O(N) + O(N) = O(3N) \approx O(N)$
    * **Space:** $O(\text{maxElement} + 1)$

**Java Code:**
```java
import java.util.*;

public class Solution {
    public static int getSingleElement(int []arr) {
        // Size of the array:
        int n = arr.length;

        // Find the maximum element:
        int maxi = arr[0];
        for (int i = 0; i < n; i++) {
            maxi = Math.max(maxi, arr[i]);
        }

        // Declare hash array of size maxi+1
        // And hash the elements:
        int[] hash = new int[maxi + 1];
        for (int i = 0; i < n; i++) {
            hash[arr[i]]++;
        }

        // Find the single element:
        for (int i = 0; i < n; i++) {
            if (hash[arr[i]] == 1)
                return arr[i];
        }

        // This line will never execute
        // if the condition is guaranteed:
        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {4, 1, 2, 1, 2};
        int ans = getSingleElement(arr);
        System.out.println("The single element is: " + ans);
    }
}
```

---

### 3. Optimal Approach (XOR)  
**Detailed Explanation:** We use the bitwise XOR operator. The logic relies on two properties:
1.  $X \oplus X = 0$ (Two identical numbers cancel each other out).
2.  $X \oplus 0 = X$ (Any number XORed with zero remains unchanged).
By XORing every element in the array, all pairs will become zero, and $0 \oplus \text{singleElement}$ will result in the single element.

**Why it is optimal:** It only requires one pass through the array and uses no extra space at all.

* **Complexity:** * **Time:** $O(N)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Solution {
    public static int getSingleElement(int []arr) {
        // Size of the array:
        int n = arr.length;

        // XOR all the elements:
        int xorr = 0;
        for (int i = 0; i < n; i++) {
            xorr = xorr ^ arr[i];
        }
        return xorr;
    }

    public static void main(String args[]) {
        int[] arr = {4, 1, 2, 1, 2};
        int ans = getSingleElement(arr);
        System.out.println("The single element is: " + ans);
    }
}
```

---

## 🔹 Edge Cases  
* **Array with 1 element:** The XOR sum starts at 0 and immediately becomes that element.
* **Large Values:** The XOR approach works for any integer value, whereas the Hash Array approach fails if values are extremely large (e.g., $10^9$).
* **Negative Numbers:** The Hash Array approach fails with negative indices; XOR handles them perfectly.

---

## 🔹 Important Notes / Takeaways  
* **Bit Manipulation:** XOR is a powerful tool for "pairing" problems. Always consider it when you see elements appearing twice.
* **Hashing Alternatives:** If the elements are very large, you should use a `HashMap<Integer, Integer>` instead of a frequency array to keep space complexity $O(N)$ rather than $O(\text{maxElement})$.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Simple but very slow. |
| **Better (Hashing)** | $O(N)$ | $O(\text{maxElement})$ | Faster, but space-intensive. |
| **Optimal (XOR)** | $O(N)$ | $O(1)$ | **Most efficient in both time and space.** |
---

13q 
# Longest Subarray with given Sum K (Positives)

## 🔹 Problem Summary  
Given an array `nums` of size `n` and an integer `k`, find the length of the **longest sub-array** that sums up exactly to `k`. If no such sub-array exists, return `0`. This version of the problem specifically focuses on arrays containing **positives and zeros**.

---

## 🔹 Key Observations & Intuition  
* **Subarray vs. Subset:** A subarray must be a contiguous part of the array.
* **Monotonicity:** Since the elements are positive, as we add more elements, the sum strictly increases (or stays the same if 0 is added). This allows us to use a **Sliding Window** or **Two-Pointer** approach effectively.
* **Expansion & Contraction:** We expand the window to increase the sum and contract it from the left to decrease the sum when it exceeds `k`.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Generate all possible subarrays using two nested loops for the start and end indices. For every subarray, use a third loop to calculate the sum. If the sum equals `k`, update the maximum length.

* **Time Complexity:** $O(n^3)$ due to three nested loops.
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int getLongestSubarray(int []a, long k) {
        int n = a.length; // size of the array.

        int len = 0;
        for (int i = 0; i < n; i++) { // starting index
            for (int j = i; j < n; j++) { // ending index
                // add all the elements of subarray = a[i...j]:
                long s = 0;
                for (int K = i; K <= j; K++) {
                    s += a[K];
                }

                if (s == k)
                    len = Math.max(len, j - i + 1);
            }
        }
        return len;
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 5, 1, 9};
        long k = 10;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

### 2. Better Approach (Using Hashing)  
**Idea:** This approach uses a prefix sum and a hash map. We store the prefix sum at each index. If `(current_sum - k)` exists in the map, it means a subarray with sum `k` exists between that stored index and the current index.
*Note: This is the optimal approach if the array contains negatives.*

* **Improvements over brute:** Reduces time to linear or near-linear but uses extra space.
* **Complexity:** * **Time:** $O(N)$ or $O(N \log N)$ depending on the Map implementation.
    * **Space:** $O(N)$ to store prefix sums.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int getLongestSubarray(int []a, long k) {
        int n = a.length; // size of the array.

        Map<Long, Integer> preSumMap = new HashMap<>();
        long sum = 0;
        int maxLen = 0;
        for (int i = 0; i < n; i++) {
            //calculate the prefix sum till index i:
            sum += a[i];

            // if the sum = k, update the maxLen:
            if (sum == k) {
                maxLen = Math.max(maxLen, i + 1);
            }

            // calculate the value of remaining portion i.e. x-k:
            long rem = sum - k;

            //Calculate the length and update maxLen:
            if (preSumMap.containsKey(rem)) {
                int len = i - preSumMap.get(rem);
                maxLen = Math.max(maxLen, len);
            }

            //Finally, update the map checking the conditions:
            if (!preSumMap.containsKey(sum)) {
                preSumMap.put(sum, i);
            }
        }

        return maxLen;
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 5, 1, 9};
        long k = 10;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

### 3. Optimal Approach (Two Pointers)  
**Detailed Explanation:** 1. Use two pointers, `left` and `right`, both starting at index 0.
2. Move `right` forward, adding `nums[right]` to the `sum`.
3. If the `sum` exceeds `k`, move `left` forward and subtract `nums[left]` from `sum` until `sum <= k`.
4. If `sum == k`, calculate the current subarray length (`right - left + 1`) and update `maxLen`.
5. Repeat until `right` reaches the end of the array.

**Why it is optimal:** It processes each element at most twice (once by `right`, once by `left`), ensuring $O(N)$ time, and uses no extra data structures, ensuring $O(1)$ space.

* **Complexity:** * **Time:** $O(2N) \approx O(N)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int getLongestSubarray(int []a, long k) {
        int n = a.length; // size of the array.

        int left = 0, right = 0; // 2 pointers
        long sum = a[0];
        int maxLen = 0;
        while (right < n) {
            // if sum > k, reduce the subarray from left
            // until sum <= k:
            while (left <= right && sum > k) {
                sum -= a[left];
                left++;
            }

            // if sum = k, update the maxLen i.e. answer:
            if (sum == k) {
                maxLen = Math.max(maxLen, right - left + 1);
            }

            // Move forward throught the right pointer:
            right++;
            if (right < n) sum += a[right];
        }

        return maxLen;
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 5, 1, 9};
        long k = 10;
        int len = getLongestSubarray(a, k);
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

## 🔹 Edge Cases  
* **Array with Zeros:** Zeros don't increase the sum but do increase the length. The two-pointer approach handles this, but hashing requires a check (`!preSumMap.containsKey(sum)`) to keep the *first* occurrence for maximum length.
* **k is larger than total sum:** Returns 0.
* **Single element equals k:** Returns 1.

---

## 🔹 Important Notes / Takeaways  
* **Positives vs. Negatives:** The Two-Pointer approach **ONLY** works for positives. If the array contains negative numbers, you **must** use the Hashing (Prefix Sum) approach because the sum is no longer monotonic.
* **Interview Insight:** Always ask the interviewer if the array contains negative numbers before choosing the optimal approach.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Best For |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^3)$ or $O(N^2)$ | $O(1)$ | Small inputs |
| **Hashing** | $O(N)$ | $O(N)$ | Arrays with **Negatives** |
| **Two Pointers** | $O(N)$ | $O(1)$ | Arrays with **Positives only** |
---
14q 
# Length of the Longest Subarray with Zero Sum

## 🔹 Problem Summary  
Given an array containing both positive and negative integers, the task is to find the length of the **longest subarray** where the sum of all elements equals **zero**. For example, in the array `{15, -2, 2, -8, 1, 7, 10, 23}`, the subarray `{-2, 2, -8, 1, 7}` sums to 0, and its length is 5.

---

## 🔹 Key Observations & Intuition  
* **Prefix Sum Logic:** If the sum of elements from index `0` to `i` is $S$, and the sum from index `0` to `j` ($j > i$) is also $S$, then the sum of the elements from index `i+1` to `j` must be **zero**.
* **Hashing for Speed:** By storing the first occurrence of every prefix sum in a hash map, we can quickly check if a current prefix sum has appeared before. If it has, we calculate the distance between the current index and the stored index.
* **The Zero Case:** If the prefix sum itself becomes zero at any point, the subarray from the very beginning (index 0) to the current index has a sum of zero.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Generate every possible subarray using nested loops and calculate their sums. If a subarray sum is zero, compare its length with the maximum length found so far.

* **Time Complexity:** $O(N^2)$ (Two nested loops to find all subarrays).
* **Space Complexity:** $O(1)$ (No extra space used).

**Java Code:**
```java
import java.util.*;

class Solution {
    // Brute force approach to find the longest subarray with sum 0
    static int solve(int a[], int n) {
        int maxLen = 0;
        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += a[j];
                if (sum == 0) {
                    maxLen = Math.max(maxLen, j - i + 1);
                }
            }
        }
        return maxLen;
    }

    public static void main(String args[]) {
        int a[] = {9, -3, 3, -1, 6, -5};
        int n = a.length;
        System.out.println(solve(a, n));
    }
}
```

---

### 2. Optimal Approach (Prefix Sum + Hashing)  
**Detailed Explanation:** 1.  Initialize `sum = 0` and `maxi = 0`.
2.  Create a `HashMap` to store the prefix sum as the key and the index as the value.
3.  Traverse the array:
    * Add the current element to `sum`.
    * **Case 1:** If `sum == 0`, the subarray from index 0 to $i$ has sum 0. Update `maxi = i + 1`.
    * **Case 2:** Check if `sum` is already in the map. 
        * If **yes**, a zero-sum subarray exists between the previous index of this sum and the current index. Update `maxi = Math.max(maxi, i - map.get(sum))`.
        * If **no**, add the `sum` and current index `i` to the map.

**Why it is optimal:** It processes the array in a single pass ($O(N)$), and hash map lookups are $O(1)$ on average.

* **Complexity:** * **Time Complexity:** $O(N)$
    * **Space Complexity:** $O(N)$ (To store prefix sums in the map).

**Java Code:**
```java
import java.util.*;

class Solution {
    // Optimal approach using HashMap
    static int maxLen(int A[], int n) {
        // HashMap to store (prefix_sum, index)
        HashMap<Integer, Integer> mpp = new HashMap<Integer, Integer>();

        int maxi = 0;
        int sum = 0;

        for (int i = 0; i < n; i++) {
            sum += A[i];

            if (sum == 0) {
                maxi = i + 1;
            } else {
                if (mpp.get(sum) != null) {
                    // If sum seen before, update maxi
                    maxi = Math.max(maxi, i - mpp.get(sum));
                } else {
                    // If sum seen for the first time, store it
                    mpp.put(sum, i);
                }
            }
        }
        return maxi;
    }

    public static void main(String args[]) {
        int a[] = {9, -3, 3, -1, 6, -5};
        int n = a.length;
        System.out.println(maxLen(a, n));
    }
}
```

---

## 🔹 Edge Cases  
* **No zero-sum subarray:** The function will return 0.
* **Entire array sums to zero:** The condition `sum == 0` will handle this and return the full length of the array.
* **Single element is zero:** The map or the `sum == 0` check will correctly identify a subarray of length 1.

---

## 🔹 Important Notes / Takeaways  
* **Don't Update Indices:** If a prefix sum is already in the map, **do not** update its index. We want the *first* occurrence to maximize the subarray length.
* **Difference from "Longest Subarray with Sum K":** While the logic is similar, the `sum == 0` check is a specific shortcut for this problem.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Nested loops to check every subarray. |
| **Optimal** | $O(N)$ | $O(N)$ | **Prefix Sum + Hash Map (Tracking first occurrence).** |

---
...
# Medium Problems 
1a
# [Two Sum: Check if a pair with given sum exists in Array](https://takeuforward.org/data-structure/two-sum-check-if-a-pair-with-given-sum-exists-in-array?mode=track&sheet=a2z-dsa)

## 🔹 Problem Summary
Given an array of integers `arr[]` and an integer `target`, identify if there are two numbers that sum up to the target.
* **1st variant:** Return **YES** if such a pair exists, otherwise return **NO**.
* **2nd variant:** Return the **indices** of the two numbers. If no such pair exists, return **{-1, -1}**.

---

## 🔹 Key Observations & Intuition
* **Complement Search:** For every element $x$, we are searching for $target - x$.
* **Hashing:** Storing elements in a `HashMap` allows us to check for the complement in $O(1)$ time.
* **Two-Pointer Greedy:** If the array is sorted, we can use two pointers. If the `sum < target`, we need a larger value (increment left). If `sum > target`, we need a smaller value (decrement right).

---

## 🔹 Approaches

### 1. Brute Force
**Idea:** For each element, traverse the remaining array to find another element that completes the sum. We start the inner loop from `i + 1` to avoid checking the same pair twice or using the same element twice.

* **Time Complexity:** $O(N^2)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to check if any two numbers sum up to target (variant 1)
    public String twoSumExists ( int [] arr, int target) {
        int n = arr.length;
        // Outer loop picks one element at a time
        for ( int i = 0 ; i < n; i++) {
            // Inner loop searches for another element that complements arr[i]
            for ( int j = i + 1 ; j < n; j++) {
                // If sum equals target, return "YES"
                if (arr[i] + arr[j] == target) {
                    return "YES" ;
                }
            }
        }
        // No pair found that sums to target
        return "NO" ;
    }

    // Function to return indices of two numbers that sum to target (variant 2)
    public int [] twoSumIndices( int [] arr, int target) {
        int n = arr.length;
        // Outer loop picks one element at a time
        for ( int i = 0 ; i < n; i++) {
            // Inner loop searches for another element that complements arr[i]
            for ( int j = i + 1 ; j < n; j++) {
                // If sum equals target, return the pair of indices
                if (arr[i] + arr[j] == target) {
                    return new int []{i, j};
                }
            }
        }
        // No such pair found
        return new int []{- 1 , - 1 };
    }
}

public class Main {
    public static void main (String[] args) {
        Solution sol = new Solution ();
        int [] arr = { 2 , 6 , 5 , 8 , 11 };
        int target = 14 ;
        // Variant 1
        System.out.println(sol.twoSumExists(arr, target));
        // Variant 2
        int [] res = sol.twoSumIndices(arr, target);
        System.out.println( "[" + res[ 0 ] + ", " + res[ 1 ] + "]" );
    }
}
```

---

### 2. Better Approach (Hashing)
**Idea:** Use a `HashMap` to store elements as we iterate. For the current element, check if its complement (`target - arr[i]`) is already in the map. If yes, we found our pair.

* **Improvements over brute:** Reduces time complexity from $O(N^2)$ to $O(N)$ by avoiding the nested loop.
* **Complexity:** * **Time:** $O(N)$
    * **Space:** $O(N)$

**Java Code:**
```java
import java.util.HashMap;

class Solution {
    // Variant 1: Check if two numbers sum to target using hashing
    public String twoSumExists ( int [] arr, int target) {
        HashMap<Integer, Integer> map = new HashMap <>();
        // Iterate over all elements
        for ( int i = 0 ; i < arr.length; i++) {
            int complement = target - arr[i];
            // Check if complement exists in map
            if (map.containsKey(complement)) {
                return "YES" ; // Pair found
            }
            // Store current element and its index
            map.put(arr[i], i);
        }
        // No pair found
        return "NO" ;
    }

    // Variant 2: Return indices of two numbers that sum to target using hashing
    public int [] twoSumIndices( int [] arr, int target) {
        HashMap<Integer, Integer> map = new HashMap <>();
        for ( int i = 0 ; i < arr.length; i++) {
            int complement = target - arr[i];
            // If complement found, return indices
            if (map.containsKey(complement)) {
                return new int [] { map.get(complement), i };
            }
            // Store current element and index
            map.put(arr[i], i);
        }
        // No pair found
        return new int [] { - 1 , - 1 };
    }
}

public class Main {
    public static void main (String[] args) {
        Solution sol = new Solution ();
        int [] arr = { 2 , 6 , 5 , 8 , 11 };
        int target = 14 ;

        System.out.println(sol.twoSumExists(arr, target));
        int [] res = sol.twoSumIndices(arr, target);
        System.out.println( "[" + res[ 0 ] + ", " + res[ 1 ] + "]" );
    }
}
```

---

### 3. Optimal Approach (Two Pointers)
**Detailed Explanation:** First, sort the array. However, since we need to return original indices for Variant 2, we store each value with its original index before sorting. Use a `left` pointer at index `0` and a `right` pointer at `n-1`. Compare their sum to the target and move pointers accordingly.

**Why it is optimal:** It is the most efficient way to solve the problem if the array is already sorted ($O(N)$). If unsorted, sorting makes it $O(N \log N)$, but it is often considered "optimal" for space if the hashing overhead is unwanted.

* **Complexity:**
    * **Time:** $O(N \log N)$ (due to sorting)
    * **Space:** $O(N)$ (to store original indices)

**Java Code:**
```java
import java.util.Arrays;

class Solution {
    // Variant 1: Check if two numbers sum to target using two-pointer approach
    public String twoSumExists ( int [] arr, int target) {
        int n = arr.length;
        // Create an array of pairs [value, original_index]
        int [][] numsWithIndex = new int [n][ 2 ];
        // Store each element with its original index
        for ( int i = 0 ; i < n; i++) {
            numsWithIndex[i][ 0 ] = arr[i]; // value
            numsWithIndex[i][ 1 ] = i;      // original index
        }
        // Sort the array based on the value, not index
        Arrays.sort(numsWithIndex, (a, b) -> Integer.compare(a[ 0 ], b[ 0 ]));
        // Initialize two pointers: one at start, one at end
        int left = 0 , right = n - 1 ;
        // Run loop until pointers cross
        while (left < right) {
            // Calculate the sum of values at pointers
            int sum = numsWithIndex[left][ 0 ] + numsWithIndex[right][ 0 ];
            if (sum == target) {
                // Found the pair, return "YES"
                return "YES" ;
            } else if (sum < target) {
                // Sum is less than target, so move left pointer right to increase sum
                left++;
            } else {
                // Sum is greater than target, so move right pointer left to decrease sum
                right--;
            }
        }
        // If loop ends without returning, no pair found
        return "NO" ;
    }

    // Variant 2: Return indices of two numbers that sum to target
    public int [] twoSumIndices( int [] arr, int target) {
        int n = arr.length;
        int [][] numsWithIndex = new int [n][ 2 ];
        // Store element with original index
        for ( int i = 0 ; i < n; i++) {
            numsWithIndex[i][ 0 ] = arr[i];
            numsWithIndex[i][ 1 ] = i;
        }
        // Sort by the value to apply two-pointer
        Arrays.sort(numsWithIndex, (a, b) -> Integer.compare(a[ 0 ], b[ 0 ]));
        int left = 0 , right = n - 1 ;
        while (left < right) {
            int sum = numsWithIndex[left][ 0 ] + numsWithIndex[right][ 0 ];
            if (sum == target) {
                // Return original indices of the two numbers found
                return new int [] {numsWithIndex[left][ 1 ], numsWithIndex[right][ 1 ]};
            } else if (sum < target) {
                // Increase sum by moving left pointer forward
                left++;
            } else {
                // Decrease sum by moving right pointer backward
                right--;
            }
        }
        // No pair found
        return new int [] {- 1 , - 1 };
    }
}

public class Main {
    public static void main (String[] args) {
        Solution sol = new Solution ();
        int [] arr = { 2 , 6 , 5 , 8 , 11 };
        int target = 14 ;

        System.out.println(sol.twoSumExists(arr, target)); // Output: YES
        int [] res = sol.twoSumIndices(arr, target);
        System.out.println( "[" + res[ 0 ] + ", " + res[ 1 ] + "]" ); // Output: [1, 3]
    }
}
```

---

## 🔹 Edge Cases
* **No Solution:** Handled by returning "NO" or `{-1, -1}`.
* **Same Element usage:** The approaches ensure an element isn't added to itself (inner loop starts at `i+1` or hashing checks for complement *before* adding the current number).
* **Duplicate Values:** Hashing and sorting both handle duplicate values correctly.

---

## 🔹 Important Notes / Takeaways
* **Time-Space Tradeoff:** Hashing is faster ($O(N)$) but uses more space ($O(N)$). Brute force is slow but uses no space.
* **Sorting Requirement:** The Two-Pointer approach effectively requires the array to be sorted.

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ |
| **Better (Hashing)** | $O(N)$ | $O(N)$ |
| **Optimal (Two Pointers)** | $O(N \log N)$ | $O(N)$ |
---
2a 
# [Sort an array of 0s, 1s and 2s](https://takeuforward.org/data-structure/sort-an-array-of-0s-1s-and-2s?mode=track&sheet=a2z-dsa)

## 🔹 Problem Summary  
Given an array `nums` consisting only of 0s, 1s, or 2s, sort the array in non-decreasing order. The sorting must be done **in-place** without making a copy of the original array.

---

## 🔹 Key Observations & Intuition  
* **Fixed Range:** Since there are only three distinct values (0, 1, 2), we can use counting techniques.
* **Partitioning:** The optimal approach involves partitioning the array into three sections: one for 0s, one for 1s, and one for 2s.
* **Dutch National Flag Algorithm:** This is a classic problem solved by three pointers that maintain the invariant that all elements to the left of `low` are 0s, and all elements to the right of `high` are 2s.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Simply use a standard sorting algorithm like Merge Sort or Quick Sort. While this works, it doesn't take advantage of the fact that there are only three unique numbers.

* **Time Complexity:** $O(N \log N)$
* **Space Complexity:** $O(1)$ (if using heapsort) or $O(N)$ (if using mergesort).

**Java Code:**
```java
import java.util.*;

class Solution {
    public void sortZeroOneTwo(int[] nums) {
        // Using built-in sort as a brute force approach
        Arrays.sort(nums);
    }
}
```

---

### 2. Better Approach  
**Idea:** Traverse the array once to count the total number of 0s, 1s, and 2s. Then, in a second pass, overwrite the array with the appropriate number of 0s, followed by 1s, and finally 2s.

* **Improvements over brute:** Reduces time complexity to linear $O(N)$.
* **Complexity:** * **Time:** $O(N) + O(N) = O(2N) \approx O(N)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to sort the array containing only 0s, 1s and 2s
    public void sortZeroOneTwo(int[] nums) {
        // Initialize count variables for 0s, 1s, and 2s
        int count0 = 0, count1 = 0, count2 = 0;

        // Count the frequency of 0s, 1s, and 2s
        for (int num : nums) {
            if (num == 0) count0++;
            else if (num == 1) count1++;
            else count2++;
        }

        // Overwrite the array with sorted values
        int index = 0;

        // Fill with 0s
        while (count0-- > 0) {
            nums[index++] = 0;
        }

        // Fill with 1s
        while (count1-- > 0) {
            nums[index++] = 1;
        }

        // Fill with 2s
        while (count2-- > 0) {
            nums[index++] = 2;
        }
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        int[] nums = {1, 0, 2, 1, 0};
        Solution obj = new Solution();
        obj.sortZeroOneTwo(nums);

        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

### 3. Optimal Approach (Dutch National Flag Algorithm)  
**Detailed Explanation:** We use three pointers: `low`, `mid`, and `high`.
1.  `low` and `mid` start at the beginning (0), and `high` starts at the end ($n-1$).
2.  The goal is to ensure:
    * `nums[0...low-1]` contains only 0s.
    * `nums[low...mid-1]` contains only 1s.
    * `nums[high+1...n-1]` contains only 2s.
3.  We iterate while `mid <= high`:
    * If `nums[mid] == 0`: Swap `nums[low]` and `nums[mid]`, increment both `low` and `mid`.
    * If `nums[mid] == 1`: Just increment `mid`.
    * If `nums[mid] == 2`: Swap `nums[mid]` and `nums[high]`, decrement `high`.

**Why it is optimal:** It sorts the array in a **single pass** with $O(1)$ extra space.

* **Complexity:** * **Time:** $O(N)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to sort the array using the Dutch National Flag algorithm
    public void sortZeroOneTwo(int[] nums) {
        int low = 0, mid = 0, high = nums.length - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
                // Swap nums[low] and nums[mid]
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;

                low++;
                mid++;
            } else if (nums[mid] == 1) {
                // Move mid pointer
                mid++;
            } else {
                // Swap nums[mid] and nums[high]
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;

                high--;
            }
        }
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        int[] nums = {1, 0, 2, 1, 0};
        Solution obj = new Solution();
        obj.sortZeroOneTwo(nums);

        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 🔹 Edge Cases  
* **All elements are the same:** (e.g., `[0, 0, 0]`) The algorithm handles this without unnecessary swaps.
* **Array already sorted:** (e.g., `[0, 1, 2]`) Pointers move through the array correctly.
* **Array containing only two types:** (e.g., `[0, 2, 0]`) The logic remains consistent.

---

## 🔹 Important Notes / Takeaways  
* **Dutch National Flag:** This algorithm is the standard for 3-way partitioning.
* **In-place:** Notice we don't return a new array; we modify the existing one.
* **Comparison:** While the "Better" approach is also $O(N)$, the "Optimal" approach is superior because it only traverses the array **once**.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Passes |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N \log N)$ | $O(1)$ | 1 |
| **Better (Counting)** | $O(N)$ | $O(1)$ | 2 |
| **Optimal (DNF)** | $O(N)$ | $O(1)$ | **1** |
---
3a

# [Find the Majority Element that occurs more than N/2 times](https://takeuforward.org/data-structure/find-the-majority-element-that-occurs-more-than-n-2-times?mode=track&sheet=a2z-dsa)

## 🔹 Problem Summary  
Given an array of **N** integers, write a program to return the **majority element**. The majority element is the element that appears more than **⌊N/2⌋** times in the array. You may assume that the majority element always exists in the array.

---

## 🔹 Key Observations & Intuition  
* **Frequency Constraint:** Since the majority element appears more than half the time, there can only ever be **one** such element in any given array.
* **Cancellation Property:** If we pair the majority element with any other different element, the majority element will still remain "left over" because its count exceeds the sum of all other elements.
* **Trade-offs:** We can solve this by counting (Brute), using memory to track frequencies (Better), or using a clever cancellation logic (Optimal).

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** For each element in the array, run another loop to count its total occurrences. If the count of any element is greater than $N/2$, return that element.

* **Time Complexity:** $O(N^2)$ — Nested loops to count occurrences for each element.
* **Space Complexity:** $O(1)$ — No extra space used.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int majorityElement(int []v) {
        //size of the given array:
        int n = v.length;

        for (int i = 0; i < n; i++) {
            //selected element is v[i]
            int cnt = 0;
            for (int j = 0; j < n; j++) {
                // counting the frequency of v[i]
                if (v[j] == v[i]) {
                    cnt++;
                }
            }

            // check if frquency is greater than n/2:
            if (cnt > (n / 2))
                return v[i];
        }

        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};
        int ans = majorityElement(arr);
        System.out.println("The majority element is: " + ans);
    }
}
```

---

### 2. Better Approach (Using Hashing)  
**Idea:** Use a Hash Map to store the frequency of each element. While traversing and updating the map, check if any element's frequency has crossed $N/2$.

* **Improvements over brute:** Reduces time complexity significantly by using extra space to store counts.
* **Complexity:** * **Time:** $O(N \log N)$ or $O(N)$ — Depending on whether you use a `TreeMap` or `HashMap`.
    * **Space:** $O(N)$ — To store frequencies in the Map.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int majorityElement(int []v) {
        //size of the given array:
        int n = v.length;

        //declaring a map:
        HashMap<Integer, Integer> mpp = new HashMap<>();

        //storing the elements with its occurence:
        for (int i = 0; i < n; i++) {
            int value = mpp.getOrDefault(v[i], 0);
            mpp.put(v[i], value + 1);
        }

        //searching for the majority element:
        for (Map.Entry<Integer, Integer> it : mpp.entrySet()) {
            if (it.getValue() > (n / 2)) {
                return it.getKey();
            }
        }

        return -1;
    }

    public static void main(String args[]) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};
        int ans = majorityElement(arr);
        System.out.println("The majority element is: " + ans);
    }
}
```

---

### 3. Optimal Approach (Moore’s Voting Algorithm)  
**Detailed Explanation:** 1. Initialize a `candidate` and a `count = 0`.  
2. Traverse the array:
   - If `count == 0`, set the current element as the `candidate`.
   - If current element equals `candidate`, increment `count`.
   - Else, decrement `count`.
3. The remaining `candidate` after the loop is the potential majority element.
4. **Verification Step:** Check if the candidate's count in the array is actually $> N/2$ (Optional if the problem guarantees a majority element exists).

**Why it is optimal:** It processes the array in a **single pass** and uses **constant space**. It effectively "cancels out" pairs of different elements, and since the majority element appears more than $N/2$ times, it is guaranteed to survive the cancellation.

* **Complexity:** * **Time:** $O(N)$ — Single pass for voting + optional pass for verification.
    * **Space:** $O(1)$ — Only a few variables used.

**Java Code:**
```java
import java.util.*;

public class Solution {
    public static int majorityElement(int []v) {
        //size of the given array:
        int n = v.length;
        int cnt = 0; // count
        int el = 0; // Element

        //applying the algorithm:
        for (int i = 0; i < n; i++) {
            if (cnt == 0) {
                cnt = 1;
                el = v[i];
            } else if (el == v[i]) cnt++;
            else cnt--;
        }

        //checking if the stored element
        // is the majority element:
        int cnt1 = 0;
        for (int i = 0; i < n; i++) {
            if (v[i] == el) cnt1++;
        }

        if (cnt1 > (n / 2)) return el;
        return -1;
    }
}

// Separate Main class for execution
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};

        // Create an instance of Solution class
        Solution sol = new Solution();

        // Call the majorityElement function
        int ans = sol.majorityElement(arr);

        // Print the majority element
        System.out.println("The majority element is: " + ans);
    }
}
```

---

## 🔹 Edge Cases  
* **Array Size 1:** The single element is automatically the majority element.
* **All Elements Same:** The algorithm will correctly pick the element with count $N$.
* **No Majority Element:** Moore's Voting Algorithm will return a candidate, but the **verification step** will return -1, correctly identifying no majority exists.

---

## 🔹 Important Notes / Takeaways  
* **Moore's Voting Algorithm:** This is a top-tier interview pattern. Remember the intuition of "cancellation."
* **Guaranteed Existence:** Many problems state the majority element *always* exists; in that case, the verification step can be skipped to save a pass.
* **N/3 Variation:** There is a similar problem (Majority Element II) asking for elements occurring $> N/3$ times, which uses an extended version of this voting logic.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Simple but inefficient. |
| **Hashing** | $O(N)$ | $O(N)$ | Good if extra space is allowed. |
| **Moore's Voting** | $O(N)$ | $O(1)$ | **Optimal solution for interviews.** |

--- 
4a

# [Kadane's Algorithm : Maximum Subarray Sum in an Array](https://takeuforward.org/data-structure/kadanes-algorithm-maximum-subarray-sum-in-an-array?mode=track&sheet=a2z-dsa)

## 🔹 Problem Summary  
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

---

## 🔹 Key Observations & Intuition  
* **Contiguous:** The elements must be adjacent.
* **Positive vs. Negative:** A positive sum contributes to future potential maximums. However, if a prefix sum becomes negative, it will only decrease the sum of any future subarray. 
* **The "Reset" Logic:** If the sum of the subarray we are currently tracking drops below zero, we discard it and start a new subarray from the next element.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Check the sum of every possible subarray. We use three nested loops: the first two to define the starting and ending boundaries, and the third to calculate the sum of that specific range.

* **Time Complexity:** $O(N^3)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int maxSubarraySum(int[] arr, int n) {
        int maxi = Integer.MIN_VALUE; // maximum sum

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                // subarray = arr[i..j]
                int sum = 0;

                //add all the elements of subarray:
                for (int k = i; k <= j; k++) {
                    sum += arr[k];
                }

                maxi = Math.max(maxi, sum);
            }
        }

        return maxi;
    }

    public static void main(String args[]) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4};
        int n = arr.length;
        int maxSum = maxSubarraySum(arr, n);
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### 2. Better Approach  
**Idea:** Optimize the brute force by realizing that the sum of `arr[i...j]` is simply the sum of `arr[i...j-1]` plus `arr[j]`. This eliminates the third loop.

* **Improvements over brute:** Reduced one nested loop.
* **Complexity:** * **Time:** $O(N^2)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int maxSubarraySum(int[] arr, int n) {
        int maxi = Integer.MIN_VALUE; // maximum sum

        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                // current subarray = arr[i.....j]

                //add the current element arr[j]
                // to the sum i.e. sum of arr[i...j-1]
                sum += arr[j];

                maxi = Math.max(maxi, sum);
            }
        }

        return maxi;
    }

    public static void main(String args[]) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4};
        int n = arr.length;
        int maxSum = maxSubarraySum(arr, n);
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### 3. Optimal Approach (Kadane's Algorithm)  
**Detailed Explanation:** 1. Maintain a running `sum` and a global `maxi`.
2. Iterate through the array, adding the current element to `sum`.
3. If `sum > maxi`, update `maxi`.
4. **Crucial Step:** If `sum < 0`, reset `sum` to `0`. This is because a negative sum will only reduce the value of any subsequent subarray.

**Why it is optimal:** It solves the problem in a single pass ($O(N)$) by making a greedy choice at each step: "Is it better to carry over the previous sum, or start fresh?"

* **Complexity:** * **Time:** $O(N)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static long maxSubarraySum(int[] arr, int n) {
        long maxi = Long.MIN_VALUE; // maximum sum
        long sum = 0;

        for (int i = 0; i < n; i++) {

            sum += arr[i];

            if (sum > maxi) {
                maxi = sum;
            }

            // If sum < 0: discard the sum calculated
            if (sum < 0) {
                sum = 0;
            }
        }

        // To consider the sum of the empty subarray
        // uncomment the following check:

        //if (maxi < 0) maxi = 0;

        return maxi;
    }

    public static void main(String args[]) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4};
        int n = arr.length;
        long maxSum = maxSubarraySum(arr, n);
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

## 🔹 Edge Cases  
* **All Negative Numbers:** Kadane's will correctly pick the single largest (least negative) number. If the problem allows an empty subarray, you might return 0.
* **Single Element Array:** Returns that element's value.
* **Large Positive/Negative numbers:** Use `long` for the sum variables to prevent overflow.

---

## 🔹 Important Notes / Takeaways  
* **Greedy Property:** Kadane's is a classic example of a greedy algorithm.
* **Variation:** If you need to **print** the subarray, you need to track the `start` and `end` indices whenever `maxi` is updated.
* **Follow-up:** "What if we must pick at least one element?" (Standard Kadane's handles this by initializing `maxi` to `Integer.MIN_VALUE`).

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^3)$ | $O(1)$ | 3 loops (i, j, k) |
| **Better** | $O(N^2)$ | $O(1)$ | 2 loops (i, j) |
| **Optimal** | $O(N)$ | $O(1)$ | **Kadane's (Single Pass)** |

---
5a

Kadani's algo extended verison - The extended version of Kadane's Algorithm not only calculates the maximum subarray sum but also tracks and returns the starting and ending indices to identify the actual elements that make up that maximum sum.

--- 
6a

# [Stock Buy And Sell](https://takeuforward.org/data-structure/stock-buy-and-sell?mode=track&sheet=a2z-dsa)

## 🔹 Problem Summary  
You are given an array of prices where `prices[i]` is the price of a given stock on an $i^{th}$ day. You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock. Return the maximum profit you can achieve. If you cannot achieve any profit, return 0.

---

## 🔹 Key Observations & Intuition  
* **Buy before Sell:** The core constraint is that the buying day must come before the selling day.
* **The "Lowest" Buy:** To maximize profit on any given day, you should have ideally bought the stock at the lowest price encountered *before* that day.
* **Greedy Approach:** By maintaining the `minPrice` seen so far, you can calculate the potential profit for the current day and compare it with the maximum profit found until now.

---

## 🔹 Approaches  

### 1. Brute Force  
**Idea:** Use nested loops to check every possible pair of buy and sell days. For each day `i`, calculate the profit with every day `j` (where `j > i`) and keep track of the maximum.

* **Time Complexity:** $O(N^2)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int maxProfit(int[] arr) {
    int maxPro = 0;
    for (int i = 0; i < arr.length; i++) {
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[j] > arr[i]) {
            maxPro = Math.max(arr[j] - arr[i], maxPro);
            }
        }
    }
    return maxPro;
    }
    public static void main(String[] args) {
    int arr[] = {7, 1, 5, 3, 6, 4};
    int maxPro = maxProfit(arr);
    System.out.println("Max profit is: " + maxPro);
    }
}
```

---

### 2. Optimal Approach  
**Detailed Explanation:** Linearly traverse the array while keeping track of the minimum price encountered so far (`minPrice`). For every element, calculate the difference between the current price and `minPrice`. Update the `maxPro` if this difference is greater than the existing `maxPro`.

**Why it is optimal:** It completes the task in a single pass ($O(N)$), making it significantly faster than the brute force approach for large datasets.

* **Time Complexity:** $O(N)$
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to calculate maximum profit using single pass
    public int stockbuySell(int[] prices) {
        // Initialize the minimum price to a large number
        int minPrice = Integer.MAX_VALUE;
        // Initialize the maximum profit to 0
        int maxProfit = 0;
        // Traverse each price in the array
        for (int price : prices) {
            // If current price is less than minPrice, update minPrice
            if (price < minPrice) {
                minPrice = price;
            } // Else calculate profit and update maxProfit if it's greater
            else {
                maxProfit = Math.max(maxProfit, price - minPrice);
            }
        } // Return the maximum profit found
        return maxProfit;
    }
}

// Driver code
class Main {
    public static void main(String[] args) {
        Solution obj = new Solution();
        int[] prices = {7, 1, 5, 3, 6, 4};

        System.out.println(obj.stockbuySell(prices));
    }
}
```

---

## 🔹 Edge Cases  
* **Prices in Descending Order:** (e.g., `[7, 6, 4, 3, 1]`) No profit can be made; the algorithm should return `0`.
* **Single Day Array:** Only one price means no transaction is possible; returns `0`.
* **Empty Array:** Handled by the loop structure, returns `0`.

---

## 🔹 Important Notes / Takeaways  
* **One-Pass Logic:** This problem is a classic example of how maintaining a "running state" (the minimum value) can eliminate the need for nested loops.
* **Difference between Part I and II:** Note that this problem allows only **one transaction**. If multiple transactions were allowed, the logic would shift to capturing every upward slope.

---

## 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Nested loops (Check all pairs) |
| **Optimal** | $O(N)$ | $O(1)$ | **Single pass (Track running minimum)** |

--- 

7q

# [Rearrange Array Elements by Sign](https://takeuforward.org/arrays/rearrange-array-elements-by-sign?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
You are given an array of size `N` containing an **equal number** of positive and negative integers. Your task is to rearrange the elements so that they alternate between positive and negative values, starting with a positive number. Crucially, you must maintain the **relative order** of the positive and negative elements as they appeared in the original array.

---

## 2. 🔹 Key Observations & Intuition  
* **Relative Order:** This means if `2` appeared before `1` in the original array, it must appear before `1` in the rearranged version.
* **Fixed Positions:** Since the array starts with a positive number and alternates, all **positive** numbers will end up at **even indices** (0, 2, 4...) and all **negative** numbers will end up at **odd indices** (1, 3, 5...).
* **Equal Distribution:** The problem guarantees an equal number of positive and negative elements, meaning every even/odd slot will be filled perfectly.

---

## 3. 🔹 Approaches  

### Brute Force  
* **Idea:** Segregate the positive and negative elements into two separate lists (`pos` and `neg`). Then, iterate through these lists and place elements back into the original array at their respective alternating indices.
* **Time Complexity:** $O(N + N/2)$ — $O(N)$ for traversing the array to segregate, and $O(N/2)$ for filling the array back.
* **Space Complexity:** $O(N/2 + N/2) = O(N)$ — Space required to store the separate positive and negative lists.

**Java Code:**
```java
import java.util.*;

class ArrayManipulator {
    // Method to rearrange elements so that positives and negatives alternate
    public int[] rearrangeBySign(int[] A, int n) {
        List<Integer> pos = new ArrayList<>();
        List<Integer> neg = new ArrayList<>();

        // Step 1: Separate positives and negatives
        for (int i = 0; i < n; i++) {
            if (A[i] > 0)
                pos.add(A[i]); // Add to positives
            else
                neg.add(A[i]); // Add to negatives
        }

        // Step 2: Place positives at even indices and negatives at odd indices
        for (int i = 0; i < n / 2; i++) {
            A[2 * i] = pos.get(i); // Even index → positive
            A[2 * i + 1] = neg.get(i); // Odd index → negative
        }

        return A;
    }

    public static void main(String[] args) {
        int[] A = {1, 2, -4, -5};
        int n = A.length;
        ArrayManipulator obj = new ArrayManipulator();
        int[] result = obj.rearrangeBySign(A, n);

        // Print the result
        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
```

---

### Optimal Approach  
* **Idea:** Instead of multiple passes and intermediate lists, use a single-pass traversal. Maintain two pointers: `posIndex` starting at 0 and `negIndex` starting at 1. As you traverse the original array, place positive numbers at `posIndex` and negative numbers at `negIndex`, incrementing each by 2 after placement.
* **Detailed Explanation:** We initialize a result array `ans` of the same size. We iterate through the input once. If an element is positive, it goes to `ans[posIndex]` and `posIndex` moves to the next even slot. If negative, it goes to `ans[negIndex]` and `negIndex` moves to the next odd slot.
* **Why it is optimal:** It reduces the number of traversals to exactly one ($O(N)$), making it more time-efficient than the brute force.
* **Complexity:**
    * **Time Complexity:** $O(N)$ — Single traversal of the input array.
    * **Space Complexity:** $O(N)$ — Extra space used to store the rearranged elements in the `ans` array.

**Java Code:**
```java
import java.util.*;

public class ArrayManipulator {
    // Function to rearrange elements by alternating sign
    public int[] rearrangeBySign(int[] A) {
        int n = A.length;

        // Result array initialized to size n
        int[] ans = new int[n];

        // posIndex for even indices (positive), negIndex for odd (negative)
        int posIndex = 0, negIndex = 1;

        // Traverse input array
        for (int i = 0; i < n; i++) {

            if (A[i] < 0) {
                // Place negative number at odd index
                ans[negIndex] = A[i];
                negIndex += 2;
            } else {
                // Place positive number at even index
                ans[posIndex] = A[i];
                posIndex += 2;
            }
        }

        return ans;
    }

    public static void main(String[] args) {
        int[] A = {1, 2, -4, -5};
        ArrayManipulator obj = new ArrayManipulator();
        int[] result = obj.rearrangeBySign(A);

        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 4. 🔹 Edge Cases  
* **Minimum Array Size:** Array of size 2 (one positive, one negative).
* **Sequential Elements:** All positives appearing before all negatives (e.g., `{1, 2, -3, -4}`). The pointers correctly distribute them to alternating slots.
* **Alternating Elements:** Array is already in the correct format (the algorithm still works correctly).

---

## 5. 🔹 Important Notes / Takeaways  
* **Two-Pointer Pattern:** Using indices to manage placement in a destination array is a common pattern for "rearrangement" problems.
* **In-place vs. Extra Space:** Note that while the time is optimal, we still use $O(N)$ extra space for the answer array because the relative order constraint makes in-place swapping extremely difficult without increasing time complexity to $O(N^2)$.
* **Interview Variation:** A common follow-up is "What if the number of positives and negatives is **not** equal?" (This requires a different logic where you append the leftovers at the end).

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N + N/2)$ | $O(N)$ | Uses intermediate `pos` and `neg` lists. |
| **Optimal** | $O(N)$ | $O(N)$ | **Single-pass** using two pointers. |

**Next Problem:** Would you like to proceed with the notes for **Next Permutation**?

---

8q

# [next_permutation : find next lexicographically greater permutation](https://takeuforward.org/data-structure/next_permutation-find-next-lexicographically-greater-permutation?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
Given an array of integers, rearrange its elements into the **lexicographically next greater permutation**. If such an arrangement is not possible (i.e., the array is sorted in descending order), the array must be rearranged into the lowest possible order (i.e., sorted in ascending order).

---

## 2. 🔹 Key Observations & Intuition  
* **Lexicographical Order:** Think of permutations like numbers. To find the next larger number, we need to find the rightmost digit that can be increased and then make the digits to its right as small as possible.
* **The Breakpoint:** A sequence that is strictly decreasing has no "next permutation." We look for the first index $i$ from the right where $arr[i] < arr[i+1]$. This is the "pivot" or "breakpoint" that needs to be swapped to create a larger sequence.
* **Minimal Increase:** To keep the increase minimal, we swap the pivot with the smallest element to its right that is still larger than the pivot.
* **Smallest Tail:** After the swap, the suffix to the right of the pivot is still in descending order. Reversing it turns it into ascending order, which is the smallest possible configuration for that suffix.

---

## 3. 🔹 Approaches  

### Brute Force  
* **Idea:** Find all possible permutations of the elements, sort them, and then search for the input permutation to find the one immediately after it.
* **Complexity:**
    * **Time Complexity:** $O(N! \cdot N)$ — Generating all permutations takes $N!$ time.
    * **Space Complexity:** $O(N!)$ — Storing all permutations.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the next permutation
    public List<Integer> nextPermutation(int[] nums) {
        // List to hold all permutations
        List<List<Integer>> all = new ArrayList<>();
        // Sort the input to start from the smallest
        Arrays.sort(nums);
        // Generate all permutations
        permute(nums, 0, all);
        // Convert array to list for comparison
        List<Integer> current = new ArrayList<>();
        for (int num : nums)
            current.add(num);
        // Find and return the next permutation
        for (int i = 0; i < all.size(); i++) {
            if (all.get(i).equals(current)) {
                if (i == all.size() - 1)
                    return all.get(0);
                return all.get(i + 1);
            }
        }
        return current;
    }

    // Backtracking permutation generator
    private void permute(int[] nums, int start, List<List<Integer>> all) {
        if (start == nums.length) {
            List<Integer> temp = new ArrayList<>();
            for (int num : nums) temp.add(num);
            all.add(new ArrayList<>(temp));
            return;
        }
        for (int i = start; i < nums.length; i++) {
            swap(nums, i, start);
            permute(nums, start + 1, all);
            swap(nums, i, start);
        }
    }

    // Swap helper
    private void swap(int[] arr, int i, int j) {
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {1, 2, 3};

        List<Integer> result = sol.nextPermutation(nums);
        for (int x : result)
            System.out.print(x + " ");
        System.out.println();
    }
}
```

---

### Optimal Approach  
* **Detailed Explanation:** 1.  **Find the break-point:** Traverse from the right and find the first index $i$ such that $arr[i] < arr[i+1]$.
    2.  **Find the successor:** If a break-point exists, traverse from the right again to find the first element larger than $arr[i]$ and swap them.
    3.  **Reverse the suffix:** Reverse the entire portion of the array to the right of the break-point index $i$.
    4.  **Edge Case:** If no break-point is found (array is descending), simply reverse the whole array.
* **Why it is optimal:** It only requires a few linear passes through the array without any extra data structures.
* **Complexity:**
    * **Time Complexity:** $O(3N) \approx O(N)$ — One pass for the breakpoint, one for the swap, and one for the reversal.
    * **Space Complexity:** $O(1)$ — In-place rearrangement.

**Java Code:**
```java
import java.util.*;

public class t u f {
    public static List< Integer > nextGreaterPermutation(List< Integer > A) {
        int n = A.size(); // size of the array.

        // Step 1: Find the break point:
        int ind = -1; // break point
        for (int i = n - 2; i >= 0; i--) {
            if (A.get(i) < A.get(i + 1)) {
                // index i is the break point
                ind = i;
                break;
            }
        }

        // If break point does not exist:
        if (ind == -1) {
            // reverse the whole array:
            Collections.reverse(A);
            return A;
        }

        // Step 2: Find the next greater element
        //         and swap it with ind:

        for (int i = n - 1; i > ind; i--) {
            if (A.get(i) > A.get(ind)) {
                int tmp = A.get(i);
                A.set(i, A.get(ind));
                A.set(ind, tmp);
                break;
            }
        }

        // Step 3: reverse the right half:
        List<Integer> sublist = A.subList(ind + 1, n);
        Collections.reverse(sublist);

        return A;
    }

    public static void main(String args[]) {
        List<Integer> A = Arrays.asList(new Integer[] {2, 1, 5, 4, 3, 0, 0});
        List<Integer> ans = nextGreaterPermutation(A);

        System.out.print("The next permutation is: [");
        for (int i = 0; i < ans.size(); i++) {
            System.out.print(ans.get(i) + " ");
        }
        System.out.println("]");
    }
}
```

---

## 4. 🔹 Edge Cases  
* **Last Permutation:** If the array is sorted in descending order (e.g., `[3, 2, 1]`), there is no larger permutation. The algorithm should return the smallest permutation (`[1, 2, 3]`).
* **Duplicates:** The algorithm handles duplicates correctly by looking for strictly greater/smaller conditions ($A[i] < A[i+1]$ and $A[i] > A[ind]$).
* **Single Element:** An array with one element is its own next permutation.

---

## 5. 🔹 Important Notes / Takeaways  
* **Visualizing the Peak:** Imagine the array elements as heights. A next permutation involves finding the last "upward" step and swapping it with a slightly larger "downward" element to its right.
* **STL Function:** In C++, this is a built-in function `next_permutation()`. In Java, we must implement the logic manually.
* **In-place:** The optimal solution is highly efficient because it modifies the input directly without allocating massive memory like the brute force approach.

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N! \cdot N)$ | $O(N!)$ | Impossible for $N > 12$. |
| **Optimal** | $O(N)$ | $O(1)$ | **Standard Interview Approach.** |

---

9q

# [Leaders in an Array](https://takeuforward.org/data-structure/leaders-in-an-array?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
Given an array, find all the **Leaders**. An element is considered a Leader if it is greater than all the elements to its right side. The rightmost element is always a leader.

---

## 2. 🔹 Key Observations & Intuition  
* **Right-Side Superiority:** An element $A[i]$ is a leader if $A[i] > \text{max}(A[i+1] \dots A[n-1])$.
* **Scanning Direction:** While a left-to-right scan requires checking all elements to the right for every single index ($O(N^2)$), a **right-to-left scan** allows us to keep track of the maximum value seen so far, reducing the work to a single pass ($O(N)$).
* **Relative Order:** If the problem requires the output in the same order as the original array, we must reverse our collected list since scanning from the right picks up leaders in reverse order.

---

## 3. 🔹 Approaches  

### Brute Force  
* **Idea:** Iterate through each element and use a nested loop to check if there is any element to its right that is greater than it. 
* **Time Complexity:** $O(N^2)$
* **Space Complexity:** $O(N)$ (to store the answer)

**Java Code:**
```java
import java.util.*;

class Solution {
  public static ArrayList<Integer> 
  printLeadersBruteForce(int[] arr, int n) {

    ArrayList<Integer> ans = new ArrayList<>();

    for (int i = 0; i < n; i++) {
      boolean leader = true;

      //Checking whether arr[i] is greater than all 
      //the elements in its right side
      for (int j = i + 1; j < n; j++)
        if (arr[j] > arr[i]) {

          // If any element found is greater than current leader
          // curr element is not the leader.
          leader = false;
          break;
        }

      // Push all the leaders in the ans array.
      if (leader)
        ans.add(arr[i]);

    }

    return ans;
  }

  public static void main(String[] args) {
    int n = 6;
    int arr[] = {10, 22, 12, 3, 0, 6};

    ArrayList<Integer> ans = printLeadersBruteForce(arr, n);

    for (int i = 0; i < ans.size(); i++) {
      System.out.print(ans.get(i) + " ");
    }

  }
}
```

---

### Optimal Approach  
* **Detailed Explanation:** 1. We start from the rightmost element because the rightmost element is always a leader.
    2. We maintain a `max` variable to keep track of the maximum element encountered from the right.
    3. We traverse the array from $n-2$ down to $0$. 
    4. If the current element is greater than the current `max`, it is a leader. We add it to our list and update `max`.
* **Why it is optimal:** It only traverses the array once, performing a constant-time comparison at each step.
* **Complexity:**
    * **Time Complexity:** $O(N)$
    * **Space Complexity:** $O(1)$ (ignoring the space for the result list)

**Java Code:**
```java
import java.util.*;

class Solution {
    public ArrayList<Integer> leaders(int[] nums) {
        ArrayList<Integer> ans = new ArrayList<>();
        int n = nums.length;

        // The last element is always a leader
        int max = nums[n - 1];
        ans.add(max);

        // Traverse the array from right to left
        for (int i = n - 2; i >= 0; i--) {
            if (nums[i] >= max) {
                ans.add(nums[i]);
                max = nums[i];
            }
        }

        // Reverse the list to maintain original order
        Collections.reverse(ans);
        return ans;
    }
}

class Main {
    public static void main(String[] args) {
        int[] nums = {10, 22, 12, 3, 0, 6};

        // Create an instance of the Solution class
        Solution finder = new Solution();

        // Get leaders using class method
        ArrayList<Integer> ans = finder.leaders(nums);

        System.out.print("Leaders in the array are: ");
        for (int leader : ans) {
            System.out.print(leader + " ");
        }
        System.out.println();
    }
}
```

---

## 4. 🔹 Edge Cases  
* **All elements are the same:** Every element will be considered a leader if using `>=`.
* **Strictly Increasing Array:** Only the last element will be a leader.
* **Strictly Decreasing Array:** All elements will be leaders.

---

## 5. 🔹 Important Notes / Takeaways  
* **Reverse the Result:** Don't forget to use `Collections.reverse()` if the output order must match the input array's relative order.
* **Scan from the End:** This is a common pattern for problems involving "elements to the right."

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(N)$ | Nested loops (Check right side) |
| **Optimal** | $O(N)$ | $O(1)$ | **Backward Scan (Running Max)** |

---

10q

# [Longest Consecutive Sequence in an Array](https://takeuforward.org/data-structure/longest-consecutive-sequence-in-an-array?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
Given an array of $n$ integers, find the length of the longest sequence of consecutive integers. The integers in this sequence can appear in any order in the original array. For example, in `[100, 4, 200, 1, 3, 2]`, the longest consecutive sequence is `[1, 2, 3, 4]`, so the output is `4`.

---

## 2. 🔹 Key Observations & Intuition  
* **Consecutive means $x, x+1, x+2...$:** We are looking for numbers that can form a continuous chain.
* **Order doesn't matter:** Since the sequence can be anywhere in the array, sorting is a natural first thought to bring consecutive numbers together.
* **Finding the Start:** The most efficient way to count a sequence is to identify its **starting element** (an element $x$ where $x-1$ is not present) and then count how many subsequent numbers ($x+1, x+2...$) exist.

---

## 3. 🔹 Approaches  

### Brute Force  
* **Idea:** For every number $x$ in the array, try to find $x+1, x+2, x+3...$ by searching through the array repeatedly using a linear search.
* **Time Complexity:** $O(N^2)$ — For every element, we potentially traverse the entire array.
* **Space Complexity:** $O(1)$ — No extra space used.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static boolean linearSearch(int[] a, int num) {
        int n = a.length; //size of array
        for (int i = 0; i < n; i++) {
            if (a[i] == num)
                return true;
        }
        return false;
    }
    public static int longestSuccessiveElements(int[] a) {
        int n = a.length; //size of array
        if (n == 0) return 0;

        int longest = 1;
        //pick a element and search for its
        //consecutive numbers:
        for (int i = 0; i < n; i++) {
            int x = a[i];
            int cnt = 1;
            //search for consecutive numbers
            //using linear search:
            while (linearSearch(a, x + 1) == true) {
                x += 1;
                cnt += 1;
            }

            longest = Math.max(longest, cnt);
        }
        return longest;
    }

    public static void main(String[] args) {
        int[] a = {100, 4, 200, 1, 3, 2};
        int ans = longestSuccessiveElements(a);
        System.out.println("The longest consecutive sequence is " + ans);
    }
}
```

---

### Better Approach  
* **Idea:** Sort the array first. After sorting, consecutive elements will be adjacent. We can then traverse the array once to find the length of the longest consecutive run, making sure to handle duplicate elements.
* **Improvements over brute:** Reduces the search time by organizing the data.
* **Complexity:**
    * **Time:** $O(N \log N) + O(N)$ — $O(N \log N)$ for sorting and $O(N)$ for a single pass.
    * **Space:** $O(1)$ or $O(N)$ depending on the sorting algorithm.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int longestSuccessiveElements(int[] a) {
        int n = a.length;
        if (n == 0) return 0;

        //sort the array:
        Arrays.sort(a);
        int lastSmaller = Integer.MIN_VALUE;
        int cnt = 0;
        int longest = 1;

        //find longest sequence:
        for (int i = 0; i < n; i++) {
            if (a[i] - 1 == lastSmaller) {
                //a[i] is the next element of the
                //current sequence.
                cnt += 1;
                lastSmaller = a[i];
            } else if (a[i] != lastSmaller) {
                cnt = 1;
                lastSmaller = a[i];
            }
            longest = Math.max(longest, cnt);
        }
        return longest;
    }

    public static void main(String[] args) {
        int[] a = {100, 4, 200, 1, 3, 2};
        int ans = longestSuccessiveElements(a);
        System.out.println("The longest consecutive sequence is " + ans);
    }
}
```

---

### Optimal Approach  
* **Detailed Explanation:** 1. Insert all array elements into a **HashSet** to achieve $O(1)$ lookups.
    2. Traverse the set. For each element `it`:
    3. Check if it is the **start of a sequence** by checking if `it - 1` exists in the set.
    4. If `it - 1` does **not** exist, `it` is a starting point. Start a loop to find how many consecutive elements (`it + 1, it + 2...`) exist in the set.
    5. Update the maximum length found so far.
* **Why it is optimal:** Each element is visited at most twice (once in the outer loop and once as part of a sequence count), leading to linear time complexity.
* **Complexity:**
    * **Time Complexity:** $O(N) + O(2N) \approx O(N)$ — Assuming Hash Map/Set operations are $O(1)$.
    * **Space Complexity:** $O(N)$ — To store elements in the HashSet.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int longestSuccessiveElements(int[] a) {
        int n = a.length;
        if (n == 0)
            return 0;

        int longest = 1;
        Set<Integer> set = new HashSet<>();

        // put all the array elements into set
        for (int i = 0; i < n; i++) {
            set.add(a[i]);
        }

        // Find the longest sequence
        for (int it : set) {
            // if 'it' is a starting number
            if (!set.contains(it - 1)) {
                // find consecutive numbers
                int cnt = 1;
                int x = it;
                while (set.contains(x + 1)) {
                    x = x + 1;
                    cnt = cnt + 1;
                }
                longest = Math.max(longest, cnt);
            }
        }
        return longest;
    }

    public static void main(String[] args) {
        int[] a = {100, 4, 200, 1, 3, 2};
        int ans = longestSuccessiveElements(a);
        System.out.println("The longest consecutive sequence is " + ans);
    }
}
```

---

## 4. 🔹 Edge Cases  
* **Empty Array:** Should return `0`.
* **Array with one element:** Should return `1`.
* **Array with all same elements:** Should return `1` (handled by Set or sorting check).
* **Array with strictly decreasing elements:** Handled correctly as the sequence length would be `1` for each.

---

## 5. 🔹 Important Notes / Takeaways  
* **The Set "Start" Trick:** The `!set.contains(it - 1)` check is the secret to bringing the complexity down to $O(N)$. It ensures we only start counting from the beginning of a sequence.
* **Duplicate Handling:** The Set naturally handles duplicates. In the Sorting approach, we must explicitly skip duplicates (`a[i] != lastSmaller`) to avoid resetting the count incorrectly.

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Performance |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Slowest |
| **Better (Sorting)** | $O(N \log N)$ | $O(1)$ / $O(N)$ | Good |
| **Optimal (Set)** | $O(N)$ | $O(N)$ | **Fastest (Single Pass)** |

---

11q

# [Set Matrix Zero](https://takeuforward.org/data-structure/set-matrix-zero?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
Given an $m \times n$ integer matrix, if an element is **0**, set its entire row and column to **0**. The modification should be done such that the final matrix reflects all necessary zeroing based on the *original* zeros present in the matrix.

---

## 2. 🔹 Key Observations & Intuition  
* **The Trap:** If you modify the matrix to 0 as you encounter them, you will create "new" zeros that will lead to incorrect row/column wipes in subsequent iterations.
* **Marking:** We need a way to "remember" which rows and columns should be zeroed without using the value `0` itself during the first pass.
* **Space Optimization:** We can move from using extra external space (arrays) to using the matrix's own first row and column as storage for these "markers."

---

## 3. 🔹 Approaches  

### Brute Force  
* **Idea:** Traverse the matrix. When a `0` is found, mark all non-zero elements in that row and column with a special value (like `-1`). In a second pass, convert all `-1` values to `0`.
* **Time Complexity:** $O(m \times n \times (m + n))$  
* **Space Complexity:** $O(1)$ (In-place modification)

**Java Code:**
```java
import java.util.*;
class Solution {
    // Function to set entire row and column to 0 if an element in the matrix is 0
    public void setZeroes ( int [][] matrix) {
        // Get number of rows
        int m = matrix.length;
        // Get number of columns
        int n = matrix[ 0 ].length;
        // First pass: mark rows and columns
        for ( int i = 0 ; i < m; i++) {
            for ( int j = 0 ; j < n; j++) {
                // If the cell is zero
                if (matrix[i][j] == 0 ) {
                    // Mark entire row as -1 (except zeros)
                    for ( int col = 0 ; col < n; col++) {
                        if (matrix[i][col] != 0 )
                            matrix[i][col] = - 1 ;
                    }
                    // Mark entire column as -1 (except zeros)
                    for ( int row = 0 ; row < m; row++) {
                        if (matrix[row][j] != 0 )
                            matrix[row][j] = - 1 ;
                    }
                }
            }
        }
        // Second pass: replace -1 with 0
        for ( int i = 0 ; i < m; i++) {
            for ( int j = 0 ; j < n; j++) {
                if (matrix[i][j] == - 1 )
                    matrix[i][j] = 0 ;
            }
        }
    }
}
public class Main {
    public static void main (String[] args) {
        // Example matrix
        int [][] matrix = {{ 1 , 1 , 1 },{ 1 , 0 , 1 },{ 1 , 1 , 1 }};
        // Create Solution object
        Solution sol = new Solution ();
        // Modify matrix
        sol.setZeroes(matrix);
        // Print result
        for ( int [] row : matrix) {
            for ( int val : row) {
                System.out.print(val + " " );
            }
            System.out.println();
        }
    }
}
```

---

### Better Approach  
* **Idea:** Use two separate prefix arrays: `row[m]` and `col[n]`. During the first traversal, if `matrix[i][j] == 0`, mark `row[i]` and `col[j]` as `true`. In the second pass, if either `row[i]` or `col[j]` is marked, set `matrix[i][j]` to `0`.
* **Improvements over brute:** Reduces the time complexity by avoiding redundant row/column scans for every zero found.
* **Complexity:** * **Time:** $O(m \times n)$
    * **Space:** $O(m + n)$

**Java Code:**
```java
import java.util.*;
class Solution {
    // Function to set entire row and column to 0 if an element in the matrix is 0
    public void setZeroes ( int [][] matrix) {
        // Get number of rows
        int m = matrix.length;
        // Get number of columns
        int n = matrix[ 0 ].length;
        // Create row marker array
        boolean [] row = new boolean [m];
        // Create column marker array
        boolean [] col = new boolean [n];
        // First pass: mark rows and columns that need to be zeroed
        for ( int i = 0 ; i < m; i++) {
            for ( int j = 0 ; j < n; j++) {
                // If element is zero, mark its row and column
                if (matrix[i][j] == 0 ) {
                    row[i] = true ;
                    col[j] = true ;
                }
            }
        }
        // Second pass: set cells to zero based on markers
        for ( int i = 0 ; i < m; i++) {
            for ( int j = 0 ; j < n; j++) {
                // If the row or column is marked, set cell to zero
                if (row[i] || col[j]) {
                    matrix[i][j] = 0 ;
                }
            }
        }
    }
}
public class Main {
    public static void main (String[] args) {
        // Create the matrix
        int [][] matrix = {{ 1 , 1 , 1 },{ 1 , 0 , 1 },{ 1 , 1 , 1 }};
        // Create Solution object
        Solution obj = new Solution ();
        // Call function
        obj.setZeroes(matrix);
        // Print the updated matrix
        for ( int [] row : matrix) {
            for ( int val : row) {
                System.out.print(val + " " );
            }
            System.out.println();
        }
    }
}
```

---

### Optimal Approach  
* **Detailed Explanation:** Use the first row and first column of the matrix itself as the marker arrays. Since the very first cell `matrix[0][0]` overlaps for both, use an extra variable `col0` to track the first column status. 
    1.  Determine if the first row/column should be zeroed.
    2.  Use `matrix[i][0]` and `matrix[0][j]` to store markers for the rest of the matrix.
    3.  Iterate backwards (from `m-1` to `0`) to update the matrix based on these markers to avoid overwriting them prematurely.
* **Why it is optimal:** It achieves the best possible time complexity while using absolutely no extra auxiliary space ($O(1)$).
* **Complexity:** * **Time:** $O(m \times n)$
    * **Space:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    static void setZeroes(int[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;

        // int[] row = new int[n]; --> matrix[..][0]
        // int[] col = new int[m]; --> matrix[0][..]

        int col0 = 1;
        // step 1: Traverse the matrix and
        // mark 1st row & col accordingly:
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (matrix[i][j] == 0) {
                    // mark i-th row:
                    matrix[i][0] = 0;

                    // mark j-th column:
                    if (j != 0)
                        matrix[0][j] = 0;
                    else
                        col0 = 0;
                }
            }
        }

        // Step 2: Mark with 0 from (1,1) to (n-1, m-1):
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (matrix[i][j] != 0) {
                    // check for col & row:
                    if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                        matrix[i][j] = 0;
                    }
                }
            }
        }

        //step 3: Finally mark the 1st col & then 1st row:
        if (matrix[0][0] == 0) {
            for (int j = 0; j < m; j++) {
                matrix[0][j] = 0;
            }
        }
        if (col0 == 0) {
            for (int i = 0; i < n; i++) {
                matrix[i][0] = 0;
            }
        }

    }

    public static void main(String[] args) {
        int[][] matrix = {{1, 1, 1}, {1, 0, 1}, {1, 1, 1}};
        int n = matrix.length;
        int m = matrix[0].length;
        setZeroes(matrix);
        System.out.println("The Final Matrix is ");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

---

## 4. 🔹 Edge Cases  
* **Matrix with no zeros:** Should remain unchanged.
* **Matrix with all zeros:** Entire matrix becomes zeros.
* **First row or first column containing zeros:** Specifically handled in the Optimal Approach using `col0` and the first row/column logic.
* **1x1 Matrix:** Correctly handled by all approaches.

---

## 5. 🔹 Important Notes / Takeaways  
* **In-Place vs. Auxiliary Space:** Interviews often push for the $O(1)$ space solution. Reusing the input structure is a top-tier optimization technique.
* **Pass Order:** In the Optimal approach, the order of zeroing matters (processing the inner matrix before the marker row/column) to prevent the "zero-out" effect from propagating incorrectly.

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(m \times n \times (m + n))$ | $O(1)$ | Mark with special value (`-1`) |
| **Better** | $O(m \times n)$ | $O(m + n)$ | Extra arrays for row/col status |
| **Optimal** | $O(m \times n)$ | $O(1)$ | Use first row/col as markers |

---
12q

# [Rotate Image by 90 degree](https://takeuforward.org/data-structure/rotate-image-by-90-degree?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary
Given an $N \times N$ 2D integer matrix, rotate the matrix by **90 degrees clockwise**. The rotation must be done **in-place**, meaning the input matrix must be modified directly without using a second matrix.

---

## 2. 🔹 Key Observations & Intuition
* **Row-to-Column Mapping:** In a 90-degree clockwise rotation, the first row becomes the last column, the second row becomes the second-to-last column, and so on.
* **Mathematical Transformation:** For an element at `matrix[i][j]`, its new position after rotation is `matrix[j][n - 1 - i]`.
* **In-Place Strategy:** To avoid $O(N^2)$ extra space, notice that rotating is equivalent to performing a **Transpose** (turning rows into columns) followed by **Reversing** each row.

---

## 3. 🔹 Approaches

### Brute Force Approach
* **Idea:** Create a dummy $N \times N$ matrix. Iterate through the original matrix and place each element `matrix[i][j]` at its rotated position `dummy[j][n - 1 - i]`. Finally, copy the dummy matrix back to the original.
* **Time Complexity:** $O(N^2)$
* **Space Complexity:** $O(N^2)$ (due to the extra dummy matrix).

**Java Code:**
```java
import java.util.*;
class TUF {
    static int[][] rotate(int[][] matrix) {
        int n = matrix.length;
        int rotated[][] = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                rotated[j][n - i - 1] = matrix[i][j];
            }
        }
        return rotated;
    }

    public static void main(String args[]) {
        int arr[][] =  {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        int rotated[][] = rotate(arr);
        System.out.println("Rotated Image");
        for (int i = 0; i < rotated.length; i++) {
            for (int j = 0; j < rotated.length; j++) {
                System.out.print(rotated[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

---

### Optimal Approach
* **Detailed Explanation:** This approach achieves the rotation in-place in two steps:
    1. **Transpose the Matrix:** Swap `matrix[i][j]` with `matrix[j][i]`. This turns rows into columns but in an anti-clockwise sense.
    2. **Reverse Each Row:** Reverse the elements in every row. This results in the final 90-degree clockwise rotation.
* **Why it is optimal:** It modifies the matrix in-place, reducing space complexity to $O(1)$ while maintaining $O(N^2)$ time complexity.
* **Complexity:**
    * **Time Complexity:** $O(N^2)$ (for Transpose) + $O(N^2)$ (for Reversing) $\approx O(N^2)$
    * **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;
class TUF {
    static void rotate(int[][] matrix) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = i; j < matrix[0].length; j++) {
                int temp = 0;
                temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix.length / 2; j++) {
                int temp = 0;
                temp = matrix[i][j];
                matrix[i][j] = matrix[i][matrix.length - 1 - j];
                matrix[i][matrix.length - 1 - j] = temp;
            }
        }
    }

    public static void main(String args[]) {
        int arr[][] =  {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
        rotate(arr);
        System.out.println("Rotated Image");
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr.length; j++) {
                System.out.print(arr[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

---

## 4. 🔹 Edge Cases
* **$1 \times 1$ Matrix:** A single element matrix remains unchanged after rotation.
* **Empty Matrix:** If $N=0$, the function should return or handle it gracefully.
* **Rectangular Matrix:** The problem specifies $N \times N$, but if it were $M \times N$, an in-place rotation would be much more complex.

---

## 5. 🔹 Important Notes / Takeaways
* **Transpose + Reverse:** This is the standard "trick" for 90-degree clockwise rotation. If asked for **Anti-Clockwise**, you would Transpose and then **Reverse Each Column** (or reverse rows then transpose).
* **Two-Pass Optimization:** Even though it's two passes (Transpose then Reverse), it's still $O(N^2)$, which is the theoretical minimum since every element must be moved.
* **Interview Insight:** Mentioning the Transpose property shows a deep understanding of matrix properties.

---

## 6. 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(N^2)$ | Use extra dummy matrix. |
| **Optimal** | $O(N^2)$ | $O(1)$ | **Transpose** then **Reverse Rows**. |
---
13q

# [Spiral Traversal of Matrix](https://takeuforward.org/data-structure/spiral-traversal-of-matrix?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
Given an $m \times n$ 2D matrix, return all elements of the matrix in **spiral order**. The traversal starts from the top-left corner and moves in a clockwise direction (Right $\to$ Down $\to$ Left $\to$ Up) until all elements are visited.

---

## 2. 🔹 Key Observations & Intuition  
* **Boundary Management:** The spiral consists of layers. We need to maintain four boundaries: `top`, `bottom`, `left`, and `right`.
* **The Cycle:** A single "loop" of the spiral involves:
    1. Moving **left to right** along the `top` row.
    2. Moving **top to bottom** along the `right` column.
    3. Moving **right to left** along the `bottom` row (if it still exists).
    4. Moving **bottom to top** along the `left` column (if it still exists).
* **Shrinking the Box:** After each directional move, we increment or decrement the corresponding boundary to "shrink" the available matrix area.

---

## 3. 🔹 Approaches  

### Optimal Approach (Boundary Simulation)
* **Detailed Explanation:** 1. Initialize `top = 0`, `left = 0`, `bottom = n-1`, `right = m-1`.
    2. Loop while `top <= bottom` and `left <= right`.
    3. **Right:** Traverse from `left` to `right` on `top` row. Increment `top`.
    4. **Down:** Traverse from `top` to `bottom` on `right` column. Decrement `right`.
    5. **Left:** (Check `top <= bottom`) Traverse from `right` to `left` on `bottom` row. Decrement `bottom`.
    6. **Up:** (Check `left <= right`) Traverse from `bottom` to `top` on `left` column. Increment `left`.
* **Why it is optimal:** It visits every element exactly once with $O(1)$ auxiliary space (excluding the result list).
* **Complexity:**
    * **Time Complexity:** $O(n \times m)$ — Every element is visited once.
    * **Space Complexity:** $O(1)$ — No extra data structures used other than the output list.

**Java Code:**
```java
import java.util.*;

public class Main {
    public static List<Integer> printSpiral(int[][] mat) {
        // Define ans list to store the result.
        List<Integer> ans = new ArrayList<Integer>();

        int n = mat.length; // no. of rows
        int m = mat[0].length; // no. of columns

        // Initialize the pointers req. for traversal.
        int top = 0, left = 0, bottom = n - 1, right = m - 1;

        // Loop until all elements are not traversed.
        while (top <= bottom && left <= right) {

            // For moving left to right
            for (int i = left; i <= right; i++)
                ans.add(mat[top][i]);

            top++;

            // For moving top to bottom
            for (int i = top; i <= bottom; i++)
                ans.add(mat[i][right]);

            right--;

            // For moving right to left.
            if (top <= bottom) {
                for (int i = right; i >= left; i--)
                    ans.add(mat[bottom][i]);

                bottom--;
            }

            // For moving bottom to top.
            if (left <= right) {
                for (int i = bottom; i >= top; i--)
                    ans.add(mat[i][left]);

                left++;
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        // Matrix initialization.
        int[][] mat = {{1, 2, 3, 4},
                       {5, 6, 7, 8},
                       {9, 10, 11, 12},
                       {13, 14, 15, 16}};

        List<Integer> ans = printSpiral(mat);

        for (int i = 0; i < ans.size(); i++) {
            System.out.print(ans.get(i) + " ");
        }

        System.out.println();
    }
}
```

---

## 4. 🔹 Edge Cases  
* **Single Row Matrix:** `[[1, 2, 3]]` → The "down", "left", and "up" loops should not execute or should be handled by condition checks.
* **Single Column Matrix:** `[[1], [2], [3]]` → Handled by boundary conditions.
* **Empty Matrix:** Should return an empty list.
* **Redundant Checks:** The `if (top <= bottom)` and `if (left <= right)` checks inside the loop are **critical** for non-square matrices to prevent printing the same row/column twice.

---

## 5. 🔹 Important Notes / Takeaways  
* **Clockwise Logic:** Always maintain the order: Right $\to$ Down $\to$ Left $\to$ Up.
* **Square vs. Rectangular:** This algorithm works perfectly for both, provided the internal checks are present.
* **Standard Pattern:** Boundary-based simulation is the most common and accepted way to solve matrix traversal problems in interviews.

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Optimal** | $O(N \times M)$ | $O(1)$ | **Boundary Simulation** |

---

14q 
# [Count Subarrays with Given Sum](https://takeuforward.org/arrays/count-subarray-sum-equals-k?mode=track&sheet=a2z-dsa)

## 1. 🔹 Problem Summary  
Given an array of integers `arr[]` and an integer `k`, return the total number of **contiguous subarrays** whose sum equals `k`. A subarray is a sequence of elements within an array that are adjacent to each other.

---

## 2. 🔹 Key Observations & Intuition  
* **Contiguous Nature:** Since we need contiguous subarrays, we can think in terms of prefix sums.
* **Prefix Sum Logic:** If the sum of elements from index $0$ to $i$ is $S_i$, and the sum from $0$ to $j$ ($j < i$) is $S_j$, then the sum of the subarray between $j+1$ and $i$ is $S_i - S_j$.
* **The Equation:** We want $S_i - S_j = k$. This can be rewritten as **$S_j = S_i - k$**. 
* **Hashing for Speed:** If we store the frequency of all prefix sums encountered so far in a Map, we can instantly check how many times the value ($S_i - k$) has occurred before.

---

## 3. 🔹 Approaches  

### Brute Force  
* **Idea:** Generate all possible subarrays using two nested loops and calculate the sum of each subarray using a third loop.
* **Time Complexity:** $O(N^3)$  
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int findAllSubarraysWithGivenSum(int arr[], int k) {
        int n = arr.length; // size of the given array.
        int cnt = 0; // count

        for (int i = 0; i < n; i++) { // starting index i
            for (int j = i; j < n; j++) { // ending index j

                // calculate the sum of subarray [i...j]
                int sum = 0;
                for (int K = i; K <= j; K++)
                    sum += arr[K];

                // Increase the count if sum == k:
                if (sum == k)
                    cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 4};
        int k = 6;
        int cnt = findAllSubarraysWithGivenSum(arr, k);
        System.out.println("The number of subarrays is: " + cnt);
    }
}
```

---

### Better Approach  
* **Idea:** Optimize the brute force by removing the third loop. We can calculate the sum of the current subarray on the fly while moving the end index `j`.
* **Improvements over brute:** Reduces time complexity from $O(N^3)$ to $O(N^2)$.
* **Complexity:**
    * **Time Complexity:** $O(N^2)$
    * **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int findAllSubarraysWithGivenSum(int arr[], int k) {
        int n = arr.length; // size of the given array.
        int cnt = 0; // count

        for (int i = 0; i < n; i++) { // starting index i
            int sum = 0;
            for (int j = i; j < n; j++) { // ending index j
                // calculate the sum of subarray [i...j]
                // sum of [i..j-1] + arr[j]
                sum += arr[j];

                // Increase the count if sum == k:
                if (sum == k)
                    cnt++;
            }
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 4};
        int k = 6;
        int cnt = findAllSubarraysWithGivenSum(arr, k);
        System.out.println("The number of subarrays is: " + cnt);
    }
}
```

---

### Optimal Approach  
* **Detailed Explanation:** 1. Use a HashMap to store the prefix sums encountered so far and their frequencies: `Map<PrefixSum, Frequency>`.
    2. Initialize `preSum = 0` and `cnt = 0`.
    3. Add `{0: 1}` to the map to handle cases where a subarray starting from index 0 itself equals `k`.
    4. Traverse the array, adding each element to `preSum`.
    5. Calculate `remove = preSum - k`.
    6. If `remove` exists in the map, add its frequency to `cnt`.
    7. Update the map with the current `preSum`.
* **Why it is optimal:** It solves the problem in a single pass using the prefix sum property combined with a Hash Map for $O(1)$ lookups.
* **Complexity:**
    * **Time Complexity:** $O(N)$ (or $O(N \log N)$ depending on the map implementation).
    * **Space Complexity:** $O(N)$ (to store the prefix sums in the map).

**Java Code:**
```java
import java.util.*;

public class Main {
    public static int findAllSubarraysWithGivenSum(int arr[], int k) {
        int n = arr.length; // size of the given array.
        Map<Integer, Integer> mpp = new HashMap<>();
        int preSum = 0, cnt = 0;

        mpp.put(0, 1); // Setting 0 in the map.
        for (int i = 0; i < n; i++) {
            // add current element to prefix Sum:
            preSum += arr[i];

            // Calculate x-k:
            int remove = preSum - k;

            // Add the number of subarrays to be removed:
            cnt += mpp.getOrDefault(remove, 0);

            // Update the count of prefix sum
            // in the map.
            mpp.put(preSum, mpp.getOrDefault(preSum, 0) + 1);
        }
        return cnt;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 2, 4};
        int k = 6;
        int cnt = findAllSubarraysWithGivenSum(arr, k);
        System.out.println("The number of subarrays is: " + cnt);
    }
}
```

---

## 4. 🔹 Edge Cases  
* **k = 0:** The algorithm correctly handles cases where subarrays sum to zero (common with negative numbers).
* **All Negative Numbers:** The prefix sum logic still holds true.
* **Array with only one element:** If `arr[0] == k`, the map initialization `mpp.put(0, 1)` ensures it is counted.
* **No Subarray found:** Returns 0 correctly.

---

## 5. 🔹 Important Notes / Takeaways  
* **Hashing + Prefix Sum:** This is a very common pattern for subarray problems. If the problem involves "Sum equals K", think of this approach.
* **Difference from Two Pointers:** You cannot use the Two Pointers / Sliding Window approach here if the array contains **negative numbers**, because the sum doesn't increase monotonically. Hashing is the robust solution.
* **Initialization:** Never forget to put `(0, 1)` in your map initially.

---

## 6. 🔹 Complexity Summary Table  

| Approach | Time Complexity | Space Complexity | Strategy |
| :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^3)$ | $O(1)$ | Three nested loops |
| **Better** | $O(N^2)$ | $O(1)$ | Two nested loops |
| **Optimal** | $O(N)$ | $O(N)$ | **Prefix Sum + HashMap** |
---
...
# Hard Problems 
1a