# Arrays - Striver's A2Z DSA Sheet Notes

> Notes generated from [Striver's A2Z DSA Sheet](https://takeuforward.org/strivers-a2z-dsa-course/strivers-a2z-dsa-course-sheet-2)


# ═══════════════════════════════════════
# Easy Problems
# ═══════════════════════════════════════

---
Q1
# Find the Largest element in an array

## 🔹 Problem Summary
Problem Statement: Given an array, we have to find the largest element in the array.

**Examples:**
Examples
Example 1:
Input:
 arr[] = {2, 5, 1, 3, 0}  

Output:
 5  

Explanation:
  
5 is the largest element in the array.


Example 2:
Input:
 arr[] = {8, 10, 5, 7, 9}  

Output:
 10  

Explanation:
  
10 is the largest element in the array.

---

## 🔹 Key Observations & Intuition
* Create a variable called max and initialize it with the value of the first element in the array.
* Use a for loop to iterate through the rest of the elements in the array.
* In each iteration, compare the current element with the max variable.
* If the current element is greater than the max value, update the max value with the current element's value.
* After completing the loop, print the max variable, which will hold the largest value in the array.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Sort the array in ascending order.
Print the element at the (size of the array - 1)th index, which corresponds to the largest element in the array.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.Arrays;

class Solution {

    // Function to sort the array and return the largest element
    public static int sortArr(int[] arr) {
        // Sort the array in ascending order
        Arrays.sort(arr);
        
        // Return the last element (largest element) after sorting
        return arr[arr.length - 1];
    }
}

public class Main {

    public static void main(String[] args) {
        // Initialize arrays
        int[] arr1 = {2, 5, 1, 3, 0};
        int[] arr2 = {8, 10, 5, 7, 9};
        
        // Find and output the largest element in both arrays
        System.out.println("The Largest element in the array is: " + Solution.sortArr(arr1));
        System.out.println("The Largest element in the array is: " + Solution.sortArr(arr2));
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Create a variable called max and initialize it with the value of the first element in the array.
Use a for loop to iterate through the rest of the elements in the array.
In each iteration, compare the current element with the max variable.
If the current element is greater than the max value, update the max value with the current element's value.
After completing the loop, print the max variable, which will hold the largest value in the array.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
class Solution {

    // Function to find the largest element in the array
    public static int findLargestElement(int[] arr, int n) {
        int max = arr[0];  // Initialize max with the first element in the array

        // Iterate through the array to find the maximum element
        for (int i = 1; i < n; i++) {
            if (arr[i] > max) {  // If the current element is greater than max, update max
                max = arr[i];
            }
        }

        return max;  // Return the largest element found
    }
}

public class Main {

    public static void main(String[] args) {
        // Array 1
        int[] arr1 = {2, 5, 1, 3, 0};
        int n = arr1.length;  // Size of the array
        int max = Solution.findLargestElement(arr1, n);  // Call the function to find the largest element
        System.out.println("The largest element in the array is: " + max);  // Output the result

        // Array 2
        int[] arr2 = {8, 10, 5, 7, 9};
        n = arr2.length;  // Size of the array
        max = Solution.findLargestElement(arr2, n);  // Call the function to find the largest element
        System.out.println("The largest element in the array is: " + max);  // Output the result
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q2
# Find Second Smallest and Second Largest Element in an array

## 🔹 Problem Summary
Problem Statement: Given an array, find the second smallest and second largest element in the array. Print ‘-1’ in the event that either of them doesn’t exist.

**Examples:**
Examples
Example 1:
Input:
 [1, 2, 4, 7, 7, 5]  

Output:
  
Second Smallest : 2  
Second Largest : 5  

Explanation:
  The elements are sorted as 1, 2, 4, 5, 7, 7.  
Hence, the second smallest element is 2, and the second largest element is 5.


Example 2:
Input:
 [1]  

Output:
  
Second Smallest : -1  
Second Largest : -1  

Explanation:
  Since there is only one element in the array, it is both the largest and smallest element.  
Therefore, there is no second smallest or second largest element present.

---

## 🔹 Key Observations & Intuition
* We will need four variables: small, second_small, large, and second_large. Initialize small and second_small to INT_MAX, and large and second_large to INT_MIN.
* Second Smallest Algorithm:
* If the current element is smaller than 'small', update the values of second_small and small.
* Else if the current element is smaller than 'second_small', update the value of second_small.
* After traversing the array, the second smallest element will be stored in the variable second_small.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Sort the array in ascending order.
The element at the second index (index 1) is the second smallest element.
The element at the second index from the end (index length-2) is the second largest element.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.Arrays;

class Solution {

    // Method to find the second smallest and second largest elements in the array
    public static void getElements(int[] arr, int n) {
        
        // Edge case: when the array has less than 2 elements
        if (n == 0 || n == 1) {
            System.out.println(-1 + " " + -1);  // Print -1 for both second smallest and second largest
            return;
        }

        // Sort the array to easily find the second smallest and second largest elements
        Arrays.sort(arr);

        // Second smallest element is at index 1 after sorting
        int small = arr[1];

        // Second largest element is at index n-2 after sorting
        int large = arr[n - 2];

        // Output the second smallest and second largest elements
        System.out.println("Second smallest is " + small);
        System.out.println("Second largest is " + large);
    }
}

public class Main {

    public static void main(String[] args) {
        
        // Initialize the array with elements
        int[] arr = {1, 2, 4, 6, 7, 5};
        
        // Calculate the size of the array
        int n = arr.length;
        
        // Call the method to find and print the second smallest and second largest elements
        Solution.getElements(arr, n);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Perform a single traversal to find the smallest and largest elements in the array.
After that, traverse the array again to find the element just greater than the smallest element (this will be the second smallest).
Similarly, find the element just smaller than the largest element (this will be the second largest).

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

// Class to solve the problem of finding the second smallest and second largest elements
class Solution {

    // Method to find the second smallest and second largest elements in the array
    public static void getElements(int[] arr, int n) {

        // Edge case: when the array has less than 2 elements
        if (n == 0 || n == 1) {
            System.out.println(-1 + " " + -1);  // Print -1 for both second smallest and second largest
            return;
        }

        // Initialize variables to track the smallest, second smallest, largest, and second largest elements
        int small = Integer.MAX_VALUE, second_small = Integer.MAX_VALUE;
        int large = Integer.MIN_VALUE, second_large = Integer.MIN_VALUE;

        // Find the smallest and largest elements in the array
        for (int i = 0; i < n; i++) {
            small = Math.min(small, arr[i]);  // Update the smallest element
            large = Math.max(large, arr[i]);  // Update the largest element
        }

        // Find the second smallest and second largest elements
        for (int i = 0; i < n; i++) {
            if (arr[i] < second_small && arr[i] != small) {
                second_small = arr[i];  // Update second smallest if a smaller element is found
            }
            if (arr[i] > second_large && arr[i] != large) {
                second_large = arr[i];  // Update second largest if a larger element is found
            }
        }

        // Output the second smallest and second largest elements
        System.out.println("Second smallest is " + second_small);
        System.out.println("Second largest is " + second_large);
    }
}

public class Main {

    public static void main(String[] args) {

        // Driver code
        int n = 6;
        int[] arr = {1, 2, 4, 6, 7, 5};  // Array of elements

        // Call the function to find and print the second smallest and second largest elements
        Solution.getElements(arr, n);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
We will need four variables: small, second_small, large, and second_large. Initialize small and second_small to INT_MAX, and large and second_large to INT_MIN.
Second Smallest Algorithm:
If the current element is smaller than 'small', update the values of second_small and small.
Else if the current element is smaller than 'second_small', update the value of second_small.
After traversing the array, the second smallest element will be stored in the variable second_small.
Second Largest Algorithm:
If the current element is larger than 'large', update the values of second_large and large.
Else if the current element is larger than 'second_large', update the value of second_large.
After traversing the array, the second largest element will be stored in the variable second_large.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {

    // Function to find the second smallest element in the array
    public static int secondSmallest(int[] arr, int n) {
        // Edge case: if the array has fewer than 2 elements
        if (n < 2)
            return -1;

        int small = Integer.MAX_VALUE;
        int second_small = Integer.MAX_VALUE;

        // Loop through the array to find the second smallest element
        for (int i = 0; i < n; i++) {
            // Update the smallest and second smallest values
            if (arr[i] < small) {
                second_small = small;
                small = arr[i];
            } 
            else if (arr[i] < second_small && arr[i] != small) {
                second_small = arr[i];
            }
        }
        return second_small; // Return the second smallest element
    }

    // Function to find the second largest element in the array
    public static int secondLargest(int[] arr, int n) {
        // Edge case: if the array has fewer than 2 elements
        if (n < 2)
            return -1;

        int large = Integer.MIN_VALUE, second_large = Integer.MIN_VALUE;

        // Loop through the array to find the second largest element
        for (int i = 0; i < n; i++) {
            // Update the largest and second largest values
            if (arr[i] > large) {
                second_large = large;
                large = arr[i];
            } 
            else if (arr[i] > second_large && arr[i] != large) {
                second_large = arr[i];
            }
        }
        return second_large; // Return the second largest element
    }
}

public class Main {

    public static void main(String[] args) {
        // Array of elements
        int[] arr = {1, 2, 4, 7, 7, 5};

        // Calculate the size of the array
        int n = arr.length;

        // Find the second smallest and second largest elements
        int sS = Solution.secondSmallest(arr, n);
        int sL = Solution.secondLargest(arr, n);

        // Output the results
        System.out.println("Second smallest is " + sS);
        System.out.println("Second largest is " + sL);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q3
# Check if an Array is Sorted

## 🔹 Problem Summary
Problem Statement: Given an array of size n, write a program to check if the given array is sorted in (ascending / Increasing / Non-decreasing) order or not. If the array is sorted then return True, Else return False.

**Examples:**
Examples
Example 1:
Input: N = 5, array[] = {1,2,3,4,5}
Output: True.
Explanation: The given array is sorted i.e Every element in the array is smaller than or equals to its next values, So the answer is True.

Example 2:
Input: N = 5, array[] = {5,4,6,7,8}
Output: False.
Explanation: The given array is Not sorted i.e Every element in the array is not smaller than or equal to its next values, So the answer is False.
Here element 5 is not smaller than or equal to its future elements.

---

## 🔹 Key Observations & Intuition
* As we know that for a sorted array the previous of every element is smaller than or equal to its current element.
* So, Through this, we can conclude that if the previous element is smaller than or equal to the current element then. Then we can say that the two elements are sorted. If the condition is true for the entire array then the array is sorted.
* We will check every element with its previous element if the previous element is smaller than or equal to the current element then we will move to the next index.
* If the whole array is traversed successfully or the size of the given array is zero or one (i.e N = 0 or N = 1). Then we will return True else return False.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
The idea is pretty simple here, We will start with the element at the 0th index, and will compare it with all of its future elements that are present in the array.
If the picked element is smaller than or equal to all of its future values then we will move to the next Index/element until the whole array is traversed.
If any of the picked elements is greater than its future elements, Then simply we will return False.
If the size of the array is Zero or One i.e ( N = 0 or N = 1 ) or the entire array is traversed successfully then we will simply return True.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
As we know that for a sorted array the previous of every element is smaller than or equal to its current element.
So, Through this, we can conclude that if the previous element is smaller than or equal to the current element then. Then we can say that the two elements are sorted. If the condition is true for the entire array then the array is sorted.
We will check every element with its previous element if the previous element is smaller than or equal to the current element then we will move to the next index.
If the whole array is traversed successfully or the size of the given array is zero or one (i.e N = 0 or N = 1). Then we will return True else return False.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
class Solution {
    // Function to check if the array is sorted
    public boolean isSorted(int[] arr, int n) {
        for (int i = 1; i < n; i++) {
            if (arr[i] < arr[i - 1])  // If any element is smaller than the previous one, return false
                return false;
        }
        return true;  // Return true if the array is sorted
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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q4
# Remove Duplicates in-place from Sorted Array

## 🔹 Problem Summary
Problem Statement: Given an integer array sorted in non-decreasing order, remove the duplicates in place such that each unique element appears only once. The relative order of the elements should be kept the same.

If there are k elements after removing the duplicates, then the first k elements of the array should hold the final result. It does not matter what you leave beyond the first k elements.

**Examples:**
Examples
Input: arr[]=[1,1,2,2,2,3,3]
Output: [1,2,3,_,_,_,_]
Explanation: Total number of unique elements are 3, i.e[1,2,3] and Therefore return 3 after assigning [1,2,3] in the beginning of the array.

Input: arr[]=[1,1,1,2,2,3,3,3,3,4,4]
Output: [1,2,3,4,_,_,_,_,_,_,_]
Explanation: Total number of unique elements are 4, i.e[1,2,3,4] and Therefore return 4 after assigning [1,2,3,4] in the beginning of the array.

---

## 🔹 Key Observations & Intuition
* Instead of using a set to store the unique elements, we can implement a two pointer strategy to optimize the space. Since the array is sorted, we know that all the duplicate values will be adjacent to each other.
* Begin at the first position, which will always be part of the final unique list.
* Move through the list one item at a time, comparing the current item with the most recently kept unique item.
* If the current item is the same as the last kept one, skip it because it’s a duplicate.
* If it’s different, place it right after the last kept unique item to keep all unique values grouped at the front.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
Since we need to store only unique elements, we can use the set data structure. We can insert all the elements of the array in the set irrespective of their frequency as set only allows one occurence of each element.
Declare a set and insert all the elements of the array into the set.
The number of unique elements in array is equal to size of the set.
Traverse the set and fill the first k indices with elements in set.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

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
        int[] nums = {0,0,1,1,1,2,2,3,3,4};

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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Instead of using a set to store the unique elements, we can implement a two pointer strategy to optimize the space. Since the array is sorted, we know that all the duplicate values will be adjacent to each other.
Begin at the first position, which will always be part of the final unique list.
Move through the list one item at a time, comparing the current item with the most recently kept unique item.
If the current item is the same as the last kept one, skip it because it’s a duplicate.
If it’s different, place it right after the last kept unique item to keep all unique values grouped at the front.
Continue until every element in the list has been checked. The first part of the list now contains all the unique values in their original order, and the rest can be ignored.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

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
        int[] nums = {0,0,1,1,1,2,2,3,3,4};

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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q5
# Left Rotate the Array by One

## 🔹 Problem Summary
Problem Statement: Given an integer array nums, rotate the array to the left by one.

Note: There is no need to return anything, just modify the given array.

**Examples:**
Examples
Example 1:
Input:
 nums = [1, 2, 3, 4, 5]  

Output:
 [2, 3, 4, 5, 1]  

Explanation:
 Initially, nums = [1, 2, 3, 4, 5]  
Rotating once to the left results in nums = [2, 3, 4, 5, 1].


Example 2:
Input:
 nums = [-1, 0, 3, 6]  

Output:
 [0, 3, 6, -1]  

Explanation:
 Initially, nums = [-1, 0, 3, 6]  
Rotating once to the left results in nums = [0, 3, 6, -1].

---

## 🔹 Key Observations & Intuition
* Store the value of the first element of the array in a temporary variable.
* Iterate through the array starting from the second element.
* Shift each element one position to the left by assigning the current element to the position of its predecessor.
* After completing the iteration, place the value from the temporary variable into the last position of the array.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Create a dummy array of the same length as the original array.
Shift all elements in the original array toward the left, copying them into the dummy array.
After shifting, place the value of the 0th index of the original array into the last element of the dummy array.
Finally, print the dummy array which now contains the left-shifted elements with the 0th element moved to the last position.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
// Class containing the solve method
class Solution {

    // Function to solve and shift array elements left by one position
    public static void solve(int[] arr, int n) {
        int[] temp = new int[n];  // Temporary array to store shifted elements

        // Shift elements to the left by one position
        for (int i = 1; i < n; i++) {
            temp[i - 1] = arr[i];
        }
        temp[n - 1] = arr[0];  // First element moves to the last position

        // Print the rotated array
        for (int i = 0; i < n; i++) {
            System.out.print(temp[i] + " ");
        }
        System.out.println();
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        int n = 5;  // Size of the array
        int[] arr = {1, 2, 3, 4, 5};  // Original array

        Solution.solve(arr, n);  // Call the solve function from Solution class
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Store the value of the first element of the array in a temporary variable.
Iterate through the array starting from the second element.
Shift each element one position to the left by assigning the current element to the position of its predecessor.
After completing the iteration, place the value from the temporary variable into the last position of the array.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
class Solution {
    public void rotateArrayByOne(int[] nums) {
        // Store the first element in a temporary variable
        int temp = nums[0];
        
        // Shift elements to the left
        for (int i = 1; i < nums.length; i++) {
            nums[i - 1] = nums[i];
        }

        // Place the first element at the end
        nums[nums.length - 1] = temp;
    }
}

class Main {
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {1, 2, 3, 4, 5};

        solution.rotateArrayByOne(nums);

        // Output the rotated array
        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q6
# Rotate array by K elements

## 🔹 Problem Summary
Problem Statement: Given an array of integers, rotating array of elements by k elements either left or right.

**Examples:**
Examples

Input : nums = [1, 2, 3, 4, 5, 6, 7], k = 2, right
Output : [6, 7, 1, 2, 3, 4, 5]
Explanation : rotate 1 step to the right: [7, 1, 2, 3, 4, 5, 6]
rotate 2 steps to the right: [6, 7, 1, 2, 3, 4, 5] 

Input : nums = [1, 2, 3, 4, 5, 6], k=2, left
Output : [3, 4, 5, 6, 1, 2]
Explanation :rotate 1 step to the left: [2, 3, 4, 5, 6, 1]
rotate 2 steps to the left: [3, 4, 5, 6, 1, 2]

---

## 🔹 Key Observations & Intuition
* Instead of simulating each rotation one by one, we can get the rotated array in-place by reversing specific parts of the array. This works because rotating is just rearranging sections of the array.
* For Right Rotation by k steps:
* Reverse the entire array
* Reverse the first k elements
* Reverse the remaining n - k elements

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
Right Rotation: We store the last k elements of the array into a temporary array. Then we shift all the other elements (n-k elements) to the right by k positions. Finally, we place the elements from the temporary array at the beginning of the original array. This achieves a right rotation by k positions.
Take the last k elements and store them in a temporary array.
Shift the first n-k elements to the right by k positions.
Copy the k stored elements from the temporary array to the start of the original array.

Left Rotation: We store the first k elements in a temporary array. Then we shift the remaining n-k elements to the left by k positions. Finally, we copy the elements from the temporary array to the end of the array. This achieves a left rotation by k positions.
Store the first k elements in a temporary array.
Shift the remaining elements to the left by k positions.
Copy the k stored elements to the end of the original array.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Instead of simulating each rotation one by one, we can get the rotated array in-place by reversing specific parts of the array. This works because rotating is just rearranging sections of the array.
For Right Rotation by k steps:
Reverse the entire array
Reverse the first k elements
Reverse the remaining n - k elements
For Left Rotation by k steps:
Reverse the first k elements
Reverse the remaining n - k elements
Reverse the entire array
Normalize k by doing k = k % N
If direction is "right":
Reverse the entire array
Reverse the first k elements
Reverse the rest (from k to end)
If direction is "left":
Reverse the first k elements
Reverse the rest (from k to end)
Reverse the entire array

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q7
# Move all Zeros to the end of the array

## 🔹 Problem Summary
Problem Statement: You are given an array of integers, your task is to move all the zeros in the array to the end of the array and move non-negative integers to the front by maintaining their order.

**Examples:**
Examples
Input: 1 ,0 ,2 ,3 ,0 ,4 ,0 ,1
Output: 1 ,2 ,3 ,4 ,1 ,0 ,0 ,0
Explanation: All the zeros are moved to the end and non-negative integers are moved to front by maintaining order

Input : 1,2,0,1,0,4,0
Output: 1,2,1,4,0,0,0
Explanation : All the zeros are moved to the end and non-negative integers are moved to front by maintaining order

---

## 🔹 Key Observations & Intuition
* We can optimize the approach using 2 pointers i.e. i and j. The pointer j will point to the first 0 in the array and i will point to the next index.
* Assume, the given array is {1, 0, 2, 3, 2, 0, 0, 4, 5, 1}. Now, initially, we will place the 2-pointers like the following:
* First, we iterate through the array to locate the position of the first zero, using a pointer j. If no zero is found, no further steps are needed.
* Next, we set a second pointer i to j + 1 and start moving it forward through the array.
* While moving i, whenever we encounter a non-zero element a[i], we swap it with the element at index j. After the swap, since j now holds a non-zero value, we increment j to point to the next zero.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
The extremely naive solution, we can think of, involves the use of an extra array. The algorithm is as follows.
Suppose, there are N-X zeros and X non-zero elements in the array. We will first copy those X non-zero elements from the original array to a temporary array.
Then, we will copy the elements from the temporary array one by one and fill the first X places of the original array.
The last N-X places of the original array will be then filled with zero. Now, our task is completed.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
We can optimize the approach using 2 pointers i.e. i and j. The pointer j will point to the first 0 in the array and i will point to the next index.

Assume, the given array is {1, 0, 2, 3, 2, 0, 0, 4, 5, 1}. Now, initially, we will place the 2-pointers like the following:

First, we iterate through the array to locate the position of the first zero, using a pointer j. If no zero is found, no further steps are needed.
Next, we set a second pointer i to j + 1 and start moving it forward through the array.
While moving i, whenever we encounter a non-zero element a[i], we swap it with the element at index j. After the swap, since j now holds a non-zero value, we increment j to point to the next zero.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q8
# Linear Search in C

## 🔹 Problem Summary
Problem Statement: Given an array, and an element num the task is to find if num is present in the given array or not. If present print the index of the element or print -1.

**Examples:**
Examples
Example 1:
Input:
 arr[] = 1 2 3 4 5, num = 3  

Output:
 2  `

Explanation:
 3 is present at the 2nd index of the array.


Example 2:
Input:
 arr[] = 5 4 3 2 1, num = 5  

Output:
 0  

Explanation:
 5 is present at the 0th index of the array.

---

## 🔹 Key Observations & Intuition
* Given an array, traverse through the entire array.
* For each element, check if the element is present in the array.
* If the element is found, print the index of the element.
* If the element is not found, print -1.

---

## 🔹 Approaches

### ➤ Brute Force
**(Approach)**

**Idea:**
Given an array, traverse through the entire array.
For each element, check if the element is present in the array.
If the element is found, print the index of the element.
If the element is not found, print -1.

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Approach** | Refer to approach details | Refer to approach details |

---

---
Q9
# Union of Two Sorted Arrays

## 🔹 Problem Summary
Problem Statement: Given two sorted arrays, arr1, and arr2 of size n and m. Find the union of two sorted arrays.

**Examples:**
Examples


Input:n = 5,m = 5 arr1[] = {1,2,3,4,5}  arr2[] = {2,3,4,4,5}
Output: {1,2,3,4,5}
Explanation: Common Elements in arr1 and arr2  are:  2,3,4,5
Distnict Elements in arr1 are : 1
Distnict Elemennts in arr2 are : No distinct elements.
Union of arr1 and arr2 is {1,2,3,4,5}

Input:n = 10,m = 7,arr1[] = {1,2,3,4,5,6,7,8,9,10}arr2[] = {2,3,4,4,5,11,12}
Output: {1,2,3,4,5,6,7,8,9,10,11,12}
Explanation: Common Elements in arr1 and arr2  are:  2,3,4,5
Distnict Elements in arr1 are : 1,6,7,8,9,10
Distnict Elemennts in arr2 are : 11,12
Union of arr1 and arr2 is {1,2,3,4,5,6,7,8,9,10,11,12}

---

## 🔹 Key Observations & Intuition
* Since both arrays are sorted, we can efficiently find their union by iterating through them simultaneously. Using two pointers, one for each array, we compare elements and add the smaller one to the result (skipping duplicates). If elements are equal, add once and move both pointers. This way, we merge the arrays like in merge sort, avoiding extra space for maps or sets and achieving linear time complexity.
* Initialize two pointers at the start of both arrays.
* While neither pointer has reached the end:
* If element pointed by first pointer is smaller, add it to result if not duplicate, move first pointer.
* If element pointed by second pointer is smaller, add it to result if not duplicate, move second pointer.

---

## 🔹 Approaches

### ➤ Brute Force
**(Approach 1- Using Map)**

**Idea:**
Our aim is to find the common elements in arr1 and arr2, and the distinct elements of arr1,arr2. Use a Single map to find the frequencies of elements in arr1 and arr2.

As we are using only a single map the common element in arr1 and arr2 are treated as a single element for finding frequency, so there would be no duplicates.

Why not unordered_map?
In unordered_map the keys are stored in random order, while in the map the keys are stored in sorted order (ascending order by default). As we require elements of the union to be in ascending order, using a map is preferable.

We can also use unordered_map, but after finding the union of arr1 and arr2, we need to sort the union vector to get the elements of the union in sorted order.

Initialize an empty map named freq to store element frequencies
Initialize an empty vector named Union to store unique elements
Loop through the first array arr1:
For each element, increment its count in freq
Loop through the second array arr2:
For each element, increment its count in freq
Iterate over each key-value pair in freq (keys will be sorted because map is ordered):
Push the key (element) into the Union vector

**Java Code:**
```java
import java.util.*;

// Define the Solution class
class Solution {
    // Function to find union of two arrays
    public List<Integer> FindUnion(int[] arr1, int[] arr2, int n, int m) {
        // Create TreeMap to store elements in sorted order
        TreeMap<Integer, Integer> freq = new TreeMap<>();
        // Loop through first array and store frequency
        for (int i = 0; i < n; i++)
            freq.put(arr1[i], freq.getOrDefault(arr1[i], 0) + 1);
        // Loop through second array and store frequency
        for (int i = 0; i < m; i++)
            freq.put(arr2[i], freq.getOrDefault(arr2[i], 0) + 1);
        // Create a list to store union result
        List<Integer> Union = new ArrayList<>();
        // Traverse map keys and add to union list
        for (int key : freq.keySet())
            Union.add(key);
        // Return the union list
        return Union;
    }
}

// Driver class
public class Main {
    public static void main(String[] args) {
        // Define size of first array
        int n = 10;
        // Define size of second array
        int m = 7;
        // Initialize first array
        int[] arr1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        // Initialize second array
        int[] arr2 = {2, 3, 4, 4, 5, 11, 12};
        // Create object of Solution class
        Solution obj = new Solution();
        // Call FindUnion method
        List<Integer> Union = obj.FindUnion(arr1, arr2, n, m);
        // Print output message
        System.out.println("Union of arr1 and arr2 is ");
        // Print all elements of union
        for (int val : Union)
            System.out.print(val + " ");
    }
}
```

---

### ➤ Better Approach
**(Approach 2- Using Set)**

**Idea:**
Using a set we can find the distinct elements because the set does not hold any duplicates. Hence we can find the union of arr1 and arr2.

Initialize an empty set.
Insert all elements from the first array into set.
Insert all elements from the second array into set.
Convert the set into a list/array to get the result.
If required in sorted order, sort the list before returning.
Return/print the union result.
Why not unordered_set?
In unordered_set the elements are stored in random order, while in a set the keys are stored in sorted order (ascending order by default). As we require elements of the union to be in ascending order, using a set is preferable.

We can also use unordered_set, but after finding the union of arr1 and arr2, we need to sort the union vector to get the elements of the union in sorted order.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the union of two arrays using set
    public List<Integer> findUnion(int[] arr1, int[] arr2) {
        // Create a TreeSet to store unique sorted elements
        Set<Integer> st = new TreeSet<>();

        // Insert elements from first array
        for (int num : arr1) {
            st.add(num);
        }

        // Insert elements from second array
        for (int num : arr2) {
            st.add(num);
        }

        // Convert set to list
        return new ArrayList<>(st);
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int[] arr2 = {2, 3, 4, 4, 5, 11, 12};

        Solution obj = new Solution();
        List<Integer> result = obj.findUnion(arr1, arr2);

        System.out.print("Union of arr1 and arr2 is: ");
        for (int val : result) {
            System.out.print(val + " ");
        }
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach - Two Pointers)**

**Idea:**
Since both arrays are sorted, we can efficiently find their union by iterating through them simultaneously. Using two pointers, one for each array, we compare elements and add the smaller one to the result (skipping duplicates). If elements are equal, add once and move both pointers. This way, we merge the arrays like in merge sort, avoiding extra space for maps or sets and achieving linear time complexity.
Initialize two pointers at the start of both arrays.
While neither pointer has reached the end:
If element pointed by first pointer is smaller, add it to result if not duplicate, move first pointer.
If element pointed by second pointer is smaller, add it to result if not duplicate, move second pointer.
If both elements are equal, add one to result if not duplicate, move both pointers.
After exiting loop, append remaining elements from either array, skipping duplicates.
Return the result array containing the union.

**Complexity:**
* **Time Complexity:** .
* **Space Complexity:** N/A

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find union of two sorted arrays using two pointers
    public List<Integer> findUnion(int[] arr1, int[] arr2, int n, int m) {
        // List to store union elements
        List<Integer> Union = new ArrayList<>();

        // Initialize pointers
        int i = 0, j = 0;

        // Iterate while both arrays have elements
        while (i < n && j < m) {
            // If element in arr1 is smaller
            if (arr1[i] < arr2[j]) {
                // Add if empty or not duplicate
                if (Union.isEmpty() || Union.get(Union.size() - 1) != arr1[i])
                    Union.add(arr1[i]);
                i++;  // Move pointer in arr1
            }
            // If element in arr2 is smaller
            else if (arr2[j] < arr1[i]) {
                // Add if empty or not duplicate
                if (Union.isEmpty() || Union.get(Union.size() - 1) != arr2[j])
                    Union.add(arr2[j]);
                j++;  // Move pointer in arr2
            }
            else {
                // Elements are equal, add once if not duplicate
                if (Union.isEmpty() || Union.get(Union.size() - 1) != arr1[i])
                    Union.add(arr1[i]);
                i++; j++;  // Move both pointers
            }
        }

        // Append remaining elements from arr1
        while (i < n) {
            if (Union.isEmpty() || Union.get(Union.size() - 1) != arr1[i])
                Union.add(arr1[i]);
            i++;
        }

        // Append remaining elements from arr2
        while (j < m) {
            if (Union.isEmpty() || Union.get(Union.size() - 1) != arr2[j])
                Union.add(arr2[j]);
            j++;
        }

        // Return the union list
        return Union;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
        int[] arr2 = {2, 3, 4, 4, 5, 11, 12};
        int n = arr1.length, m = arr2.length;

        Solution obj = new Solution();
        List<Integer> result = obj.findUnion(arr1, arr2, n, m);

        System.out.print("Union of arr1 and arr2 is: ");
        for (int val : result) System.out.print(val + " ");
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **.** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Approach 1- Using Map** | Refer to approach details | Refer to approach details |
| **Approach 2- Using Set** | Refer to approach details | Refer to approach details |
| **Optimal Approach - Two Pointers** | . | N/A |

---

---
Q10
# Find the missing number in an array

## 🔹 Problem Summary
Problem Statement: Given an integer N and an array of size N-1 containing N-1 numbers between 1 to N. Find the number(between 1 to N), that is not present in the given array..

**Examples:**
Examples
Example 1:
Input Format: N = 5, array[] = {1,2,4,5}
Result: 3
Explanation: In the given array, number 3 is missing. So, 3 is the answer.


Example 2:
Input Format: N = 3, array[] = {1,3}
Result: 2
Explanation: In the given array, number 2 is missing. So, 2 is the answer.

---

## 🔹 Key Observations & Intuition
* Intuition
* Two important properties of XOR are the following:
* XOR of two same numbers is always 0 i.e. a ^ a = 0. ←Property 1.
* XOR of a number with 0 will result in the number itself i.e. 0 ^ a = a. ←Property 2
* Approach

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
For each number between 1 to N, we will try to find it in the given array using linear search. And if we don’t find any of them, we will return the number.
We will run a loop from 1 to N.
For each integer, we will try to find it in the given array using linear search.
For that, we will run another loop to iterate over the array and consider a flag variable to indicate if the element exists in the array. Flag = 1 means the element is present and flag = 0 means the element is missing.
Initially, the flag value will be set to 0. While iterating the array, if we find the element, we will set the flag to 1 and break out from the loop.
Now, for any number i, if we cannot find it, the flag will remain 0 even after iterating the whole array and we will return the number.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the missing number from 1 to N
    public int missingNumber(int[] a, int N) {
        // Check each number from 1 to N
        for (int i = 1; i <= N; i++) {
            boolean found = false;

            // Check if i exists in the array using linear search
            for (int j = 0; j < N - 1; j++) {
                if (a[j] == i) {
                    found = true;
                    break;
                }
            }

            // If not found, return it as the missing number
            if (!found) return i;
        }

        // This line should not be reached
        return -1;
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 4, 5};
        int N = 5;

        Solution obj = new Solution();
        int ans = obj.missingNumber(a, N);
        System.out.println("The missing number is: " + ans);
    }
}
```

---

### ➤ Better Approach
**(Optimised Apporach 1)**

**Idea:**
Intuition
We know that the summation of the first N numbers is (N*(N+1))/2. We can say this S1. Now, in the given array, every number between 1 to N except one number is present. So, if we add the numbers of the array (say S2), the difference between S1 and S2 will be the missing number. Because, while adding all the numbers of the array, we did not add that particular number that is missing.
Approach
We will first calculate the summation of first N natural numbers(i.e. 1 to N) using the specified formula.
Then we will add all the array elements using a loop.
Finally, we will consider the difference between the summation of the first N natural numbers and the sum of the array elements.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the missing number using sum formula
    public int missingNumber(int[] a, int N) {
        // Calculate the sum of first N natural numbers
        int sum = (N * (N + 1)) / 2;

        // Calculate the sum of elements in the array
        int actualSum = 0;
        for (int i = 0; i < N - 1; i++) {
            actualSum += a[i];
        }

        // Missing number is the difference
        return sum - actualSum;
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 4, 5};
        int N = 5;

        Solution obj = new Solution();
        int ans = obj.missingNumber(a, N);
        System.out.println("The missing number is: " + ans);
    }
}
```

---

### ➤ Optimal Approach
**(Optimised Approach 2)**

**Idea:**
Intuition
Two important properties of XOR are the following:
XOR of two same numbers is always 0 i.e. a ^ a = 0. ←Property 1.
XOR of a number with 0 will result in the number itself i.e. 0 ^ a = a. ←Property 2
Approach
We will first run a loop, from 0 to size-2(as the length of the array = sie-1).
Inside the loop, xor2 variable will calculate the XOR of array elements i.e.xor2 = xor2 ^ a[i]
And the xor1 variable will calculate the XOR of 1 to N-1 i.e. xor1 = xor1 ^ (i+1).
After the loop ends we will XOR xor1 and N to get the total XOR of 1 to N.
Finally, the answer will be the XOR of xor1 and xor2.

**Java Code:**
```java
class Solution {
    // Function to find the missing number using XOR approach
    public int missingNumber(int[] a, int N) {
        int xor1 = 0, xor2 = 0;

        // XOR all the elements and numbers from 1 to N-1
        for (int i = 0; i < N - 1; i++) {
            xor2 ^= a[i];        // XOR of array elements
            xor1 ^= (i + 1);     // XOR of numbers from 1 to N-1
        }

        xor1 ^= N; // Include N in the XOR

        // XOR of xor1 and xor2 gives the missing number
        return xor1 ^ xor2;
    }

    public static void main(String[] args) {
        int[] a = {1, 2, 4, 5};
        int N = 5;

        Solution obj = new Solution();
        int ans = obj.missingNumber(a, N);
        System.out.println("The missing number is: " + ans);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Optimised Apporach 1** | Refer to approach details | Refer to approach details |
| **Optimised Approach 2** | Refer to approach details | Refer to approach details |

---

---
Q11
# Count Maximum Consecutive One's in the array

## 🔹 Problem Summary
Problem Statement: Given an array that contains only 1 and 0 return the count of maximum consecutive ones in the array..

**Examples:**
Examples
Example 1:
Input: prices = {1, 1, 0, 1, 1, 1}
Output: 3
Explanation: There are two consecutive 1’s and three consecutive 1’s in the array out of which maximum is 3.

Example 2:
Input: prices = {1, 0, 1, 1, 0, 1} 
Output: 2
Explanation: There are two consecutive 1's in the array.

---

## 🔹 Key Observations & Intuition
* We need to find the longest streak of consecutive 1’s in a binary array. A simple idea is to traverse the array while maintaining a counter. Every time we encounter a 1, we increase the counter. If we encounter a 0, the streak breaks, so we reset the counter to 0. At each step, we track the maximum streak length seen so far.
* Initialize two variables:
* cnt → counts the current streak of 1’s.
* maxi → stores the maximum streak found so far.
* Traverse through the array:

---

## 🔹 Approaches

### ➤ Brute Force
**(Approach)**

**Idea:**
We need to find the longest streak of consecutive 1’s in a binary array. A simple idea is to traverse the array while maintaining a counter. Every time we encounter a 1, we increase the counter. If we encounter a 0, the streak breaks, so we reset the counter to 0. At each step, we track the maximum streak length seen so far.

Initialize two variables:
cnt → counts the current streak of 1’s.
maxi → stores the maximum streak found so far.
Traverse through the array:
If nums[i] == 1, increment cnt.
If nums[i] == 0, reset cnt to 0.
Update maxi = max(maxi, cnt) at each step.
Finally, return maxi, which contains the length of the longest consecutive 1’s.

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
        int[] nums = {1, 1, 0, 1, 1, 1};

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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Approach** | Refer to approach details | Refer to approach details |

---

---
Q12
# Find the number that appears once, and the other numbers twice

## 🔹 Problem Summary
Problem Statement: Given a non-empty array of integers arr, every element appears twice except for one. Find that single one.

**Examples:**
Examples
Example 1:
Input Format: arr[] = {2,2,1}
Result: 1
Explanation: In this array, only the element 1 appear once and so it is the answer.


Example 2:
Input Format: arr[] = {4,1,2,1,2}
Result: 4
Explanation: In this array, only element 4 appear once and the other elements appear twice. So, 4 is the answer.

---

## 🔹 Key Observations & Intuition
* Intuition
* Two important properties of XOR are the following:
* XOR of two same numbers is always 0 i.e. a ^ a = 0. ←Property 1.
* XOR of a number with 0 will result in the number itself i.e. 0 ^ a = a. ←Property 2
* Approach

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Intuition
For every element present in the array, we will do a linear search and count the occurrence. If for any element, the occurrence is 1, we will return it.
Approach
First, we will run a loop to select the elements of the array one by one.
For every element of the array, we will perform a linear search using another loop and count its occurrence.
If for any element the occurrence is 1, we will return it.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
class Solution {
    // Function to find the single element using brute force
    public int getSingleElement(int[] arr) {
        int n = arr.length;

        for (int i = 0; i < n; i++) {
            int num = arr[i];
            int count = 0;

            // Count how many times num occurs
            for (int j = 0; j < n; j++) {
                if (arr[j] == num)
                    count++;
            }

            // If only once, return it
            if (count == 1) return num;
        }

        return -1; // fallback, won't be hit if array has a single element
    }

    public static void main(String[] args) {
        int[] arr = {4, 1, 2, 1, 2};

        Solution obj = new Solution();
        int ans = obj.getSingleElement(arr);

        System.out.println("The single element is: " + ans);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Intuition
In the previous approach, we were finding the occurrence of an element using linear search. We can optimize this using hashing technique. We can simply hash the elements along with their occurrences in the form of (key, value) pair. Thus, we can reduce the cost of finding the occurrence and hence the time complexity. Now, hashing can be done in two different ways and they are the following:
Array hashing(not applicable if the array contains negatives or very large numbers)
Hashing using the map data structure
Approach
First, we will find the maximum element(say maxElement) to know the size of the hash array.
Then we will declare a hash array of size maxElement+1.
Now, using another loop we will store the elements of the array along with their frequency in the hash array.
After that, using another loop we will iterate over the hash array, and try to find the element for which the frequency is 1, and finally, we will return that particular element.
While searching for the answer finally, we can either use a loop from 0 to n(i.e. Size of the array) or use a loop from 0 to maxElement. So, the time complexity will change accordingly

**Complexity:**
* **Time Complexity:** . Now, hashing can be done in two different ways and they are the following:
* **Space Complexity:** N/A

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the single element using a hash array
    public int getSingleElement(int[] arr) {
        int n = arr.length;

        // Step 1: Find maximum element
        int maxi = arr[0];
        for (int i = 0; i < n; i++) {
            maxi = Math.max(maxi, arr[i]);
        }

        // Step 2: Create frequency array of size maxi+1
        int[] hash = new int[maxi + 1];

        // Step 3: Count frequencies
        for (int i = 0; i < n; i++) {
            hash[arr[i]]++;
        }

        // Step 4: Find element with frequency = 1
        for (int i = 0; i < n; i++) {
            if (hash[arr[i]] == 1)
                return arr[i];
        }

        return -1; // fallback
    }

    public static void main(String[] args) {
        int[] arr = {4, 1, 2, 1, 2};
        Solution obj = new Solution();
        int ans = obj.getSingleElement(arr);
        System.out.println("The single element is: " + ans);
    }
}
```

---

### ➤ Optimal Approach
**(Optimised Approach)**

**Idea:**
Intuition
Two important properties of XOR are the following:
XOR of two same numbers is always 0 i.e. a ^ a = 0. ←Property 1.
XOR of a number with 0 will result in the number itself i.e. 0 ^ a = a. ←Property 2
Approach
We will just perform the XOR of all elements of the array using a loop and the final XOR will be the answer.

**Java Code:**
```java
class Solution {
    // Function to find the element that appears once using XOR
    public int getSingleElement(int[] arr) {
        int xorr = 0;

        // XOR all elements — duplicates cancel each other out
        for (int num : arr) {
            xorr ^= num;
        }

        return xorr;
    }

    public static void main(String[] args) {
        int[] arr = {4, 1, 2, 1, 2};

        Solution obj = new Solution();
        int ans = obj.getSingleElement(arr);
        System.out.println("The single element is: " + ans);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | . Now, hashing can be done in two different ways and they are the following: | N/A |
| **Optimised Approach** | Refer to approach details | Refer to approach details |

---

---
Q13
# Longest Subarray with given Sum K(Positives)

## 🔹 Problem Summary
Problem Statement: Given an array nums of size n and an integer k, find the length of the longest sub-array that sums to k. If no such sub-array exists, return 0.

**Examples:**
Examples
Example 1:
Input:
 nums = [10, 5, 2, 7, 1, 9], k = 15  

Output:
 4  

Explanation:
 The longest sub-array with a sum equal to 15 is [5, 2, 7, 1], which has a length of 4. This sub-array starts at index 1 and ends at index 4, and the sum of its elements (5 + 2 + 7 + 1) equals 15. Therefore, the length of this sub-array is 4.


Example 2:
Input:
 nums = [-3, 2, 1], k = 6  

Output:
 0  

Explanation:
 There is no sub-array in the array that sums to 6. Therefore, the output is 0.

---

## 🔹 Key Observations & Intuition
* Two pointers, left and right, are used to maintain the current window of elements in the array. These pointers represent the start and end of the current subarray.
* A variable, sum, is used to keep track of the sum of the elements in the current window between left and right.
* The right pointer expands the window by including new elements, increasing the sum.
* If the sum of the window exceeds k, the left pointer shrinks the window by removing elements from the start until the sum is less than or equal to k.
* If the sum of the current window equals k, the maximum length of such a subarray is updated.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
We first run a loop with index i to select every possible starting index of the subarray. These starting indices range from 0 to n-1 where n is the size of the array.
Inside this loop, we run another loop with index j to select the ending index of the subarray. For each subarray starting at index i, the ending index j can range from i to n-1.
Next, for each subarray starting from index i and ending at index j (i.e., arr[i...j]), we run an additional loop to calculate the sum of all the elements in that subarray.
If the sum equals k, we consider its length, which is (j - i + 1). Among all such subarrays, we keep track of the maximum length by comparing all the lengths found so far.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
// GFG.java
import java.util.*;

class Solution {

    public int longestSubarray(int[] nums, int k) {
        int n = nums.length;
        int maxLength = 0;

        // starting index
        for (int startIndex = 0; startIndex < n; startIndex++) {
            // ending index
            for (int endIndex = startIndex; endIndex < n; endIndex++) {

                /* add all the elements of
                   subarray = nums[startIndex...endIndex] */
                int currentSum = 0;
                for (int i = startIndex; i <= endIndex; i++) {
                    currentSum += nums[i];
                }

                if (currentSum == k) {
                    maxLength = Math.max(maxLength, endIndex - startIndex + 1);
                }
            }
        }
        return maxLength;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] a = { -1, 1, 1 };
        int k = 1;

        // Create an instance of the Solution class
        Solution solution = new Solution();

        // Function call to get the result
        int len = solution.longestSubarray(a, k);

        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Two pointers, left and right, are used to maintain the current window of elements in the array. These pointers represent the start and end of the current subarray.
A variable, sum, is used to keep track of the sum of the elements in the current window between left and right.
The right pointer expands the window by including new elements, increasing the sum.
If the sum of the window exceeds k, the left pointer shrinks the window by removing elements from the start until the sum is less than or equal to k.
If the sum of the current window equals k, the maximum length of such a subarray is updated.
The process continues until the right pointer traverses the entire array.
Finally, the maximum length of the subarray with sum k is returned as the result.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

// Class containing the sliding window algorithm
class Solution {
    public int longestSubarray(int[] nums, int k) {
        int n = nums.length;

        // To store the maximum length of the subarray
        int maxLen = 0;

        // Pointers for sliding window
        int left = 0, right = 0;

        // Sum of the current window
        int sum = nums[0];

        // Traverse through the array
        while (right < n) {

            // Shrink the window if sum exceeds k
            while (left <= right && sum > k) {
                sum -= nums[left];
                left++;
            }

            // Update max length if sum equals k
            if (sum == k) {
                maxLen = Math.max(maxLen, right - left + 1);
            }

            // Expand the window to the right
            right++;
            if (right < n) {
                sum += nums[right];
            }
        }

        return maxLen;
    }
}

// Separate class containing only the main method
public class Main {
    public static void main(String[] args) {
        int[] nums = {10, 5, 2, 7, 1, 9};
        int k = 15;

        // Create Solution object
        Solution sol = new Solution();

        // Function call to find the result
        int ans = sol.longestSubarray(nums, k);

        // Output the result
        System.out.println("The length of longest subarray having sum k is: " + ans);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q14
# Longest Subarray with sum K | [Postives and Negatives]

## 🔹 Problem Summary
Problem Statement: Given an array and a sum k, we need to print the length of the longest subarray that sums to k.

**Examples:**
Examples
Example 1:
Input Format: N = 3, k = 5, array[] = {2,3,5}
Result: 2
Explanation: The longest subarray with sum 5 is {2, 3}. And its length is 2.

Example 2:
Input Format: N = 3, k = 1, array[] = {-1, 1, 1}
Result: 3
Explanation: The longest subarray with sum 1 is {-1, 1, 1}. And its length is 3.

---

## 🔹 Key Observations & Intuition
* First, we will declare a map to store the prefix sums and the indices.
* Then we will run a loop(say i) from index 0 to n-1(n = size of the array).
* For each index i, we will do the following:
* We will add the current element i.e. a[i] to the prefix sum.
* If the sum is equal to k, we should consider the length of the current subarray i.e. i+1. We will compare this length with the existing length and consider the maximum one.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Intuition

We will check the sum of every possible subarray and consider the one with the sum k and the maximum length among them. To get every possible subarray sum, we will be using three nested loops. The first loops(say i and j) will iterate over every possible starting index and ending index of a subarray. Basically, in each iteration, the subarray range will be from index i to index j. Using another loop we will get the sum of the elements of the subarray [i…..j]. Among all the subarrays with sum k, we will consider the one with the maximum length.

Approach
First, go through each position in the list as the starting point of a group of numbers.
For each starting point, go through every possible ending point that comes after or at the same position.
For each group formed by the starting and ending positions, add up all the numbers in that group.
If the total matches the target value, check how many numbers are in the group and keep track of the largest size found.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class SubarraySolver {
    // Method to find the longest subarray with sum equal to k
    public int getLongestSubarray(int[] a, int k) {
        int n = a.length;
        int len = 0;

        // Loop for starting index
        for (int i = 0; i < n; i++) {
            // Loop for ending index
            for (int j = i; j < n; j++) {
                int sum = 0;

                // Calculate sum of elements between i and j
                for (int idx = i; idx <= j; idx++) {
                    sum += a[idx];
                }

                // If sum equals k, update max length
                if (sum == k) {
                    len = Math.max(len, j - i + 1);
                }
            }
        }
        return len;
    }

    public static void main(String[] args) {
        int[] a = { -1, 1, 1 };
        int k = 1;

        SubarraySolver solver = new SubarraySolver();
        int len = solver.getLongestSubarray(a, k);

        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
First, go through each position in the list to choose a starting point for a group of numbers.
For each starting point, go through every position after it to select the current number and extend the group.
As you move through the list, keep adding each number to the total of the current group.
If the total becomes equal to the desired value, check how many numbers are in the group and keep track of the largest group that meets the condition.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;
class SubarraySolver {
// Method to find the longest subarray whose sum equals k
    public int getLongestSubarray(int[] a, int k) {
        int n = a.length; // Total number of elements in the array
        int maxLen = 0;   // Variable to store the maximum length found

        // Outer loop to select the starting index of the subarray
        for (int i = 0; i < n; i++) {
            int sum = 0; // Reset sum for each new starting index

            // Inner loop to extend the subarray from the starting index 'i'
            for (int j = i; j < n; j++) {
                sum += a[j]; // Incrementally add elements to the sum

                // If the current subarray sum equals k
                if (sum == k) {
                    // Calculate the length of the subarray (j - i + 1)
                    // Update maxLen if this subarray is longer
                    maxLen = Math.max(maxLen, j - i + 1);
                }
            }
        }

        return maxLen; // Return the maximum length found
    }

    // Main method to test the implementation
    public static void main(String[] args) {
        int[] a = { -1, 1, 1 }; // Sample input array
        int k = 1; // Target sum

        SubarraySolver solver = new SubarraySolver(); // Create an instance of the solver
        int len = solver.getLongestSubarray(a, k); // Call the method to find the result

        // Print the length of the longest subarray
        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
First, we will declare a map to store the prefix sums and the indices.
Then we will run a loop(say i) from index 0 to n-1(n = size of the array).
For each index i, we will do the following:
We will add the current element i.e. a[i] to the prefix sum.
If the sum is equal to k, we should consider the length of the current subarray i.e. i+1. We will compare this length with the existing length and consider the maximum one.
We will calculate the prefix sum i.e. x-k, of the remaining subarray.
If that sum of the remaining part i.e. x-k exists in the map, we will calculate the length i.e. i-preSumMap[x-k], and consider the maximum one comparing it with the existing length we have achieved until now.
If the sum, we got after step 3.1, does not exist in the map we will add that with the current index into the map. We are checking the map before insertion because we want the index to be as minimum as possible and so we will consider the earliest index where the sum x-k has occurred. [Detailed discussion in the edge case section]
In this approach, we are using the concept of the prefix sum to solve this problem. Here, the prefix sum of a subarray ending at index i, simply means the sum of all the elements of that subarray.
Dry Run

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class SubarraySolver {
    // Method to find the longest subarray with sum equal to k
    public int getLongestSubarray(int[] a, int k) {
        int n = a.length;
        Map<Integer, Integer> preSumMap = new HashMap<>(); // prefix sum -> index
        int sum = 0;       // Running sum
        int maxLen = 0;    // Longest subarray length

        for (int i = 0; i < n; i++) {
            sum += a[i]; // Update running prefix sum

            // Case 1: If full subarray from 0 to i has sum = k
            if (sum == k) {
                maxLen = i + 1;
            }

            // Case 2: If (sum - k) was seen before
            int rem = sum - k;
            if (preSumMap.containsKey(rem)) {
                int len = i - preSumMap.get(rem); // Length of current valid subarray
                maxLen = Math.max(maxLen, len);
            }

            // Store the first occurrence of a prefix sum
            if (!preSumMap.containsKey(sum)) {
                preSumMap.put(sum, i);
            }
        }

        return maxLen;
    }

    public static void main(String[] args) {
        int[] a = { -1, 1, 1 };
        int k = 1;

        SubarraySolver solver = new SubarraySolver();
        int len = solver.getLongestSubarray(a, k);

        System.out.println("The length of the longest subarray is: " + len);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---


# ═══════════════════════════════════════
# Medium Problems
# ═══════════════════════════════════════

---
Q15
# Two Sum : Check if a pair with given sum exists in Array

## 🔹 Problem Summary
Problem Statement: Given an array of integers arr[] and an integer target.

**Examples:**
Examples


Input: N = 5, arr[] = {2,6,5,8,11}, target = 14
Output : YES
Explanation: arr[1] + arr[3] = 14. So, the answer is “YES” for first variant for second variant output will be : [1,3].

Input: N = 5, arr[] = {2,6,5,8,11}, target = 15
Output : NO.
Explanation: There exist no such two numbers whose sum is equal to the target.

---

## 🔹 Key Observations & Intuition
* In this approach, we will first sort the array and will try to choose the numbers in a greedy way.
* We will keep a left pointer at the first index and a right pointer at the last index. Now until left < right, we will check the sum of arr[left] and arr[right]. Now if the sum < target, we need bigger numbers and so we will increment the left pointer. But if sum > target, we need to consider lesser numbers and so we will decrement the right pointer.
* If sum == target we will return either “YES” or the indices as per the question. But if the left crosses the right pointer, we will return “NO” or {-1, -1}.
* We will sort the given array first.
* Now, we will take two pointers i.e. left, which points to the first index, and right, which points to the last index.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute force Approach)**

**Idea:**
For each element of the given array, we will try to search for another element such that its sum is equal to the target. If such two numbers exist, we will return the indices or “YES” accordingly.
First, we will use a loop (say i) to select the indices of the array one by one.
For every index i, we will traverse through the remaining array using another loop (say j) to find the other number such that the sum is equal to the target (i.e. arr[i] + arr[j] = target).
Observation: In every iteration, if the inner loop starts from index 0, we will be checking the same pair of numbers multiple times. For example, in iteration 1, for i = 0, we will check for the pair arr[0] and arr[1]. Again in iteration 2, for i = 1, we will check arr[1] and arr[0]. So, to eliminate these same pairs, we will start the inner loop from i + 1.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import.java.util.*;
class Solution {
    // Function to check if any two numbers sum up to target (variant 1)
    public String twoSumExists(int[] arr, int target) {
        int n = arr.length;
        // Outer loop picks one element at a time
        for (int i = 0; i < n; i++) {
            // Inner loop searches for another element that complements arr[i]
            for (int j = i + 1; j < n; j++) {
                // If sum equals target, return "YES"
                if (arr[i] + arr[j] == target) {
                    return "YES";
                }
            }
        }
        // No pair found that sums to target
        return "NO";
    }

    // Function to return indices of two numbers that sum to target (variant 2)
    public int[] twoSumIndices(int[] arr, int target) {
        int n = arr.length;
        // Outer loop picks one element at a time
        for (int i = 0; i < n; i++) {
            // Inner loop searches for another element that complements arr[i]
            for (int j = i + 1; j < n; j++) {
                // If sum equals target, return the pair of indices
                if (arr[i] + arr[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        // No such pair found
        return new int[]{-1, -1};
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();

        int[] arr = {2, 6, 5, 8, 11};
        int target = 14;

        // Variant 1
        System.out.println(sol.twoSumExists(arr, target));

        // Variant 2
        int[] res = sol.twoSumIndices(arr, target);
        System.out.println("[" + res[0] + ", " + res[1] + "]");
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Basically, in the previous approach we selected one element and then searched for the other one using a loop. Here instead of using a loop, we will use the HashMap to check if the other element i.e. target (selected element) exists. Thus we can trim down the time complexity of the problem.

And for the second variant, we will store the element along with its index in the HashMap. Thus we can easily retrieve the index of the other element i.e. target (selected element) without iterating the array.
We will select the element of the array one by one using a loop (say i).
Then we will check if the other required element (i.e. target - arr[i]) exists in the HashMap.
If that element exists, then we will return “YES” for the first variant or we will return the current index i.e. i, and the index of the element found using map i.e. mp[target - arr[i]].
If that element does not exist, then we will just store the current element in the HashMap along with its index. Because in the future, the current element might be a part of our answer.
Finally, if we are out of the loop, that means there is no such pair whose sum is equal to the target. In this case, we will return either “NO” or {-1, -1} as per the variant of the question.

**Complexity:**
* **Time Complexity:** of the problem.
* **Space Complexity:** N/A

**Java Code:**
```java
import java.util.HashMap;

class Solution {
    // Variant 1: Check if two numbers sum to target using hashing
    public String twoSumExists(int[] arr, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        // Iterate over all elements
        for (int i = 0; i < arr.length; i++) {
            int complement = target - arr[i];
            // Check if complement exists in map
            if (map.containsKey(complement)) {
                return "YES";  // Pair found
            }
            // Store current element and its index
            map.put(arr[i], i);
        }
        // No pair found
        return "NO";
    }

    // Variant 2: Return indices of two numbers that sum to target using hashing
    public int[] twoSumIndices(int[] arr, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            int complement = target - arr[i];
            // If complement found, return indices
            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }
            // Store current element and index
            map.put(arr[i], i);
        }
        // No pair found
        return new int[] { -1, -1 };
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] arr = {2, 6, 5, 8, 11};
        int target = 14;

        System.out.println(sol.twoSumExists(arr, target));
        int[] res = sol.twoSumIndices(arr, target);
        System.out.println("[" + res[0] + ", " + res[1] + "]");
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
In this approach, we will first sort the array and will try to choose the numbers in a greedy way.

We will keep a left pointer at the first index and a right pointer at the last index. Now until left < right, we will check the sum of arr[left] and arr[right]. Now if the sum < target, we need bigger numbers and so we will increment the left pointer. But if sum > target, we need to consider lesser numbers and so we will decrement the right pointer.

If sum == target we will return either “YES” or the indices as per the question. But if the left crosses the right pointer, we will return “NO” or {-1, -1}.
We will sort the given array first.
Now, we will take two pointers i.e. left, which points to the first index, and right, which points to the last index.
Now using a loop we will check the sum of arr[left] and arr[right] until left < right.
If arr[left] + arr[right] > sum, we will decrement the right pointer.
If arr[left] + arr[right] < sum, we will increment the left pointer.
If arr[left] + arr[right] == sum, we will return the result.
Finally, if no results are found we will return “NO” or {-1, -1}.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.Arrays;

class Solution {
    // Variant 1: Check if two numbers sum to target using two-pointer approach
    public String twoSumExists(int[] arr, int target) {
        int n = arr.length;
        
        // Create an array of pairs [value, original_index]
        int[][] numsWithIndex = new int[n][2];
        
        // Store each element with its original index
        for (int i = 0; i < n; i++) {
            numsWithIndex[i][0] = arr[i]; // value
            numsWithIndex[i][1] = i;      // original index
        }
        
        // Sort the array based on the value, not index
        Arrays.sort(numsWithIndex, (a, b) -> Integer.compare(a[0], b[0]));

        // Initialize two pointers: one at start, one at end
        int left = 0, right = n - 1;
        
        // Run loop until pointers cross
        while (left < right) {
            // Calculate the sum of values at pointers
            int sum = numsWithIndex[left][0] + numsWithIndex[right][0];
            
            if (sum == target) {
                // Found the pair, return "YES"
                return "YES";
            } else if (sum < target) {
                // Sum is less than target, so move left pointer right to increase sum
                left++;
            } else {
                // Sum is greater than target, so move right pointer left to decrease sum
                right--;
            }
        }
        
        // If loop ends without returning, no pair found
        return "NO";
    }

    // Variant 2: Return indices of two numbers that sum to target
    public int[] twoSumIndices(int[] arr, int target) {
        int n = arr.length;
        int[][] numsWithIndex = new int[n][2];
        
        // Store element with original index
        for (int i = 0; i < n; i++) {
            numsWithIndex[i][0] = arr[i];
            numsWithIndex[i][1] = i;
        }
        
        // Sort by the value to apply two-pointer
        Arrays.sort(numsWithIndex, (a, b) -> Integer.compare(a[0], b[0]));

        int left = 0, right = n - 1;
        while (left < right) {
            int sum = numsWithIndex[left][0] + numsWithIndex[right][0];
            if (sum == target) {
                // Return original indices of the two numbers found
                return new int[] {numsWithIndex[left][1], numsWithIndex[right][1]};
            } else if (sum < target) {
                // Increase sum by moving left pointer forward
                left++;
            } else {
                // Decrease sum by moving right pointer backward
                right--;
            }
        }
        
        // No pair found
        return new int[] {-1, -1};
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] arr = {2, 6, 5, 8, 11};
        int target = 14;

        System.out.println(sol.twoSumExists(arr, target)); // Output: YES
        int[] res = sol.twoSumIndices(arr, target);
        System.out.println("[" + res[0] + ", " + res[1] + "]"); // Output: [1, 3]
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | of the problem. | N/A |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q16
# Sort an array of 0s, 1s and 2s

## 🔹 Problem Summary
Problem Statement: Given an array nums consisting of only 0, 1, or 2. Sort the array in non-decreasing order. The sorting must be done in-place, without making a copy of the original array.

**Examples:**
Examples

Input: nums = [1, 0, 2, 1, 0]
Output: [0, 0, 1, 1, 2]
Explanation: The nums array in sorted order has 2 zeroes, 2 ones and 1 two

Input: nums = [0, 0, 1, 1, 1]
Output: [0, 0, 1, 1, 1]
Explanation: The nums array in sorted order has 2 zeroes, 3 ones and zero twos.

---

## 🔹 Key Observations & Intuition
* This approach is a direct implementation of the Dutch National Flag algorithm.
* We divide the array into three partitions using three pointers – low, mid, and high.
* From 0 to low-1, we’ll keep only 0s
* From low to mid-1, only 1s
* From high+1 to n-1, only 2

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute force Approach)**

**Idea:**
We are given an array containing only 0s, 1s, and 2s. Since the values are fixed and known, the simplest approach is to first count how many 0s, 1s, and 2s are present in the array. After counting, we overwrite the original array based on the frequency of these values first fill it with 0s, then 1s, then 2s. This does not require any extra array and modifies the input array in-place.
Initialize three counters to count the frequency of 0s, 1s, and 2s
Loop through the array once and count each number
In the second loop, fill the array based on the frequency of each number: first 0s, then 1s, then 2s

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to sort the array containing only 0s, 1s and 2s
    public void sortZeroOneTwo(int[] nums) {
        // Initialize count variables for 0s, 1s, and 2s
        int count0 = 0, count1 = 0, count2 = 0;

        // Count the frequency of 0s, 1s, and 2s
        for(int num : nums) {
            if(num == 0) count0++;
            else if(num == 1) count1++;
            else count2++;
        }

        // Overwrite the array with sorted values
        int index = 0;

        // Fill with 0s
        while(count0-- > 0) {
            nums[index++] = 0;
        }

        // Fill with 1s
        while(count1-- > 0) {
            nums[index++] = 1;
        }

        // Fill with 2s
        while(count2-- > 0) {
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

        for(int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Since the array contains only 0s, 1s, and 2s, we can exploit this limited range of values to count how many of each element exists. Once we know how many 0s, 1s, and 2s are in the array, we can simply overwrite the original array by placing that many 0s, then 1s, and then 2s in order. This approach avoids sorting and gives a linear-time, constant-space solution.
Initialize three counters to zero: one each for 0s, 1s, and 2s.
Traverse the entire array and increment the respective counter based on the element value.
After counting, overwrite the array:
Place all 0s first (based on count of 0s).
Then all 1s (based on count of 1s).
Then all 2s (based on count of 2s).

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to sort an array containing only 0s, 1s, and 2s
    public void sortZeroOneTwo(int[] nums) {
        // Count of 0s, 1s, and 2s
        int cnt0 = 0, cnt1 = 0, cnt2 = 0;

        // First pass: Count the number of 0s, 1s, and 2s
        for (int num : nums) {
            if (num == 0) cnt0++;
            else if (num == 1) cnt1++;
            else cnt2++;
        }

        // Second pass: Fill the array with 0s, then 1s, then 2s

        // Fill the first 'cnt0' elements with 0
        for (int i = 0; i < cnt0; i++) {
            nums[i] = 0;
        }

        // Fill the next 'cnt1' elements with 1
        for (int i = cnt0; i < cnt0 + cnt1; i++) {
            nums[i] = 1;
        }

        // Fill the remaining elements with 2
        for (int i = cnt0 + cnt1; i < nums.length; i++) {
            nums[i] = 2;
        }
    }
}

// Driver code
class Main {
    public static void main(String[] args) {
        int[] nums = {0, 2, 1, 2, 0, 1};

        Solution sol = new Solution();
        sol.sortZeroOneTwo(nums);

        System.out.println("After sorting:");
        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
This approach is a direct implementation of the Dutch National Flag algorithm.

We divide the array into three partitions using three pointers – low, mid, and high.
From 0 to low-1, we’ll keep only 0s
From low to mid-1, only 1s
From high+1 to n-1, only 2
The range from mid to high is the unsorted zone we’re scanning and fixing. At each step:
If arr[mid] == 0, it belongs to the left section → swap with low, move both low and mid.
If arr[mid] == 1, it’s already in the middle section → just move mid.
If arr[mid] == 2, it belongs to the right section → swap with high, only move high.
When you swap with high, you don’t move mid because the incoming value might still be 0 or 2 which needs processing.This ensures we sort the array in one single pass without using extra space.
Start with three pointers at the beginning, middle, and end of the array.
Iterate while the middle pointer is less than or equal to the end pointer.
If the current element belongs to the front section:
Swap it with the element at the front boundary.
Move both front and middle boundaries forward.
If the current element belongs to the middle section:
Move the middle boundary forward.
If the current element belongs to the end section:
Swap it with the element at the end boundary.
Move the end boundary backward.
Repeat until all elements are in their correct zones.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to sort array containing 0s, 1s, and 2s using Dutch National Flag Algorithm
    public void sortZeroOneTwo(int[] nums) {
        // Initialize three pointers: low and mid at 0, high at the end
        int low = 0, mid = 0, high = nums.length - 1;

        // Continue processing until mid crosses high
        while (mid <= high) {
            // If current element is 0, swap with low and move both low and mid forward
            if (nums[mid] == 0) {
                int temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;
                low++;
                mid++;
            }
            // If current element is 1, just move mid forward
            else if (nums[mid] == 1) {
                mid++;
            }
            // If current element is 2, swap with high and move only high backward
            else {
                int temp = nums[mid];
                nums[mid] = nums[high];
                nums[high] = temp;
                high--;
            }
        }
    }
}

// Driver code
class Main {
    public static void main(String[] args) {
        Solution obj = new Solution();
        int[] nums = {2, 0, 2, 1, 1, 0};

        obj.sortZeroOneTwo(nums);

        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q17
# Find the Majority Element that occurs more than N/2 times

## 🔹 Problem Summary
Problem Statement: Given an integer array nums of size n, return the majority element of the array.

The majority element of an array is an element that appears more than n/2 times in the array. The array is guaranteed to have a majority element.

**Examples:**
Examples
Example 1:
Input:
 nums = [7, 0, 0, 1, 7, 7, 2, 7, 7]  

Output:
 7  

Explanation:
 The number 7 appears 5 times in the 9-sized array, making it the most frequent element.


Example 2:
Input:
 nums = [1, 1, 1, 2, 1, 2]  

Output:
 1  

Explanation:
 The number 1 appears 4 times in the 6-sized array, making it the most frequent element.

---

## 🔹 Key Observations & Intuition
* Initialize two variables: count to track the count of elements, and element to keep track of the element being counted.
* Traverse through the given array. If count is 0, store the current value of the array as element.
* If the current element in the array is the same as element, increment the count by 1.
* If the current element is different from element, decrement the count by 1.
* At the end of the traversal, the integer stored in element will be the expected result (the majority element).

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Iterate through the array to select each element one by one.
For each selected element, run another loop to count its occurrences in the given array.
If the occurrence of any element is greater than the floor of (N/2), return that element immediately as the majority element.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

// Class containing the majority element logic
class Solution {
    // Function to find the majority element in an array
    public int majorityElement(int[] nums) {
        
        // Size of the given array
        int n = nums.length;
        
        // Iterate through each element of the array
        for (int i = 0; i < n; i++) {
            
            // Counter to count occurrences of nums[i]
            int cnt = 0; 
            
            // Count the frequency of nums[i] in the array
            for (int j = 0; j < n; j++) {
                if (nums[j] == nums[i]) {
                    cnt++;
                }
            }
            
            // Check if frequency of nums[i] is greater than n/2
            if (cnt > (n / 2)) {
                // Return the majority element
                return nums[i]; 
            }
        }
        
        // Return -1 if no majority element is found
        return -1; 
    }
}

// Separate class containing only the main method
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};
        
        // Create an instance of Solution class
        Solution sol = new Solution();
 
        int ans = sol.majorityElement(arr);
        
        // Print the majority element found
        System.out.println("The majority element is: " + ans);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Use a hashmap to store elements as (key, value) pairs, where the key is the element of the array and the value is the number of times it occurs.
Traverse the array and update the value of the corresponding key in the hashmap.
Simultaneously check if the value (the count) of any key is greater than the floor of (N/2).
If the value is greater than the floor of (N/2), return the key immediately as the majority element.
If no majority element is found, continue iterating through the array.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

// Class containing the majority element logic
class Solution {
    // Function to find the majority element in an array
    public int majorityElement(int[] nums) {
        
        // Size of the given array
        int n = nums.length;
        
        // Hash map to store element counts
        HashMap<Integer, Integer> map = new HashMap<>();
        
        // Count occurrences of each element
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        /* Iterate through the map to
           find the majority element */
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() > n / 2) {
                return entry.getKey();
            }
        }
        
        // Return -1 if no majority element is found
        return -1;
    }
}

// Separate class containing only the main method
public class Main {
    public static void main(String[] args) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};
        
        // Create an instance of Solution class
        Solution sol = new Solution();
 
        int ans = sol.majorityElement(arr);
        
        // Print the majority element found
        System.out.println("The majority element is: " + ans);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Initialize two variables: count to track the count of elements, and element to keep track of the element being counted.
Traverse through the given array. If count is 0, store the current value of the array as element.
If the current element in the array is the same as element, increment the count by 1.
If the current element is different from element, decrement the count by 1.
At the end of the traversal, the integer stored in element will be the expected result (the majority element).

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

// Class containing the majority element logic
class Solution {
    // Function to find the majority element in an array
    public int majorityElement(int[] nums) {
        // Size of the given array
        int n = nums.length;
        
        // Count variable
        int cnt = 0;
        
        // Candidate element
        int el = 0;
        
        // Step 1: Find the potential majority element
        for (int i = 0; i < n; i++) {
            if (cnt == 0) {
                cnt = 1;
                el = nums[i];
            } else if (el == nums[i]) {
                cnt++;
            } else {
                cnt--;
            }
        }
        
        // Step 2: Verify the candidate
        int cnt1 = 0;
        for (int i = 0; i < n; i++) {
            if (nums[i] == el) {
                cnt1++;
            }
        }
        
        // Return the element if it's a majority
        if (cnt1 > (n / 2)) {
            return el;
        }
        
        // No majority found
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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q18
# Kadane's Algorithm : Maximum Subarray Sum in an Array

## 🔹 Problem Summary
Problem Statement: Given an integer array nums, find the subarray with the largest sum and return the sum of the elements present in that subarray.

A subarray is a contiguous non-empty sequence of elements within an array.

**Examples:**
Examples
Example 1:
Input:
 nums = [2, 3, 5, -2, 7, -4]  

Output:
 15  

Explanation:
 The subarray from index 0 to index 4 has the largest sum = 15, which is the maximum sum of any contiguous subarray.


Example 2:
Input:
 nums = [-2, -3, -7, -2, -10, -4]  

Output:
 -2  

Explanation:
 The largest sum is -2, which comes from taking the element at index 0 or index 3 as the subarray. Since all numbers are negative, the subarray with the least negative number gives the largest sum.

---

## 🔹 Key Observations & Intuition
* Follow-up Question:
* Can you print the subarray that has the maximum sum?
* Approach:
* Start by iterating through the array using a variable i. During each iteration, add the current element arr[i] to a running sum variable.
* Initialize a start variable to keep track of the starting index of the current subarray.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Iterate through the array with variable i, which represents the starting index of each subarray. The possible values for i range from 0 to n-1, where n is the size of the array.
Inside the first loop, run another loop with variable j that represents the ending index of the subarray. For each i, j can range from i to n-1.
For each subarray defined by i and j, iterate through its elements to calculate the sum. Maintain a variable, max, to store the maximum sum encountered so far during the iteration.
At each step, compare the current subarray sum with the current max value. If the current sum is greater, update the max value with the new sum.
Finally, after completing all iterations, return the max variable, which holds the maximum sum of any subarray.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays
    public int maxSubArray(int[] nums) {
        
        /* Initialize maximum sum with
           the smallest possible integer */
        int maxi = Integer.MIN_VALUE;

        // Iterate over each starting index of subarrays
        for (int i = 0; i < nums.length; i++) {
            
            /* Iterate over each ending index
               of subarrays starting from i */
            for (int j = i; j < nums.length; j++) {
                
                /* Variable to store the sum
                   of the current subarray */
                int sum = 0;

                // Calculate the sum of subarray nums[i...j]
                for (int k = i; k <= j; k++) {
                    sum += nums[k];
                }

                /* Update maxi with the maximum of its current
                   value and the sum of the current subarray */
                maxi = Math.max(maxi, sum);
            }
        }

        // Return the maximum subarray sum found
        return maxi;
    }
}

// Separate Main class
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Iterate through the array with variable i, which represents the starting index of each subarray. The possible values for i range from 0 to n-1, where n is the size of the array.
Inside the first loop, iterate again with variable j to signify the ending index of the subarray and the current element of the subarray. For each i, j can range from i to n-1.
For each subarray defined by i and j, add the current element at arr[j] to the sum of the previous subarray.
Keep track of the maximum sum encountered during the iteration using a variable, say maxSum, and update it whenever a greater sum is found.
Once all iterations are complete, return maxSum as the maximum sum of all subarrays.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays
    public int maxSubArray(int[] nums) {
        
        /* Initialize maximum sum with
           the smallest possible integer */
        int maxi = Integer.MIN_VALUE;

        // Iterate over each starting index of subarrays
        for (int i = 0; i < nums.length; i++) {
            
            /* Variable to store the sum
               of the current subarray */
            int sum = 0; 
            
            /* Iterate over each ending index
               of subarrays starting from i */
            for (int j = i; j < nums.length; j++) {
                
                /* Add the current element nums[j] to
                   the sum i.e. sum of nums[i...j-1] */
                sum += nums[j];

                /* Update maxi with the maximum of its current
                   value and the sum of the current subarray */
                maxi = Math.max(maxi, sum);
            }
        }

        // Return the maximum subarray sum found
        return maxi;
    }
}

// Separate Main class in the same file
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### ➤ Better Approach
**(Optimal Approach)**

**Idea:**
Iterate through the array using a variable i. During each iteration, add the current element arr[i] to a running sum variable.
Keep track of the maximum sum encountered during the iteration by comparing the current sum with the previous maximum sum, and update it if the current sum is greater.
If at any point the sum becomes negative, reset it to 0, as a negative sum won't contribute positively to the overall maximum sum.
Continue the iteration until all elements in the array are processed.
Finally, return the maximum sum encountered during the iteration.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays
    public int maxSubArray(int[] nums) {
        
        // Maximum sum
        long maxi = Long.MIN_VALUE; 
        
        // Current sum of subarray 
        long sum = 0; 
        
        // Iterate through the array
        for (int i = 0; i < nums.length; i++) {
            
            // Add current element to the sum
            sum += nums[i]; 
            
            // Update maxi if current sum is greater
            if (sum > maxi) {
                maxi = sum; 
            }
            
            // Reset sum to 0 if it becomes negative
            if (sum < 0) {
                sum = 0; 
            }
        }
        
        // Return the maximum subarray sum found
        return (int) maxi;
    }
}

// Separate Main class in same file
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### ➤ Optimal Approach
**(Follow Up)**

**Idea:**
Follow-up Question:

Can you print the subarray that has the maximum sum?

Approach:
Start by iterating through the array using a variable i. During each iteration, add the current element arr[i] to a running sum variable.
Initialize a start variable to keep track of the starting index of the current subarray.
Use ansStart and ansEnd to store the starting and ending indices of the subarray with the maximum sum found so far. Initially, set both to -1.
If the current sum is greater than the previous maximum sum, update ansStart to start and ansEnd to i.
If the sum becomes negative at any point, reset it to 0 and set start to i + 1 to start a new subarray.
After processing all elements, ansStart and ansEnd will point to the starting and ending indices of the subarray with the maximum sum.
Return the subarray from arr[ansStart] to arr[ansEnd].

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays and print the subarray having maximum sum
    public int maxSubArray(int[] nums) {
        
        // Maximum sum
        long maxi = Long.MIN_VALUE; 
        
        // Current sum of subarray
        long sum = 0; 
        
        // Starting index of current subarray
        int start = 0; 
        
        // Indices of the maximum sum subarray
        int ansStart = -1, ansEnd = -1; 
        
        // Iterate through the array
        for (int i = 0; i < nums.length; i++) {
            
            // Update starting index if sum is reset
            if (sum == 0) {
                start = i;
            }
            
            // Add current element to the sum
            sum += nums[i]; 
            
            // Update maxi and subarray indices if current sum is greater
            if (sum > maxi) {
                maxi = sum;
                ansStart = start;
                ansEnd = i;
            }
            
            // Reset sum to 0 if it becomes negative
            if (sum < 0) {
                sum = 0;
            }
        }
        
        // Printing the subarray
        System.out.print("The subarray is: [");
        for (int i = ansStart; i <= ansEnd; i++) {
            System.out.print(nums[i] + " ");
        }
        System.out.println("]");

        // Return the maximum subarray sum found
        return (int) maxi;
    }
}

// Separate Main class
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |
| **Follow Up** | Refer to approach details | Refer to approach details |

---

---
Q19
# Kadane's Algorithm : Maximum Subarray Sum in an Array

## 🔹 Problem Summary
Problem Statement: Given an integer array nums, find the subarray with the largest sum and return the sum of the elements present in that subarray.

A subarray is a contiguous non-empty sequence of elements within an array.

**Examples:**
Examples
Example 1:
Input:
 nums = [2, 3, 5, -2, 7, -4]  

Output:
 15  

Explanation:
 The subarray from index 0 to index 4 has the largest sum = 15, which is the maximum sum of any contiguous subarray.


Example 2:
Input:
 nums = [-2, -3, -7, -2, -10, -4]  

Output:
 -2  

Explanation:
 The largest sum is -2, which comes from taking the element at index 0 or index 3 as the subarray. Since all numbers are negative, the subarray with the least negative number gives the largest sum.

---

## 🔹 Key Observations & Intuition
* Follow-up Question:
* Can you print the subarray that has the maximum sum?
* Approach:
* Start by iterating through the array using a variable i. During each iteration, add the current element arr[i] to a running sum variable.
* Initialize a start variable to keep track of the starting index of the current subarray.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Iterate through the array with variable i, which represents the starting index of each subarray. The possible values for i range from 0 to n-1, where n is the size of the array.
Inside the first loop, run another loop with variable j that represents the ending index of the subarray. For each i, j can range from i to n-1.
For each subarray defined by i and j, iterate through its elements to calculate the sum. Maintain a variable, max, to store the maximum sum encountered so far during the iteration.
At each step, compare the current subarray sum with the current max value. If the current sum is greater, update the max value with the new sum.
Finally, after completing all iterations, return the max variable, which holds the maximum sum of any subarray.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays
    public int maxSubArray(int[] nums) {
        
        /* Initialize maximum sum with
           the smallest possible integer */
        int maxi = Integer.MIN_VALUE;

        // Iterate over each starting index of subarrays
        for (int i = 0; i < nums.length; i++) {
            
            /* Iterate over each ending index
               of subarrays starting from i */
            for (int j = i; j < nums.length; j++) {
                
                /* Variable to store the sum
                   of the current subarray */
                int sum = 0;

                // Calculate the sum of subarray nums[i...j]
                for (int k = i; k <= j; k++) {
                    sum += nums[k];
                }

                /* Update maxi with the maximum of its current
                   value and the sum of the current subarray */
                maxi = Math.max(maxi, sum);
            }
        }

        // Return the maximum subarray sum found
        return maxi;
    }
}

// Separate Main class
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Iterate through the array with variable i, which represents the starting index of each subarray. The possible values for i range from 0 to n-1, where n is the size of the array.
Inside the first loop, iterate again with variable j to signify the ending index of the subarray and the current element of the subarray. For each i, j can range from i to n-1.
For each subarray defined by i and j, add the current element at arr[j] to the sum of the previous subarray.
Keep track of the maximum sum encountered during the iteration using a variable, say maxSum, and update it whenever a greater sum is found.
Once all iterations are complete, return maxSum as the maximum sum of all subarrays.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays
    public int maxSubArray(int[] nums) {
        
        /* Initialize maximum sum with
           the smallest possible integer */
        int maxi = Integer.MIN_VALUE;

        // Iterate over each starting index of subarrays
        for (int i = 0; i < nums.length; i++) {
            
            /* Variable to store the sum
               of the current subarray */
            int sum = 0; 
            
            /* Iterate over each ending index
               of subarrays starting from i */
            for (int j = i; j < nums.length; j++) {
                
                /* Add the current element nums[j] to
                   the sum i.e. sum of nums[i...j-1] */
                sum += nums[j];

                /* Update maxi with the maximum of its current
                   value and the sum of the current subarray */
                maxi = Math.max(maxi, sum);
            }
        }

        // Return the maximum subarray sum found
        return maxi;
    }
}

// Separate Main class in the same file
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### ➤ Better Approach
**(Optimal Approach)**

**Idea:**
Iterate through the array using a variable i. During each iteration, add the current element arr[i] to a running sum variable.
Keep track of the maximum sum encountered during the iteration by comparing the current sum with the previous maximum sum, and update it if the current sum is greater.
If at any point the sum becomes negative, reset it to 0, as a negative sum won't contribute positively to the overall maximum sum.
Continue the iteration until all elements in the array are processed.
Finally, return the maximum sum encountered during the iteration.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays
    public int maxSubArray(int[] nums) {
        
        // Maximum sum
        long maxi = Long.MIN_VALUE; 
        
        // Current sum of subarray 
        long sum = 0; 
        
        // Iterate through the array
        for (int i = 0; i < nums.length; i++) {
            
            // Add current element to the sum
            sum += nums[i]; 
            
            // Update maxi if current sum is greater
            if (sum > maxi) {
                maxi = sum; 
            }
            
            // Reset sum to 0 if it becomes negative
            if (sum < 0) {
                sum = 0; 
            }
        }
        
        // Return the maximum subarray sum found
        return (int) maxi;
    }
}

// Separate Main class in same file
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

### ➤ Optimal Approach
**(Follow Up)**

**Idea:**
Follow-up Question:

Can you print the subarray that has the maximum sum?

Approach:
Start by iterating through the array using a variable i. During each iteration, add the current element arr[i] to a running sum variable.
Initialize a start variable to keep track of the starting index of the current subarray.
Use ansStart and ansEnd to store the starting and ending indices of the subarray with the maximum sum found so far. Initially, set both to -1.
If the current sum is greater than the previous maximum sum, update ansStart to start and ansEnd to i.
If the sum becomes negative at any point, reset it to 0 and set start to i + 1 to start a new subarray.
After processing all elements, ansStart and ansEnd will point to the starting and ending indices of the subarray with the maximum sum.
Return the subarray from arr[ansStart] to arr[ansEnd].

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find maximum sum of subarrays and print the subarray having maximum sum
    public int maxSubArray(int[] nums) {
        
        // Maximum sum
        long maxi = Long.MIN_VALUE; 
        
        // Current sum of subarray
        long sum = 0; 
        
        // Starting index of current subarray
        int start = 0; 
        
        // Indices of the maximum sum subarray
        int ansStart = -1, ansEnd = -1; 
        
        // Iterate through the array
        for (int i = 0; i < nums.length; i++) {
            
            // Update starting index if sum is reset
            if (sum == 0) {
                start = i;
            }
            
            // Add current element to the sum
            sum += nums[i]; 
            
            // Update maxi and subarray indices if current sum is greater
            if (sum > maxi) {
                maxi = sum;
                ansStart = start;
                ansEnd = i;
            }
            
            // Reset sum to 0 if it becomes negative
            if (sum < 0) {
                sum = 0;
            }
        }
        
        // Printing the subarray
        System.out.print("The subarray is: [");
        for (int i = ansStart; i <= ansEnd; i++) {
            System.out.print(nums[i] + " ");
        }
        System.out.println("]");

        // Return the maximum subarray sum found
        return (int) maxi;
    }
}

// Separate Main class
public class Main {
    public static void main(String[] args) {
        int[] arr = { -2, 1, -3, 4, -1, 2, 1, -5, 4 };

        // Create an instance of Solution class
        Solution sol = new Solution();

        int maxSum = sol.maxSubArray(arr);

        // Print the max subarray sum
        System.out.println("The maximum subarray sum is: " + maxSum);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |
| **Follow Up** | Refer to approach details | Refer to approach details |

---

---
Q20
# Stock Buy And Sell

## 🔹 Problem Summary
Problem Statement: You are given an array of prices where prices[i] is the price of a given stock on an ith day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock. Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

**Examples:**
Examples

Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note: That buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.

---

## 🔹 Key Observations & Intuition
* The idea is to track the minimum price so far while traversing the array and calculate the profit if we sold today. This way, we can constantly update the maximum profit without using nested loops. We’re basically simulating:
* What’s the lowest price we’ve seen so far?
* What’s the profit if we sold today?
* Is it better than our best so far?
* Initialize a variable to store the minimum price so far, set it to a very large value initially.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
We try every possible pair of days (buy day and sell day after buy) and calculate the profit. The maximum profit among all these pairs is our answer. If no profit is possible, return 0.
Loop through all days to consider each as a possible buy day.
For each buy day, loop through all future days to consider them as sell days.
Calculate the profit for each (buy, sell) pair.
Track the maximum profit seen.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
class Solution {
    // Function to calculate max profit using brute force
    public int stockbuySell(int[] prices) {
        // Initialize max profit to 0
        int maxProfit = 0;

        // Loop through each day as a potential buy day
        for (int i = 0; i < prices.length; i++) {
            // Loop through each future day as a potential sell day
            for (int j = i + 1; j < prices.length; j++) {
                // Calculate profit
                int profit = prices[j] - prices[i];

                // Update max profit if higher
                maxProfit = Math.max(maxProfit, profit);
            }
        }

        // Return the maximum profit
        return maxProfit;
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] prices = {7, 1, 5, 3, 6, 4};
        System.out.println("Max Profit: " + sol.stockbuySell(prices));
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
The idea is to track the minimum price so far while traversing the array and calculate the profit if we sold today. This way, we can constantly update the maximum profit without using nested loops. We’re basically simulating:
What’s the lowest price we’ve seen so far?
What’s the profit if we sold today?
Is it better than our best so far?
Initialize a variable to store the minimum price so far, set it to a very large value initially.
Initialize a variable to store the maximum profit seen so far, set it to 0 initially.
Loop through each price in the array.
Update the minimum price if the current price is smaller.
Calculate the profit if the stock were bought at the minimum price and sold at the current price.
Update the maximum profit if this new profit is higher.
Return the maximum profit after the loop ends.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import.java.util.*;
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
            }
            // Else calculate profit and update maxProfit if it's greater
            else {
                maxProfit = Math.max(maxProfit, price - minPrice);
            }
        }

        // Return the maximum profit found
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
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q21
# Rearrange Array Elements by Sign

## 🔹 Problem Summary
Problem Statement: There’s an array ‘A’ of size ‘N’ with an equal number of positive and negative elements. Without altering the relative order of positive and negative elements, you must return an array of alternately positive and negative values.

**Examples:**
Examples
Example 1:
Input:
arr[] = {1,2,-4,-5}, N = 4
Output:
1 -4 2 -5
Explanation: 
Positive elements = 1,2
Negative elements = -4,-5
To maintain relative ordering, 1 must occur before 2, and -4 must occur before -5.




Example 2:
Input:
arr[] = {1,2,-3,-1,-2,-3}, N = 6
Output:
1 -3 2 -1 3 -2
Explanation: 
Positive elements = 1,2,3
Negative elements = -3,-1,-2
To maintain relative ordering, 1 must occur before 2, and 2 must occur before 3.
Also, -3 should come before -1, and -1 should come before -2.

---

## 🔹 Key Observations & Intuition
* In this optimal approach, we will try to solve the problem in a single pass and try to arrange the array elements in the correct order in that pass only.
* We know that the resultant array must start from a positive element so we initialize the positive index as 0 and negative index as 1 and start traversing the array such that whenever we see the first positive element, it occupies the space at 0 and then posIndex increases by 2 (alternate places).
* Similarly, when we encounter the first negative element, it occupies the position at index 1, and then each time we find a negative number, we put it on the negIndex and it increments by 2.
* When both the negIndex and posIndex exceed the size of the array, we see that the whole array is now rearranged alternatively according to the sign.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
In this simple approach, since the number of positive and negative elements are the same, we put positives into an array called “pos” and negatives into an array called “neg”.
After segregating each of the positive and negative elements, we start putting them alternatively back into array A.
Since the array must begin with a positive number and the start index is 0, so all the positive numbers would be placed at even indices (2*i) and negatives at the odd indices (2*i+1), where i is the index of the pos or neg array while traversing them simultaneously.
This approach uses O(N+N/2) of running time due to multiple traversals which we’ll try to optimize in the optimized approach given below.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

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
            A[2 * i] = pos.get(i);       // Even index → positive
            A[2 * i + 1] = neg.get(i);   // Odd index → negative
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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
In this optimal approach, we will try to solve the problem in a single pass and try to arrange the array elements in the correct order in that pass only.
We know that the resultant array must start from a positive element so we initialize the positive index as 0 and negative index as 1 and start traversing the array such that whenever we see the first positive element, it occupies the space at 0 and then posIndex increases by 2 (alternate places).
Similarly, when we encounter the first negative element, it occupies the position at index 1, and then each time we find a negative number, we put it on the negIndex and it increments by 2.
When both the negIndex and posIndex exceed the size of the array, we see that the whole array is now rearranged alternatively according to the sign.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

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

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q22
# next_permutation : find next lexicographically greater permutation

## 🔹 Problem Summary
Problem Statement: Given an array Arr[] of integers, rearrange the numbers of the given array into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange to the lowest possible order (i.e., sorted in ascending order).

**Examples:**
Examples
Input: Arr[] = {1,3,2}
Output: {2,1,3}
Explanation: All permutations of {1,2,3} are {{1,2,3} , {1,3,2}, {2,13} , {2,3,1} , {3,1,2} , {3,2,1}}. So, the next permutation just after {1,3,2} is {2,1,3}.

Input : Arr[] = {3,2,1}
Output: {1,2,3}
Explanation : As we see all permutations of {1,2,3}, we find {3,2,1} at the last position. So, we have to return the lowest permutation.

---

## 🔹 Key Observations & Intuition
* We want to rearrange the array to form the next greater permutation. If that's not possible (i.e., it's the last permutation), we return the smallest one (i.e., sorted ascendingly).
* To find this next permutation with minimal change, we need to find a digit that can be increased slightly to make the number bigger and then rearrange the remaining part to be the smallest possible.
* Traverse from the end and find the first index where the current digit is smaller than the next one (this is the "breaking point").
* Then again traverse from the end to find the first digit greater than the breaking point digit and swap them.
* Finally, reverse the part of the array to the right of the breaking point to get the smallest next permutation.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute-Force Approach)**

**Idea:**
The brute force approach to find the next permutation is to find all possible permutations of the array and then look for next permutation.
Find all possible permutations of elements present and store them.
Sort the permutations and search input from all possible permutations. Print the next permutation present right after it.
If the current permutation is the last, return the first permutation in the list.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
We want to rearrange the array to form the next greater permutation. If that's not possible (i.e., it's the last permutation), we return the smallest one (i.e., sorted ascendingly).

To find this next permutation with minimal change, we need to find a digit that can be increased slightly to make the number bigger and then rearrange the remaining part to be the smallest possible.
Traverse from the end and find the first index where the current digit is smaller than the next one (this is the "breaking point").
Then again traverse from the end to find the first digit greater than the breaking point digit and swap them.
Finally, reverse the part of the array to the right of the breaking point to get the smallest next permutation.
If no such breaking point exists (entire array is descending), just reverse the whole array.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

// Solution class
class Solution {
    // Function to find next permutation
    public void nextPermutation(int[] nums) {
        // Set index to -1
        int index = -1;

        // Find the first decreasing element from end
        for (int i = nums.length - 2; i >= 0; i--) {
            // If smaller found
            if (nums[i] < nums[i + 1]) {
                // Store index
                index = i;
                break;
            }
        }

        // If no index found
        if (index == -1) {
            // Reverse the entire array
            reverse(nums, 0, nums.length - 1);
            return;
        }

        // Find just larger element
        for (int i = nums.length - 1; i > index; i--) {
            // Swap them
            if (nums[i] > nums[index]) {
                swap(nums, i, index);
                break;
            }
        }

        // Reverse part after index
        reverse(nums, index + 1, nums.length - 1);
    }

    // Helper to reverse array
    private void reverse(int[] arr, int start, int end) {
        while (start < end) {
            swap(arr, start, end);
            start++;
            end--;
        }
    }

    // Helper to swap
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}

// Main class
public class Main {
    public static void main(String[] args) {
        // Input array
        int[] nums = {1, 2, 3};

        // Create object
        Solution sol = new Solution();

        // Call function
        sol.nextPermutation(nums);

        // Print result
        for (int num : nums) {
            System.out.print(num + " ");
        }
        System.out.println();
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute-Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q23
# Leaders in an Array

## 🔹 Problem Summary
Problem Statement: .

**Examples:**
Examples
Example 1:
Input:
 arr = [4, 7, 1, 0]  

Output:
 7 1 0  

Explanation:
 The rightmost element (0) is always a leader.  
7 and 1 are greater than the elements to their right, making them leaders as well.


Example 2:
Input:
 arr = [10, 22, 12, 3, 0, 6]  

Output:
 22 12 6  

Explanation:
 6 is a leader because there are no elements after it.  
12 is greater than all the elements to its right (3, 0, 6), and 22 is greater than 12, 3, 0, 6, making them leaders as well.

---

## 🔹 Key Observations & Intuition
* Set a variable max to the last element of the array (nums[sizeOfArray - 1]), as the last element is always a leader.
* Create an empty list ans to store the leader elements, and initially add the last element of the array to this list, as it is always a leader.
* Start from the second last element (index = sizeOfArray - 2) and move towards the first element (index = 0).
* For each element, compare it with the max variable. If the current element is greater than max, add this element to the ans list and update max to the current element.
* After processing all elements, the ans list will contain all the leader elements in reverse order. Reverse the ans list and return it.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
In this brute force approach, we start by checking all the elements from the start of the array to the end to determine if an element is greater than all the elements to its right (i.e., the leader).
We use nested loops for this:
The outer loop checks each element in the array to see if it is a leader.
The inner loop checks if there is any element to the right that is greater than the element being currently processed by the outer loop.
Begin by initializing the outer loop pointer at the start element and set it as the current leader.
If any element traversed is found to be greater than the current leader, the element is not considered a leader, and the outer loop pointer is incremented by 1, setting the next element as the current leader.
If no other element to the right is greater than the current element, it is added to the answer array as a leader element.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    //Function to find leaders in an array.
    public ArrayList<Integer> leaders(int[] nums) {
        ArrayList<Integer> ans = new ArrayList<>();

        // Iterate through each element in nums
        for (int i = 0; i < nums.length; i++) {
            boolean leader = true;

            /* Check whether nums[i] is greater
            than all elements to its right */
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] >= nums[i]) {
                    /* If any element to the right is greater 
                    or equal, nums[i] is not a leader */
                    leader = false;
                    break;
                }
            }

            // If nums[i] is a leader, add it to the ans list
            if (leader) {
                ans.add(nums[i]);
            }
        }

        // Return the leaders 
        return ans;
    }
}

class Main {
    public static void main(String[] args) {
        int[] nums = {1, 2, 5, 3, 1, 2};

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

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Set a variable max to the last element of the array (nums[sizeOfArray - 1]), as the last element is always a leader.
Create an empty list ans to store the leader elements, and initially add the last element of the array to this list, as it is always a leader.
Start from the second last element (index = sizeOfArray - 2) and move towards the first element (index = 0).
For each element, compare it with the max variable. If the current element is greater than max, add this element to the ans list and update max to the current element.
After processing all elements, the ans list will contain all the leader elements in reverse order. Reverse the ans list and return it.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find the leaders in an array.
    public ArrayList<Integer> leaders(int[] nums) {
        ArrayList<Integer> ans = new ArrayList<>();
        
        if (nums.length == 0) {
            return ans;
        }
        
        // Last element of the array is always a leader
        int max = nums[nums.length - 1];
        ans.add(nums[nums.length - 1]);
        
        // Check elements from right to left
        for (int i = nums.length - 2; i >= 0; i--) {
            if (nums[i] > max) {
                ans.add(nums[i]);
                max = nums[i];
            }
        }
        
        /* Reverse the list to match
        the required output order */
        Collections.reverse(ans);
        
        // Return the leaders
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

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q24
# Longest Consecutive Sequence in an Array

## 🔹 Problem Summary
Problem Statement: Given an array nums of n integers.

Return the length of the longest sequence of consecutive integers. The integers in this sequence can appear in any order.

**Examples:**
Examples
Example 1:
Input:
 nums = [100, 4, 200, 1, 3, 2]  

Output:
 4  

Explanation:
 The longest sequence of consecutive elements in the array is [1, 2, 3, 4], which has a length of 4. This sequence can be formed regardless of the initial order of the elements in the array.


Example 2:
Input:
 nums = [0, 3, 7, 2, 5, 8, 4, 6, 0, 1]  

Output:
 9  

Explanation:
 The longest sequence of consecutive elements in the array is [0, 1, 2, 3, 4, 5, 6, 7, 8], which has a length of 9.

---

## 🔹 Key Observations & Intuition
* We will use two variables: cnt to store the length of the current sequence and longest to store the maximum length found.
* First, place all the array elements into a set data structure to allow efficient lookups for consecutive numbers.
* For each element x that can start a sequence (i.e., x - 1 does not exist in the set), we follow these steps:
* Initialize cnt to 1, indicating the starting element of a new sequence.
* Use the set to search for consecutive elements such as x + 1, x + 2, and so on, to determine the maximum possible length of the current sequence. Update cnt accordingly.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
As you iterate through each number in the array, begin by checking if consecutive numbers like (x+1, x+2, x+3), and so on, exist in the array. The occurrence of the next consecutive number can be checked by using a linear search.
When you find consecutive numbers, start counting them using a counter. Increment this counter each time you find the next consecutive number in the sequence.
This counter effectively keeps track of how long the current consecutive sequence is as you move through the array and find more consecutive numbers.
Dry Run: Please refer to the video for the dry run.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to search for a given number in the array
    private boolean linearSearch(int[] a, int num) {
        // Get length of the array
        int n = a.length;
        // Traverse through the array to check if the number exists
        for (int i = 0; i < n; i++) {
            // If element matches the number, return true
            if (a[i] == num)
                return true;
        }
        // Number not found
        return false;
    }

    // Function to find the length of the longest consecutive sequence
    public int longestConsecutive(int[] nums) {
        // If the array is empty, no sequence exists
        if (nums.length == 0) {
            return 0;
        }
        
        // Get length of the array
        int n = nums.length;
        
        // Initialize the longest sequence length to 1 (minimum possible)
        int longest = 1;

        // Iterate over each element of the array
        for (int i = 0; i < n; i++) {
            // Store the current number
            int x = nums[i];
            
            // Start sequence length count from 1
            int cnt = 1;

            // Search for consecutive numbers starting from x + 1
            while (linearSearch(nums, x + 1) == true) {
                // Move to the next consecutive number
                x += 1;
                
                // Increase the count of the current sequence
                cnt += 1;
            }

            // Update the longest sequence length if the current is longer
            longest = Math.max(longest, cnt);
        }
        
        // Return the longest consecutive sequence length found
        return longest;
    }

    public static void main(String[] args) {
        // Input array of integers
        int[] a = {100, 4, 200, 1, 3, 2};

        // Create an instance of Solution class
        Solution solution = new Solution();

        // Call the function and store the result
        int ans = solution.longestConsecutive(a);
        
        // Output the result
        System.out.println("The longest consecutive sequence is " + ans);
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Begin by sorting the entire array in ascending order. This step helps group consecutive numbers together, simplifying the sequence detection process.
Use a loop to iterate through each element of the sorted array.
Track consecutive sequences by comparing each element arr[i] with the lastSmaller variable. If arr[i] - 1 == lastSmaller, increment the length of the current sequence (cnt) and update lastSmaller to arr[i].
Skip the current element if arr[i] equals lastSmaller, as it's already part of a sequence.
If arr[i] is greater than lastSmaller + 1, start a new sequence from arr[i] by updating lastSmaller to arr[i] and reset cnt to 1.
Throughout the iteration, compare cnt with longest and update longest to store the maximum sequence length encountered.
Note: Here, we are distorting the given array by sorting it.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    public int longestConsecutive(int[] nums) {
        // Store the size of the array
        int n = nums.length;

        // Return 0 if array is empty
        if (n == 0) return 0; 

        // Sort the array to bring consecutive numbers together
        Arrays.sort(nums); 

        // Variable to track the last smaller element in sequence
        int lastSmaller = Integer.MIN_VALUE; 

        // Variable to store the current sequence length
        int cnt = 0; 

        // Variable to store the longest sequence length found
        int longest = 1; 

        // Iterate through the sorted array
        for (int i = 0; i < n; i++) {
            // Case 1: Current element is exactly one greater than lastSmaller → part of sequence
            if (nums[i] - 1 == lastSmaller) {
                // Increment the sequence length
                cnt += 1; 
                // Update the last smaller element
                lastSmaller = nums[i]; 
            } 
            // Case 2: Current element is not consecutive and not a duplicate
            else if (nums[i] != lastSmaller) {
                // Reset the sequence length count to 1
                cnt = 1; 
                // Update the last smaller element
                lastSmaller = nums[i]; 
            }
            // Update the longest sequence length if the current sequence is longer
            longest = Math.max(longest, cnt); 
        }
        
        // Return the length of the longest consecutive sequence
        return longest;
    }

    public static void main(String[] args) {
        // Input array
        int[] a = {100, 4, 200, 1, 3, 2}; 

        // Create an instance of Solution class
        Solution solution = new Solution(); 
        
        // Function call for finding longest consecutive sequence
        int ans = solution.longestConsecutive(a); 
        
        // Output the result
        System.out.println("The longest consecutive sequence is " + ans);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
We will use two variables: cnt to store the length of the current sequence and longest to store the maximum length found.
First, place all the array elements into a set data structure to allow efficient lookups for consecutive numbers.
For each element x that can start a sequence (i.e., x - 1 does not exist in the set), we follow these steps:
Initialize cnt to 1, indicating the starting element of a new sequence.
Use the set to search for consecutive elements such as x + 1, x + 2, and so on, to determine the maximum possible length of the current sequence. Update cnt accordingly.
Compare cnt with longest and update longest to hold the maximum value: longest = max(longest, cnt).
Finally, longest will contain the length of the longest consecutive sequence found in the array.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    public int longestConsecutive(int[] nums) {
        // Get the length of the array
        int n = nums.length;

        // If the array is empty, no sequence exists
        if (n == 0) return 0;

        // Variable to store the longest sequence length found
        int longest = 1; 

        // HashSet to store unique elements for O(1) lookup
        Set<Integer> st = new HashSet<>();

        // Add all elements to the set to remove duplicates
        for (int i = 0; i < n; i++) {
            st.add(nums[i]);
        }

        /* Loop through each element in the set to find 
           the starting point of consecutive sequences */
        for (int it : st) {
            // If there is no number before 'it', it’s the start of a sequence
            if (!st.contains(it - 1)) {
                // Start the count for this sequence
                int cnt = 1; 
                // Store the current number
                int x = it; 

                // Keep checking for the next consecutive number
                while (st.contains(x + 1)) {
                    // Move to the next number in sequence
                    x = x + 1; 
                    // Increment the length of current sequence
                    cnt = cnt + 1; 
                }

                // Update the longest sequence length if needed
                longest = Math.max(longest, cnt);
            }
        }

        // Return the length of the longest sequence
        return longest;
    }

    public static void main(String[] args) {
        // Input array
        int[] a = {100, 4, 200, 1, 3, 2}; 

        // Create an instance of Solution class
        Solution solution = new Solution(); 
        
        // Call the function to get the longest consecutive sequence length
        int ans = solution.longestConsecutive(a); 
        
        // Print the result
        System.out.println("The longest consecutive sequence is " + ans); 
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q25
# Set Matrix Zero

## 🔹 Problem Summary
Problem Statement: Given a matrix if an element in the matrix is 0 then you will have to set its entire column and row to 0 and then return the matrix..

**Examples:**
Examples

Input: matrix=[[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
Explanation: Since matrix[2][2]=0.Therfore the 2nd column and 2nd row wil be set to 0.

Input: matrix=[[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output:[[0,0,0,0],[0,4,5,0],[0,3,1,0]]
Explanation:Since matrix[0][0]=0 and matrix[0][3]=0. Therefore 1st row, 1st column and 4th column will be set to 0

---

## 🔹 Key Observations & Intuition
* Instead of using separate arrays, we use the first row and first column of the matrix itself to store whether a row or column needs to be zeroed. We also store two flags:
* firstRowZero:Was the first row supposed to be all zero?
* firstColZero:Was the first column supposed to be all zero?
* Then:
* First pass: Mark zeros in the first row and column for any zero found in the rest of the matrix.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute force Approach)**

**Idea:**
Think of the matrix as a chessboard. If you see a zero somewhere, you need to wipe out its whole row and column to zero. In brute force, the moment you find a zero, you immediately mark its entire row and column. But here’s the trap if you set them to zero immediately, we might mess up future checks because a newly placed zero could cause extra unwanted zeroing. To avoid that, we use a special marker value (like -1 or something that can’t exist in the input) to mark places where zeros should be placed later. Once the scanning is done, we do a second pass and replace all markers with 0.
Traverse the entire matrix.
If an element is zero:
Mark all elements in its row (except already zero) as -1.
Mark all elements in its column (except already zero) as -1.
Once the full traversal is complete, replace all -1 with 0.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to set entire row and column to 0 if an element in the matrix is 0
    public void setZeroes(int[][] matrix) {
        // Get number of rows
        int m = matrix.length;
        // Get number of columns
        int n = matrix[0].length;

        // First pass: mark rows and columns
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // If the cell is zero
                if (matrix[i][j] == 0) {
                    // Mark entire row as -1 (except zeros)
                    for (int col = 0; col < n; col++) {
                        if (matrix[i][col] != 0)
                            matrix[i][col] = -1;
                    }
                    // Mark entire column as -1 (except zeros)
                    for (int row = 0; row < m; row++) {
                        if (matrix[row][j] != 0)
                            matrix[row][j] = -1;
                    }
                }
            }
        }

        // Second pass: replace -1 with 0
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == -1)
                    matrix[i][j] = 0;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Example matrix
        int[][] matrix = {{1,1,1},{1,0,1},{1,1,1}};
        
        // Create Solution object
        Solution sol = new Solution();
        // Modify matrix
        sol.setZeroes(matrix);
        
        // Print result
        for (int[] row : matrix) {
            for (int val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Instead of marking directly in the matrix, keep two extra arrays:
One to track which rows need to be zeroed.
One to track which columns need to be zeroed.
When you find a zero, mark its row index in the row array and column index in the col array. After the scan, you go back and zero out all marked rows and columns. This avoids accidental over-zeroing in the first pass.
Create a row array of size m (rows) and a col array of size n (columns) initialized to false.
First pass: Traverse the matrix, and when you find a zero:
Mark the corresponding row index in row array.
Mark the corresponding col index in col array.
Second pass: Traverse the matrix again, and if either the row or col is marked, set the cell to zero.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to set entire row and column to 0 if an element in the matrix is 0
    public void setZeroes(int[][] matrix) {
        // Get number of rows
        int m = matrix.length;
        // Get number of columns
        int n = matrix[0].length;

        // Create row marker array
        boolean[] row = new boolean[m];
        // Create column marker array
        boolean[] col = new boolean[n];

        // First pass: mark rows and columns that need to be zeroed
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // If element is zero, mark its row and column
                if (matrix[i][j] == 0) {
                    row[i] = true;
                    col[j] = true;
                }
            }
        }

        // Second pass: set cells to zero based on markers
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // If the row or column is marked, set cell to zero
                if (row[i] || col[j]) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // Create the matrix
        int[][] matrix = {{1,1,1},{1,0,1},{1,1,1}};
        
        // Create Solution object
        Solution obj = new Solution();
        // Call function
        obj.setZeroes(matrix);
        
        // Print the updated matrix
        for (int[] row : matrix) {
            for (int val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Instead of using separate arrays, we use the first row and first column of the matrix itself to store whether a row or column needs to be zeroed. We also store two flags:
firstRowZero:Was the first row supposed to be all zero?
firstColZero:Was the first column supposed to be all zero?
Then:
First pass: Mark zeros in the first row and column for any zero found in the rest of the matrix.
Second pass: Use those markers to set rows and columns to zero.
Finally, handle the first row and column separately based on the flags. This is super space-efficient because we’re reusing the input matrix itself to store markers.
Check if the first row has any zero and store in a boolean flag.
Check if the first column has any zero and store in a boolean flag.
Traverse the rest of the matrix:
If a cell is zero, mark its row in the first column and its column in the first row as zero.
Traverse again (excluding first row and column), setting cells to zero if their row marker or column marker is zero.
Finally, update the first row and first column based on the stored flags.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import.java.util.*;
class Solution {
    // Function to set entire row and column to 0 if an element in the matrix 
    public void setZeroes(int[][] matrix) {
        // Get dimensions of matrix
        int m = matrix.length;
        int n = matrix[0].length;

        // Flag to track if first row should be zeroed
        boolean firstRowZero = false;
        // Flag to track if first column should be zeroed
        boolean firstColZero = false;

        // Check if first row has any zero
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Check if first column has any zero
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Use first row/column as markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        // Set cells to zero based on markers
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Zero the first row if needed
        if (firstRowZero) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }

        // Zero the first column if needed
        if (firstColZero) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}

// Main class to run the program
public class Main {
    public static void main(String[] args) {
        Solution obj = new Solution();
        int[][] matrix = {{0,1,2,0},{3,4,5,2},{1,3,1,5}};
        obj.setZeroes(matrix);
        for (int[] row : matrix) {
            for (int val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q26
# Rotate Image by 90 degree

## 🔹 Problem Summary
Problem Statement: Given an N * N 2D integer matrix, rotate the matrix by 90 degrees clockwise. The rotation must be done in place, meaning the input 2D matrix must be modified directly..

**Examples:**
Examples

Input :matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
            

Output :
matrix = [[7, 4, 1], [8, 5, 2], [9, 6, 3]]


Explanation :
First, we transpose the matrix: rows become columns. Then, we reverse each row to simulate 90° clockwise rotation. So element at (0,0) goes to (0,2), (0,1) goes to (1,2), and so on, achieving the rotated layout.


Input :
matrix = [[0, 1, 1, 2], [2, 0, 3, 1], [4, 5, 0, 5], [5, 6, 7, 0]]


Output :
matrix = [[5, 4, 2, 0], [6, 5, 0, 1], [7, 0, 3, 1], [0, 5, 1, 2]]


Explanation :
First, the matrix is transposed: rows become columns. Then, each row is reversed. This moves the last column to the first row, the second last column to the second row, and so on. The original position of each element is rotated 90° clockwise into its new location.

---

## 🔹 Key Observations & Intuition
* To rotate a matrix 90 degrees clockwise in-place (without using extra space), we use two key matrix operations:
* Step 1: Transpose the matrix: swap elements across the diagonal. This converts rows into columns.
* Step 2: Reverse each row: this turns the new columns into the final rotated rows.
* This works because:
* Transposing moves elements from (i, j) to (j, i), effectively rotating across the diagonal.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
In a 90-degree clockwise rotation, each element in the matrix moves from its original position to a new position based on a specific pattern. The first column becomes the first row (in reverse order) and second column becomes the second row, and so on.
We can simulate this movement by using a new matrix. For each element at position (i, j) in the original matrix, we calculate its new position in the rotated matrix as (j, n - i - 1) where n is the size of the matrix.
Initialize an empty matrix of the same size (n x n).
Loop through every element of the original matrix using two nested loops.
For each element at position (i, j), place it in the new matrix at position (j, n - i - 1).
After completing the placement for all elements, return or copy the new matrix.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import.java.util.*;
class Solution {
    // Function to rotate the matrix 90 degrees clockwise using extra space
    public int[][] rotateClockwise(int[][] matrix) {
        // Get the size of the square matrix
        int n = matrix.length;

        // Create a new matrix of same size to store rotated result
        int[][] rotated = new int[n][n];

        // Traverse each element of original matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                // Place the element at its new rotated position
                rotated[j][n - i - 1] = matrix[i][j];
            }
        }

        // Return the rotated matrix
        return rotated;
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        int[][] mat = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        Solution obj = new Solution();
        int[][] rotated = obj.rotateClockwise(mat);

        // Print the rotated matrix
        for (int[] row : rotated) {
            for (int val : row)
                System.out.print(val + " ");
            System.out.println();
        }
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
To rotate a matrix 90 degrees clockwise in-place (without using extra space), we use two key matrix operations:
Step 1: Transpose the matrix: swap elements across the diagonal. This converts rows into columns.
Step 2: Reverse each row: this turns the new columns into the final rotated rows.

This works because:
Transposing moves elements from (i, j) to (j, i), effectively rotating across the diagonal.
Reversing the rows repositions the elements in each row, finalizing the clockwise rotation.
Get the size of the square matrix (number of rows or columns).
Start the first phase: Transpose the matrix
For each row starting from the top to bottom:
For each column starting from the diagonal element (excluding already visited elements):
Swap the current element with the element that is diagonally opposite across the main diagonal.
This effectively flips the matrix over its top-left to bottom-right diagonal, converting rows into columns.
Move to the second phase: Reverse each row
For every row in the matrix:
Reverse the order of the elements in that row (first element becomes last, second becomes second last, and so on).
This realigns the columns to their correct position for the clockwise rotation.
Once both phases are done, the matrix will have been rotated 90 degrees clockwise in-place.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import.java.util.*;
class Solution {
    // Function to rotate matrix 90 degrees clockwise in-place
    public void rotateClockwise(int[][] matrix) {
        int n = matrix.length;

        // Step 1: Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                // Swap element at (i, j) with (j, i)
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; i++) {
            int left = 0, right = n - 1;

            // Swap elements from both ends moving toward center
            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
    }
}

// Driver class
class Main {
    public static void main(String[] args) {
        int[][] matrix = {
            {1, 2, 3},
            {4, 5, 6},
            {7, 8, 9}
        };

        Solution obj = new Solution();
        obj.rotateClockwise(matrix);

        // Print rotated matrix
        for (int[] row : matrix) {
            for (int val : row)
                System.out.print(val + " ");
            System.out.println();
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q27
# Spiral Traversal of Matrix

## 🔹 Problem Summary
Problem Statement: Given a Matrix, print the given matrix in spiral order.

**Examples:**
Examples

Input: Matrix[][] = { { 1, 2, 3, 4 },{ 5, 6, 7, 8 },{ 9, 10, 11, 12 },{ 13, 14, 15, 16 } }
Outhput: 1, 2, 3, 4, 8, 12, 16, 15, 14, 13, 9, 5, 6, 7, 11, 10.
Explanation: The output of matrix in spiral form.

Input: Matrix[][] = { { 1, 2, 3 }, { 4, 5, 6 },{ 7, 8, 9 } }
Output: 1, 2, 3, 6, 9, 8, 7, 4, 5.
Explanation: The output of matrix in spiral form.

---

## 🔹 Key Observations & Intuition
* The brute force method simulates movement in four directions: right, down, left, and up while keeping track of which cells have already been visited using a separate matrix. This approach ensures that we never revisit any element and always stay within bounds. After moving in one direction as far as possible, we rotate the direction and keep repeating until all elements are visited.
* Initialize a 2D boolean matrix `visited` of same size as input to keep track of visited cells.
* Define direction arrays for right, down, left, and up movements.
* Start at (0, 0), and begin with direction = 0 (right).
* For each of the total elements in the matrix:

---

## 🔹 Approaches

### ➤ Brute Force
**(Approach)**

**Idea:**
The brute force method simulates movement in four directions: right, down, left, and up while keeping track of which cells have already been visited using a separate matrix. This approach ensures that we never revisit any element and always stay within bounds. After moving in one direction as far as possible, we rotate the direction and keep repeating until all elements are visited.
Initialize a 2D boolean matrix `visited` of same size as input to keep track of visited cells.
Define direction arrays for right, down, left, and up movements.
Start at (0, 0), and begin with direction = 0 (right).
For each of the total elements in the matrix:
Add the current cell to result and mark it as visited.
Check if the next cell in the current direction is valid and not visited.
If valid, move to it; else rotate the direction and try the new direction.
Repeat this for total number of cells in the matrix.

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to return matrix in spiral order
    public List spiralOrder(int[][] matrix) {
        // Result list to store the spiral order
        List result = new ArrayList<>();

        // Initialize boundaries
        int top = 0;                        // Starting row
        int bottom = matrix.length - 1;     // Ending row
        int left = 0;                       // Starting column
        int right = matrix[0].length - 1;   // Ending column

        // Loop until all elements are traversed
        while (top <= bottom && left <= right) {

            // Traverse the top row from left to right
            for (int i = left; i <= right; i++) {
                result.add(matrix[top][i]);
            }
            top++; // Move the top boundary downward

            // Traverse the right column from top to bottom
            for (int i = top; i <= bottom; i++) {
                result.add(matrix[i][right]);
            }
            right--; // Move the right boundary leftward

            // Traverse the bottom row from right to left (only if rows remain)
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    result.add(matrix[bottom][i]);
                }
                bottom--; // Move the bottom boundary upward
            }

            // Traverse the left column from bottom to top (only if columns remain)
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    result.add(matrix[i][left]);
                }
                left++; // Move the left boundary rightward
            }
        }

        // Return the spiral order result
        return result;
    }
}

// Driver code
class Main {
    public static void main(String[] args) {
        Solution obj = new Solution();

        // Input matrix
        int[][] matrix = {
            { 1,  2,  3,  4 },
            { 5,  6,  7,  8 },
            { 9, 10, 11, 12 },
            { 13,14, 15, 16 }
        };

        // Call spiralOrder function
        List ans = obj.spiralOrder(matrix);

        // Print result
        System.out.println(ans);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Approach** | Refer to approach details | Refer to approach details |

---

---
Q28
# Count Subarray sum Equals K

## 🔹 Problem Summary
Problem Statement: Given an array of integers and an integer k, return the total number of subarrays whose sum equals k. A subarray is a contiguous non-empty sequence of elements within an array.

**Examples:**
Examples

Input : N = 4, array[] = {3, 1, 2, 4}, k = 6
Output: 2
Explanation: The subarrays that sum up to 6 are [3, 1, 2] and [2, 4].

Input: N = 3, array[] = {1,2,3}, k = 3
Output: 2
Explanation: The subarrays that sum up to 3 are [1, 2], and [3].

---

## 🔹 Key Observations & Intuition
* If we carefully observe, we can notice that to get the sum of the current subarray we just need to add the current element(i.e. arr[j]) to the sum of the previous subarray i.e. arr[i….j-1]. Assume previous subarray = arr[i……j-1]
* current subarray = arr[i…..j]
* Sum of arr[i….j] = (sum of arr[i….j-1]) + arr[j] This is how we can remove the third loop and while moving j pointer, we can calculate the sum.
* First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = array size).
* Inside the loop, we will run another loop(say j) that will signify the ending index as well as the current element of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute force Approach)**

**Idea:**
We will check the sum of every possible subarray and count how many of them are equal to k. To get every possible subarray sum, we will be using three nested loops. The first two loops(say i and j) will iterate over every possible starting index and ending index of a subarray. Basically, in each iteration, the subarray range will be from index i to index j. Using another loop we will get the sum of the elements of the subarray [i…..j]. Among all values of the sum calculated, we will only consider those that are equal to k.

Note: We are selecting every possible subarray using two nested loops and for each of them, we add all its elements using another loop.

First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = size of the array).
Inside the loop, we will run another loop(say j) that will signify the ending index of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
After that for each subarray starting from index i and ending at index j (i.e. arr[i….j]), we will run another loop to calculate the sum of all the elements(of that particular subarray).
After calculating the sum, we will check if the sum is equal to the given k. If it is, we will increase the value of the count.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import.java.util.*;
class Solution {
    // Function to find count of subarrays with sum equal to k
    public int subarraySum(int[] arr, int k) {
        // Size of the array
        int n = arr.length;

        // Initialize count of subarrays
        int count = 0;

        // Traverse all possible start indices
        for (int i = 0; i < n; i++) {
            // Traverse all possible end indices from start
            for (int j = i; j < n; j++) {
                // Initialize sum for current subarray
                int sum = 0;

                // Calculate sum of subarray from i to j
                for (int m = i; m <= j; m++) {
                    sum += arr[m];
                }

                // If sum equals k, increment count
                if (sum == k) {
                    count++;
                }
            }
        }

        // Return total count of subarrays
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        // Input array
        int[] arr = {3, 1, 2, 4};

        // Target sum
        int k = 6;

        // Create Solution object
        Solution sol = new Solution();

        // Call function and store result
        int result = sol.subarraySum(arr, k);

        // Print the count of subarrays
        System.out.println("The number of subarrays is: " + result);
    }
}
```

---

### ➤ Optimal Approach
**(Better Approach)**

**Idea:**
If we carefully observe, we can notice that to get the sum of the current subarray we just need to add the current element(i.e. arr[j]) to the sum of the previous subarray i.e. arr[i….j-1]. Assume previous subarray = arr[i……j-1]
current subarray = arr[i…..j]
Sum of arr[i….j] = (sum of arr[i….j-1]) + arr[j] This is how we can remove the third loop and while moving j pointer, we can calculate the sum.
First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = array size).
Inside the loop, we will run another loop(say j) that will signify the ending index as well as the current element of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
Inside loop j, we will add the current element to the sum of the previous subarray i.e. sum = sum + arr[j]. 
After calculating the sum, we will check if the sum is equal to the given k. If it is, we will increase the value of the count.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import.java.util.*;
class Solution {
    // Function to find count of subarrays with sum equal to k
    public int subarraySum(int[] arr, int k) {
        // Size of the array
        int n = arr.length;

        // Initialize count of subarrays
        int count = 0;

        // Traverse all possible start indices
        for (int i = 0; i < n; i++) {
            // Initialize sum for current subarray
            int sum = 0;

            // Traverse all possible end indices from start
            for (int j = i; j < n; j++) {
                // Add current element to sum
                sum += arr[j];

                // If sum equals k, increment count
                if (sum == k) {
                    count++;
                }
            }
        }

        // Return total count of subarrays
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        // Input array
        int[] arr = {3, 1, 2, 4};

        // Target sum
        int k = 6;

        // Create Solution object
        Solution sol = new Solution();

        // Call function and store result
        int result = sol.subarraySum(arr, k);

        // Print the count of subarrays
        System.out.println("The number of subarrays is: " + result);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N \log N)$ or $O(N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |

---


# ═══════════════════════════════════════
# Hard Problems
# ═══════════════════════════════════════

---
Q29
# Program to generate Pascal's Triangle

## 🔹 Problem Summary
Problem Statement: Write a program to generate Pascal's triangle. In Pascal’s triangle, each number is the sum of the two numbers directly above it as shown in the figure below:

**Examples:**
Examples
Input: N = 5, r = 5, c = 3 
Output: Element at position (r, c): 6
N-th row of Pascal’s triangle: 1 4 6 4 1
First n rows of Pascal’s triangle:
1 
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1  
Explanation: Pascal triangle for first 5 rows is shown above.

Input: N = 1, r = 1, c = 1
Output: Element at position (r, c): 1
N-th row of Pascal’s triangle: 1
First n rows of Pascal’s triangle:
1  
Explanation: N = 1 is the base case fof a pascal's triangle.

---

## 🔹 Key Observations & Intuition
* To find the element at the coordinates (R,C) where R is the row number and C is the Column number, we can simply simulate the generation of pascal's triangle for R rows. In Pascal’s Triangle, the element at row R and column C corresponds to the binomial coefficient (r-1)C(c-1). To calculate this binomial coefficient, we can simply apply the formula of binomial coefficient i.e. (r-1)!/(c-1)!(r-c)!.
* Instead of computing full factorials (which can overflow and be slow), we can multiply and divide in a loop to compute the coefficient efficiently.

---

## 🔹 Approaches

### ➤ Brute Force
**(Approach - 1)**

**Idea:**
To generate the entire Pascal’s Triangle for the first N rows, we can start with the first row containing a single 1 and iteratively build each subsequent row using the property that every element (except the first and last) is the sum of the two elements directly above it from the previous row. The first and last elements of each row are always 1. By storing the previous row, we can calculate the next row easily. This process continues until we have constructed all N rows, resulting in the complete Pascal’s Triangle structure.

**Java Code:**
```java
import java.util.*;

// Class containing Pascal's Triangle generation logic
class Solution {
    // Function to generate Pascal's Triangle up to numRows
    public List<List<Integer>> generate(int numRows) {
        // Result list to hold all rows
        List<List<Integer>> triangle = new ArrayList<>();

        // Loop for each row
        for (int i = 0; i < numRows; i++) {
            // Create a row with size (i+1)
            List<Integer> row = new ArrayList<>(Collections.nCopies(i + 1, 1));

            // Fill elements from index 1 to i-1 (middle values)
            for (int j = 1; j < i; j++) {
                // Each element = sum of two elements above it
                row.set(j, triangle.get(i - 1).get(j - 1) +
                           triangle.get(i - 1).get(j));
            }

            // Add current row to the triangle
            triangle.add(row);
        }
        return triangle;
    }
}

public class Main {
    public static void main(String[] args) {
        Solution obj = new Solution();
        int n = 5;

        // Generate and print Pascal's Triangle
        List<List<Integer>> result = obj.generate(n);
        for (List<Integer> row : result) {
            for (Integer val : row) System.out.print(val + " ");
            System.out.println();
        }
    }
}
```

---

### ➤ Better Approach
**(Approach - 2)**

**Idea:**
To print the Nth row of the pascal triangle we can take advantage of the relationship between Nth element and binomial coefficients.

In a pascal's triangle, the Nth row contains the binomial coefficients C(N-1, 0), C(N-1, 1) and so on till C(N-1, N-1). Thus we can simply calculate all these values to return the Nth row of pascal triangle.

Instead of computing full factorials, we can start with the first value as 1, and use the relation C(n, k) = C(n, k−1) × (n−k+1) / k to compute the next value from the previous one in constant time.

**Java Code:**
```java
import java.util.*;

// Class containing Pascal's Triangle row generation logic
class Solution {
    // Function to generate the Nth row of Pascal's Triangle
    public List<Long> getNthRow(int N) {
        // Result list to store the row
        List<Long> row = new ArrayList<>();
        
        // First value of the row is always 1
        long val = 1;
        row.add(val);
        
        // Compute remaining values using the relation:
        // C(n, k) = C(n, k-1) * (n-k) / k
        for (int k = 1; k < N; k++) {
            val = val * (N - k) / k;
            row.add(val);
        }
        
        return row;
    }
}

public class Main {
    public static void main(String[] args) {
        int N = 5; // Example: 5th row
        Solution sol = new Solution();
        List<Long> result = sol.getNthRow(N);

        // Print the row
        for (long num : result) {
            System.out.print(num + " ");
        }
    }
}
```

---

### ➤ Optimal Approach
**(Approach - 3)**

**Idea:**
To find the element at the coordinates (R,C) where R is the row number and C is the Column number, we can simply simulate the generation of pascal's triangle for R rows. In Pascal’s Triangle, the element at row R and column C corresponds to the binomial coefficient (r-1)C(c-1). To calculate this binomial coefficient, we can simply apply the formula of binomial coefficient i.e. (r-1)!/(c-1)!(r-c)!.

Instead of computing full factorials (which can overflow and be slow), we can multiply and divide in a loop to compute the coefficient efficiently.

**Java Code:**
```java
// Solution class to find the (r, c) element of Pascal's Triangle
class Solution {
    // Function to compute binomial coefficient (nCr)
    public long findPascalElement(int r, int c) {
        // Element is C(r-1, c-1)
        int n = r - 1;
        int k = c - 1;

        long result = 1;

        // Compute C(n, k) using iterative formula
        for (int i = 0; i < k; i++) {
            result *= (n - i);
            result /= (i + 1);
        }

        return result;
    }
}

// Main class to test the solution
public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int r = 5, c = 3;
        System.out.println(sol.findPascalElement(r, c));
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Approach - 1** | Refer to approach details | Refer to approach details |
| **Approach - 2** | Refer to approach details | Refer to approach details |
| **Approach - 3** | Refer to approach details | Refer to approach details |

---

---
Q30
# Majority Elements(>N/3 times) | Find the elements that appears more than N/3 times in the array

## 🔹 Problem Summary
Problem Statement: Given an integer array nums of size n. Return all elements which appear more than n/3 times in the array. The output can be returned in any order.

**Examples:**
Examples
Example 1:
Input:
 nums = [1, 2, 1, 1, 3, 2]  

Output:
 [1]  

Explanation:
 Here, n / 3 = 6 / 3 = 2.  
Therefore, the elements appearing 3 or more times are: [1].


Example 2:
Input:
 nums = [1, 2, 1, 1, 3, 2, 2]  

Output:
 [1, 2]  

Explanation:
 Here, n / 3 = 7 / 3 = 2.  
Therefore, the elements appearing 3 or more times are: [1, 2].

---

## 🔹 Key Observations & Intuition
* Initialize four variables: cnt1 and cnt2 for tracking the counts of elements, and el1 and el2 for storing the potential majority elements.
* Traverse through the given array:
* If cnt1 is 0 and the current element is not equal to el2, set el1 to the current element and increment cnt1 by 1.
* If cnt2 is 0 and the current element is not equal to el1, set el2 to the current element and increment cnt2 by 1.
* If the current element is equal to el1, increment cnt1 by 1.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Can there be more than 2 majority elements?
To understand why there can't be more than two majority elements (elements that appear more than n/3 times) in an array of size n, let's consider the following reasoning:
A majority element must appear more than n/3 times. Let’s assume there are more than two majority elements, say A, B, and C.
The combined frequency of these three elements would be: frequency of A + frequency of B + frequency of C > n/3 + n/3 + n/3 = n.
Since the total occurrences of all elements cannot exceed n (the size of the array), the combined frequency of any three elements each appearing more than n/3 times would exceed the total size of the array, leading to a contradiction.
Therefore, it is mathematically impossible to have more than two elements that each appear more than n/3 times in the array.
Approach:
Iterate through the array and select each element one by one.
For each unique element, run another loop to count its occurrences in the array.
If any element occurs more than floor(N/3) times, include it in the result array.
If a previously included element is found during traversal, skip it to avoid counting duplicates.
If the result array already contains 2 elements, break out of the loop, as there can’t be more than two majority elements.
Return the result array containing the majority elements or return -1 if no such element is found.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Solution {
    // Function to find majority elements in an array
    public List<Integer> majorityElementTwo(int[] nums) {
        int n = nums.length;
        List<Integer> result = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            // Check if nums[i] is not already part of the result
            if (result.size() == 0 || result.get(0) != nums[i] && (result.size() < 2 || result.get(1) != nums[i])) {
                int count = 0;
                for (int j = 0; j < n; j++) {
                    if (nums[j] == nums[i]) {
                        count++;
                    }
                }
                if (count > n / 3) {
                    result.add(nums[i]);
                }
            }

            if (result.size() == 2) {
                break;
            }
        }

        return result;
    }

    // Main method
    public static void main(String[] args) {
        int[] arr = {11, 33, 33, 11, 33, 11};

        Solution sol = new Solution();
        List<Integer> ans = sol.majorityElementTwo(arr);

        System.out.print("The majority elements are: ");
        for (int it : ans) {
            System.out.print(it + " ");
        }
        System.out.println();
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Use a hashmap (or a frequency array if the array size is small) to store the elements as key-value pairs, where the key is the element and the value is the number of times it occurs in the array.
Traverse the entire array, updating the occurrences of each element in the hashmap.
After the traversal, check the hashmap to see if any element's value (frequency) is greater than the floor of N/3. If it is, include the element in the answer array.
If the size of the answer array reaches 2, break out of the loop, as there cannot be more than two majority elements.
Finally, return the answer array containing the majority elements. If no such elements are found, return -1.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find majority elements in an array
    public List<Integer> majorityElementTwo(int[] nums) {
        int n = nums.length;
        List<Integer> result = new ArrayList<>();
        Map<Integer, Integer> mpp = new HashMap<>();
        int mini = n / 3 + 1;

        for (int i = 0; i < n; i++) {
            mpp.put(nums[i], mpp.getOrDefault(nums[i], 0) + 1);

            // Add to result only when the count just reaches mini
            if (mpp.get(nums[i]) == mini) {
                result.add(nums[i]);
            }

            if (result.size() == 2) break;
        }

        return result;
    }
}

// Separate main class
public class Main {
    public static void main(String[] args) {
        int[] arr = {11, 33, 33, 11, 33, 11};

        Solution sol = new Solution();
        List<Integer> ans = sol.majorityElementTwo(arr);

        System.out.print("The majority elements are: ");
        for (int it : ans) {
            System.out.print(it + " ");
        }
        System.out.println();
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Initialize four variables: cnt1 and cnt2 for tracking the counts of elements, and el1 and el2 for storing the potential majority elements.
Traverse through the given array:
If cnt1 is 0 and the current element is not equal to el2, set el1 to the current element and increment cnt1 by 1.
If cnt2 is 0 and the current element is not equal to el1, set el2 to the current element and increment cnt2 by 1.
If the current element is equal to el1, increment cnt1 by 1.
If the current element is equal to el2, increment cnt2 by 1.
In all other cases, decrease cnt1 and cnt2 by 1.
After processing all elements, el1 and el2 should be the candidate elements for majority. To confirm:
Use another loop to manually check the counts of el1 and el2 in the array.
If either el1 or el2's count is greater than floor(N/3), it is considered a valid majority element.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find majority elements in an array
    public List<Integer> majorityElementTwo(int[] nums) {
        int n = nums.length;
        int cnt1 = 0, cnt2 = 0;
        int el1 = Integer.MIN_VALUE, el2 = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++) {
            if (cnt1 == 0 && el2 != nums[i]) {
                cnt1 = 1;
                el1 = nums[i]; 
            } else if (cnt2 == 0 && el1 != nums[i]) {
                cnt2 = 1;
                el2 = nums[i]; 
            } else if (nums[i] == el1) {
                cnt1++;
            } else if (nums[i] == el2) {
                cnt2++; 
            } else {
                cnt1--; 
                cnt2--;
            }
        }

        cnt1 = 0; cnt2 = 0; 
        for (int i = 0; i < n; i++) {
            if (nums[i] == el1) cnt1++; 
            if (nums[i] == el2) cnt2++;
        }

        int mini = n / 3 + 1;
        List<Integer> result = new ArrayList<>(); 
        if (cnt1 >= mini) result.add(el1);
        if (cnt2 >= mini && el1 != el2) result.add(el2);

        return result;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr = {11, 33, 33, 11, 33, 11};

        Solution sol = new Solution();
        List<Integer> ans = sol.majorityElementTwo(arr);

        System.out.print("The majority elements are: ");
        for (int it : ans) {
            System.out.print(it + " ");
        }
        System.out.println();
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q31
# 3 Sum : Find all Triplets that add up to a given sum

## 🔹 Problem Summary
Problem Statement: Given an array of N integers, your task is to find unique triplets that add up to give a sum of zero. In short, you need to return an array of all the unique triplets [arr[a], arr[b], arr[c]] such that i!=j, j!=k, k!=i, and their sum is equal to zero.

**Examples:**
Examples

Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: Out of all possible unique triplets possible, [-1,-1,2] and [-1,0,1] are the two unique triplets whose sum is equal to zero. Notice the second element in the first triplet and the first element in the second triplet is the same i.e. -1, but they refer to different indices.

Example 2:
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only unique triplet whose sum is zero is [0,0,0].

---

## 🔹 Key Observations & Intuition
* The optimal approach uses sorting and the two-pointer technique. First, we sort the array. Then for each element, we use two pointers (left and right) to find pairs that sum to the negation of the current element.
* Sort the entire array.
* Use a loop to fix the first element (i). Skip duplicates for i.
* For each i, set left = i+1 and right = n-1.
* Calculate sum = arr[i] + arr[left] + arr[right].

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
The naive approach is to explore all possible triplets using three nested loops. For each triplet, check if the sum equals zero. To avoid duplicate triplets, we sort each triplet and use a set.

We will use three loops to pick three elements from the array.
For every triplet, we check if the sum is equal to zero.
If the sum is zero, we sort the triplet and insert it into a set to avoid duplicates.
Finally, we convert the set to a list and return it.

**Complexity:**
* **Time Complexity:** O(N^3 * log(no. of unique triplets)), Space Complexity: O(2 * no. of unique triplets) for the set
* **Space Complexity:** O(2 * no. of unique triplets) for the set

**Java Code:**
```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        // Set to store unique triplets
        Set<List<Integer>> tripletSet = new HashSet<>();

        // Three nested loops to explore all triplets
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    // Check if the triplet sums to zero
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        // Sort the triplet to handle duplicates
                        List<Integer> triplet = Arrays.asList(nums[i], nums[j], nums[k]);
                        Collections.sort(triplet);
                        tripletSet.add(triplet);
                    }
                }
            }
        }

        // Convert set to list and return
        return new ArrayList<>(tripletSet);
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = sol.threeSum(nums);
        System.out.println(result);
    }
}
```

---

### ➤ Better Approach
**(Better Approach (Hashing))**

**Idea:**
We can improve upon the brute force by using a HashSet to find the third element. For each pair (i, j), the third element needed is -(arr[i] + arr[j]). We search for this in a HashSet.

We will fix the first element using a loop (i).
For the remaining elements, we use a HashSet. For each element at index j, we calculate the third element needed as -(arr[i] + arr[j]).
If the third element exists in the HashSet, we have found a triplet. We sort and add it to our result set.
Otherwise, we add arr[j] to the HashSet.
Between the loops, we use a set of sorted lists to handle duplicates.

**Complexity:**
* **Time Complexity:** O(N^2 * log(no. of unique triplets)), Space Complexity: O(N) + O(2 * no. of unique triplets)
* **Space Complexity:** O(N) + O(2 * no. of unique triplets)

**Java Code:**
```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        // Set to store unique triplets
        Set<List<Integer>> tripletSet = new HashSet<>();

        for (int i = 0; i < n; i++) {
            // HashSet to find the third element
            Set<Integer> hashSet = new HashSet<>();
            for (int j = i + 1; j < n; j++) {
                // Calculate the third element needed
                int third = -(nums[i] + nums[j]);
                // If third element exists in set, we found a triplet
                if (hashSet.contains(third)) {
                    List<Integer> triplet = Arrays.asList(nums[i], nums[j], third);
                    Collections.sort(triplet);
                    tripletSet.add(triplet);
                }
                // Add current element to set
                hashSet.add(nums[j]);
            }
        }

        return new ArrayList<>(tripletSet);
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = sol.threeSum(nums);
        System.out.println(result);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach (Two Pointer))**

**Idea:**
The optimal approach uses sorting and the two-pointer technique. First, we sort the array. Then for each element, we use two pointers (left and right) to find pairs that sum to the negation of the current element.

Sort the entire array.
Use a loop to fix the first element (i). Skip duplicates for i.
For each i, set left = i+1 and right = n-1.
Calculate sum = arr[i] + arr[left] + arr[right].
If sum < 0, increment left. If sum > 0, decrement right.
If sum == 0, add the triplet to result, then skip duplicates for both left and right pointers.
Repeat until left < right.

**Complexity:**
* **Time Complexity:** O(N log N) + O(N^2) ≈ O(N^2), Space Complexity: O(no. of triplets) for the answer list only
* **Space Complexity:** O(no. of triplets) for the answer list only

**Java Code:**
```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        int n = nums.length;

        // Sort the array to use two-pointer technique
        Arrays.sort(nums);

        for (int i = 0; i < n; i++) {
            // Skip duplicate elements for the first position
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            // Two pointers
            int left = i + 1;
            int right = n - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum < 0) {
                    // Sum is too small, move left pointer right
                    left++;
                } else if (sum > 0) {
                    // Sum is too large, move right pointer left
                    right--;
                } else {
                    // Found a valid triplet
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left++;
                    right--;

                    // Skip duplicate elements for the second position
                    while (left < right && nums[left] == nums[left - 1]) left++;
                    // Skip duplicate elements for the third position
                    while (left < right && nums[right] == nums[right + 1]) right--;
                }
            }
        }

        return result;
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {-1, 0, 1, 2, -1, -4};
        List<List<Integer>> result = sol.threeSum(nums);

        // Print all triplets
        for (List<Integer> triplet : result) {
            System.out.println(triplet);
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **O(N log N) + O(N^2) ≈ O(N^2), Space Complexity: O(no. of triplets) for the answer list only** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | O(N^3 * log(no. of unique triplets)), Space Complexity: O(2 * no. of unique triplets) for the set | O(2 * no. of unique triplets) for the set |
| **Better Approach (Hashing)** | O(N^2 * log(no. of unique triplets)), Space Complexity: O(N) + O(2 * no. of unique triplets) | O(N) + O(2 * no. of unique triplets) |
| **Optimal Approach (Two Pointer)** | O(N log N) + O(N^2) ≈ O(N^2), Space Complexity: O(no. of triplets) for the answer list only | O(no. of triplets) for the answer list only |

---

---
Q32
# 4 Sum | Find Quads that add up to a target value

## 🔹 Problem Summary
Problem Statement: Given an array of N integers, your task is to find unique quads that add up to give a target value. In short, you need to return an array of all the unique quadruplets [arr[a], arr[b], arr[c], arr[d]] such that their sum is equal to a given target.

**Examples:**
Examples
Example 1:
Input Format:arr[] = [1,0,-1,0,-2,2], target = 0
Result: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
Explanation:We have to find unique quadruplets from the array such that the sum of those elements is equal to the target sum given that is 0. The result obtained is such that the sum of the quadruplets yields 0.

Example 2:
Input Format: arr[] = [4,3,3,4,4,2,1,2,1,1], target = 9
Result: [[1,1,3,4],[1,2,2,4],[1,2,3,3]]
Explanation: The sum of all the quadruplets is equal to the target i.e. 9.

---

## 🔹 Key Observations & Intuition
* Sort the array first.
* Use the first loop to pick the first number. Skip it if it is the same as the previous one to avoid duplicates.
* Inside it, use the second loop to pick the second number. Also skip it if it repeats the previous one.
* Set two pointers: one just after the second number (left pointer) and one at the end of the array (right pointer).
* While the left pointer is before the right pointer, calculate the total of the four chosen numbers.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
Create a set to keep only unique groups of four numbers.
Use the first loop from the start of the array to the end to choose the first number.
Inside it, run a second loop starting from the next position to choose the second number.
Then, run a third loop starting from the next position after the second number to choose the third number.
Finally, run a fourth loop starting from the next position after the third number to choose the fourth number.
Check if the total of these four numbers equals the target value.
If yes, arrange the four numbers in order and add them to the set.
Once all loops are done, return the set as a list of unique groups of four numbers.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find quadruplets with sum = target
    public List<List<Integer>> fourSum(int[] arr, int target) {
        // Get size of array
        int n = arr.length;
        // Use set to avoid duplicate quadruplets
        Set<List<Integer>> set = new HashSet<>();

        // First loop - pick first element
        for (int i = 0; i < n; i++) {
            // Second loop - pick second element
            for (int j = i + 1; j < n; j++) {
                // Third loop - pick third element
                for (int k = j + 1; k < n; k++) {
                    // Fourth loop - pick fourth element
                    for (int l = k + 1; l < n; l++) {
                        // Calculate sum of four numbers
                        long sum = (long) arr[i] + arr[j] + arr[k] + arr[l];
                        // If sum matches target
                        if (sum == target) {
                            // Create quadruplet
                            List<Integer> temp = Arrays.asList(arr[i], arr[j], arr[k], arr[l]);
                            // Sort to maintain uniqueness
                            Collections.sort(temp);
                            // Add to set
                            set.add(temp);
                        }
                    }
                }
            }
        }
        // Convert set to list and return
        return new ArrayList<>(set);
    }
}

public class Main {
    public static void main(String[] args) {
        // Input array
        int[] arr = {1, 0, -1, 0, -2, 2};
        // Target sum
        int target = 0;

        // Create object
        Solution obj = new Solution();
        // Get result
        List<List<Integer>> ans = obj.fourSum(arr, target);

        // Print result
        for (List<Integer> quad : ans) {
            System.out.println(quad);
        }
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Create a set to keep only unique groups of four numbers.
Run the first loop from the start to the end of the array to pick the first number.
Inside it, run the second loop from the next position to pick the second number.
Before starting the third loop, make a HashSet to keep track of numbers between the second and third positions.
Run the third loop from the next position after the second number to the end of the array to pick the third number.
Find the fourth number by subtracting the total of the first three numbers from the target value.
If this fourth number is already in the HashSet, arrange all four numbers in order and add them to the set.
Add the current third number to the HashSet (only numbers between the second and third loops are stored).
After all loops finish, return the set as a list of unique groups of four numbers.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find all unique quadruplets
    public List<List<Integer>> fourSum(int[] arr, int target) {
        int n = arr.length;
        Set<List<Integer>> set = new HashSet<>();

        // First loop - pick first number
        for (int i = 0; i < n; i++) {
            // Second loop - pick second number
            for (int j = i + 1; j < n; j++) {
                // HashSet for numbers between j and k
                HashSet<Integer> seen = new HashSet<>();

                // Third loop - pick third number
                for (int k = j + 1; k < n; k++) {
                    // Find required fourth number
                    long required = (long) target - arr[i] - arr[j] - arr[k];

                    // If required number already seen → valid quadruplet
                    if (seen.contains((int) required)) {
                        List<Integer> temp = Arrays.asList(arr[i], arr[j], arr[k], (int) required);
                        Collections.sort(temp);
                        set.add(temp);
                    }

                    // Add current third number into set
                    seen.add(arr[k]);
                }
            }
        }
        return new ArrayList<>(set);
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 0, -1, 0, -2, 2};
        int target = 0;

        Solution obj = new Solution();
        List<List<Integer>> ans = obj.fourSum(arr, target);

        for (List<Integer> quad : ans) {
            System.out.println(quad);
        }
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Sort the array first.
Use the first loop to pick the first number. Skip it if it is the same as the previous one to avoid duplicates.
Inside it, use the second loop to pick the second number. Also skip it if it repeats the previous one.
Set two pointers: one just after the second number (left pointer) and one at the end of the array (right pointer).
While the left pointer is before the right pointer, calculate the total of the four chosen numbers.
If the total equals the target, save the quadruplet, then move both pointers while skipping duplicate numbers.
If the total is less than the target, move the left pointer one step forward to increase the total.
If the total is greater than the target, move the right pointer one step backward to reduce the total.
After all loops finish, return the list of unique groups of four numbers.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find all unique quadruplets
    public List<List<Integer>> fourSum(int[] arr, int target) {
        int n = arr.length;
        List<List<Integer>> ans = new ArrayList<>();

        // Step 1: Sort array
        Arrays.sort(arr);

        // Step 2: First loop for first number
        for (int i = 0; i < n; i++) {
            if (i > 0 && arr[i] == arr[i - 1]) continue;

            // Step 3: Second loop for second number
            for (int j = i + 1; j < n; j++) {
                if (j > i + 1 && arr[j] == arr[j - 1]) continue;

                // Step 4: Two pointers
                int left = j + 1, right = n - 1;
                while (left < right) {
                    long sum = (long) arr[i] + arr[j] +
                               arr[left] + arr[right];

                    if (sum == target) {
                        ans.add(Arrays.asList(arr[i], arr[j],
                                              arr[left], arr[right]));

                        while (left < right && arr[left] == arr[left + 1]) left++;
                        while (left < right && arr[right] == arr[right - 1]) right--;

                        left++;
                        right--;
                    }
                    else if (sum < target) left++;
                    else right--;
                }
            }
        }
        return ans;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 0, -1, 0, -2, 2};
        int target = 0;

        Solution obj = new Solution();
        List<List<Integer>> ans = obj.fourSum(arr, target);

        for (List<Integer> quad : ans) {
            System.out.println(quad);
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q33
# Length of the longest subarray with zero Sum

## 🔹 Problem Summary
Problem Statement: Given an array containing both positive and negative integers, we have to find the length of the longest subarray with the sum of all elements equal to zero.

**Examples:**
Examples
Example 1:
Input:
 N = 6, array[] = {9, -3, 3, -1, 6, -5}  

Result:
 5  

Explanation:
 The following subarrays sum to zero:
- {-3, 3}
- {-1, 6, -5}
- {-3, 3, -1, 6, -5}
The length of the longest subarray with sum zero is 5.


Example 2:
Input:
 N = 8, array[] = {6, -2, 2, -8, 1, 7, 4, -10}  

Result:
 8  

Explanation:
 Subarrays with sum zero:
- {-2, 2}
- {-8, 1, 7}
- {-2, 2, -8, 1, 7}
- {6, -2, 2, -8, 1, 7, 4, -10}
The length of the longest subarray with sum zero is 8.

---

## 🔹 Key Observations & Intuition
* Initialize a variable sum = 0, which stores the sum of elements traversed so far, and another variable max = 0, which stores the length of the longest subarray with sum zero.
* Declare a HashMap<Integer, Integer> to store the prefix sum of every element as a key and its index as a value.
* Traverse the array and add the array element to the sum.
* If sum = 0, update max with the maximum value between max and current_index + 1, as the subarray from the start to the current index has a sum of 0.
* If sum is not equal to zero, check the HashMap to see if we've encountered this sum before.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Initialize a variable max = 0, which stores the length of the longest subarray with a sum of 0.
Traverse the array from the start and initialize a variable sum = 0, which stores the sum of the subarray starting with the current index.
Traverse from the next element of the current index up to the end of the array. Each time, add the element to the sum and check if it is equal to 0.
If sum = 0, check if the length of the subarray so far is greater than max, and if yes, update max.
Continue adding elements and repeat the above step until the outer loop completes traversing all elements.
Finally, return the max which holds the length of the longest subarray with a sum of 0.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

// core logic holder
class Solution {
    // compute length of the longest subarray with sum 0
    public int solve(int[] a) {
        // store best length found so far
        int maxLen = 0;
        // map prefix sum -> first index seen
        Map<Integer, Integer> sumIndexMap = new HashMap<>();
        // running prefix sum
        int sum = 0;

        // iterate through the array
        for (int i = 0; i < a.length; i++) {
            // update running sum
            sum += a[i];

            // if sum is zero, subarray [0..i] has zero sum
            if (sum == 0) {
                // update best length
                maxLen = i + 1;
            }
            // if this sum seen before, subarray (prevIndex..i] has zero sum
            else if (sumIndexMap.containsKey(sum)) {
                // maximize length using previous index
                maxLen = Math.max(maxLen, i - sumIndexMap.get(sum));
            }
            // first time seeing this sum, store its index
            else {
                sumIndexMap.put(sum, i);
            }
        }

        // return best length
        return maxLen;
    }
}

// separate main class
public class Main {
    // program entry
    public static void main(String[] args) {
        // sample input
        int[] a = new int[] {9, -3, 3, -1, 6, -5};
        // compute result
        int ans = new Solution().solve(a);
        // print result
        System.out.println(ans);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Initialize a variable sum = 0, which stores the sum of elements traversed so far, and another variable max = 0, which stores the length of the longest subarray with sum zero.
Declare a HashMap<Integer, Integer> to store the prefix sum of every element as a key and its index as a value.
Traverse the array and add the array element to the sum.
If sum = 0, update max with the maximum value between max and current_index + 1, as the subarray from the start to the current index has a sum of 0.
If sum is not equal to zero, check the HashMap to see if we've encountered this sum before.
If the HashMap contains the sum, this indicates that a subarray with the same sum exists, so update max accordingly.
If the sum is not found in the HashMap, insert (sum, current_index) into the HashMap to store the prefix sum until the current index.
After traversing the entire array, the max variable will hold the length of the longest subarray with a sum equal to zero. Return max.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

// core logic holder
class Solution {
    // compute length of the longest subarray with sum 0
    public int maxLen(int[] A, int n) {
        // map prefix sum -> first index seen
        Map<Integer, Integer> mpp = new HashMap<>();
        // best length so far
        int maxi = 0;
        // running prefix sum
        int sum = 0;

        // iterate over the array
        for (int i = 0; i < n; i++) {
            // update running sum
            sum += A[i];

            // if sum is zero, subarray [0..i] has zero sum
            if (sum == 0) {
                // update best length
                maxi = i + 1;
            }
            // otherwise check if this sum was seen before
            else {
                // when seen, zero-sum segment between previous index + 1 and i
                if (mpp.containsKey(sum)) {
                    // maximize length
                    maxi = Math.max(maxi, i - mpp.get(sum));
                }
                // first time seeing this sum
                else {
                    // record index
                    mpp.put(sum, i);
                }
            }
        }

        // return best length
        return maxi;
    }
}

// separate main class
public class Main {
    // program entry
    public static void main(String[] args) {
        // sample input
        int[] A = new int[]{9, -3, 3, -1, 6, -5};
        // compute size
        int n = A.length;
        // compute result
        int ans = new Solution().maxLen(A, n);
        // print result
        System.out.println(ans);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q34
# Count the number of subarrays with given xor K

## 🔹 Problem Summary
Problem Statement: Given an array of integers A and an integer B. Find the total number of subarrays having bitwise XOR of all elements equal to k.

**Examples:**
Examples
Input: A = [4, 2, 2, 6, 4] , k = 6
Output: 4
Explanation: The subarrays having XOR of their elements as 6 are  [4, 2], [4, 2, 2, 6, 4], [2, 2, 6], [6]

Input: A = [5, 6, 7, 8, 9], k = 5
Output: 2
Explanation: The subarrays having XOR of their elements as 5 are [5] and [5, 6, 7, 8, 9]

---

## 🔹 Key Observations & Intuition
* The brute force approach checks all possible subarrays and computes their XOR, but this quickly becomes inefficient for large arrays because it requires checking every pair of indices. Instead, we can make use of prefix XORs. A prefix XOR at index i represents the XOR of all elements from the start up to i. Using this, the XOR of any subarray can be derived by taking the XOR of two prefix XOR values.
* Now, to find whether a subarray ending at the current position has XOR equal to k, we only need to check if there was an earlier prefix XOR such that when we combine it with the current prefix XOR, the result is k. In other words, the condition becomes prefixXor[r] ^ prefixXor[l-1] = k.
* We keep track of how many times each prefix XOR has appeared using a hashmap (or dictionary). Whenever we find one that matches, we increase our count. This way, instead of checking all subarrays, we just use the hashmap and solve it much faster.
* Initialize a hashmap to store how many times each prefix XOR has appeared.
* Keep a variable to store the current prefix XOR as we move through the array.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute-Force Approach)**

**Idea:**
We to find the total number of subarrays (continuous segments of the array) such that the XOR of all elements in that subarray equals B. A brute force way would be to consider every possible subarray of the array and check its XOR.
Initialize a counter to 0 for storing the number of valid subarrays.
Loop through each index i as the starting point of the subarray.
Set a variable xor = 0 for maintaining the running XOR of the current subarray.
Loop through each index j from i to n-1 to extend the subarray.
Update xor by taking xor = xor ^ A[j].
If xor equals B, increment the counter by 1.
After all iterations, return the counter as the total number of subarrays.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to count subarrays with XOR equal to B
    public int countSubarraysXOR(int[] A, int B) {
        // Initialize count of valid subarrays
        int count = 0;
        // Traverse all starting points
        for (int i = 0; i < A.length; i++) {
            // Maintain xor of current subarray
            int xorVal = 0;
            // Extend subarray till end
            for (int j = i; j < A.length; j++) {
                // Update xor
                xorVal ^= A[j];
                // If xor equals B, increment count
                if (xorVal == B) {
                    count++;
                }
            }
        }
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        // Input array
        int[] A = {4, 2, 2, 6, 4};
        // Target xor
        int B = 6;

        Solution sol = new Solution();
        System.out.println(sol.countSubarraysXOR(A, B));
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
The brute force approach checks all possible subarrays and computes their XOR, but this quickly becomes inefficient for large arrays because it requires checking every pair of indices. Instead, we can make use of prefix XORs. A prefix XOR at index i represents the XOR of all elements from the start up to i. Using this, the XOR of any subarray can be derived by taking the XOR of two prefix XOR values.

Now, to find whether a subarray ending at the current position has XOR equal to k, we only need to check if there was an earlier prefix XOR such that when we combine it with the current prefix XOR, the result is k. In other words, the condition becomes prefixXor[r] ^ prefixXor[l-1] = k.

We keep track of how many times each prefix XOR has appeared using a hashmap (or dictionary). Whenever we find one that matches, we increase our count. This way, instead of checking all subarrays, we just use the hashmap and solve it much faster.
Initialize a hashmap to store how many times each prefix XOR has appeared.
Keep a variable to store the current prefix XOR as we move through the array.
Keep another variable to count the total number of subarrays with XOR equal to k.
For each element in the array, update the prefix XOR by combining it with the current element.
If the prefix XOR itself is equal to k, increase the count by one.
Check if there exists a prefix XOR seen before that can make the subarray XOR equal to k, and if yes, add its frequency from the hashmap to the count.
Store or update the frequency of the current prefix XOR in the hashmap.
After processing all elements, the count will be the total number of subarrays with XOR equal to k.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to count subarrays with given XOR
    public int countSubarrays(int[] A, int k) {
        // Store frequency of prefix XORs
        Map<Integer, Integer> freq = new HashMap<>();
        // Initialize with prefix XOR 0
        freq.put(0, 1);

        // Current prefix XOR
        int prefixXor = 0;
        // Answer count
        int count = 0;

        // Traverse array
        for (int num : A) {
            // Update prefix XOR
            prefixXor ^= num;

            // Compute required XOR
            int target = prefixXor ^ k;

            // If target exists in map, add its frequency
            if (freq.containsKey(target)) {
                count += freq.get(target);
            }

            // Store current prefix XOR in map
            freq.put(prefixXor, freq.getOrDefault(prefixXor, 0) + 1);
        }
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] A = {4, 2, 2, 6, 4};
        int k = 6;
        Solution sol = new Solution();
        System.out.println(sol.countSubarrays(A, k));
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute-Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q35
# Merge Overlapping Sub-intervals

## 🔹 Problem Summary
Problem Statement: Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals and return an array of the non-overlapping intervals that cover all the intervals in the input.

**Examples:**
Examples
Input : intervals=[[1,3],[2,6],[8,10],[15,18]]
Output : [[1,6],[8,10],[15,18]]
Explanation : Since intervals [1,3] and [2,6] are overlapping we can merge them to form [1,6] intervals.

Input : [[1,4],[4,5]]
Output :  [[1,5]]
Explanation :  Since intervals [1,4] and [4,5] are overlapping we can merge them to form [1,5].

---

## 🔹 Key Observations & Intuition
* Imagine laying intervals out on a number line. If two intervals overlap, we can combine them into one, like merging blocks that touch or overlap.
* Instead of checking each interval with every other one (as in brute-force), we first sort the intervals, so that any overlapping intervals will come one after the other. This way, we only need to compare each interval with the last one added to our answer. If they overlap, we merge them. If they don’t, we simply add the current interval as a new entry.
* Sort the intervals based on their starting points. This ensures overlapping intervals come together.
* Initialize an empty list to store the final merged intervals.
* If the list is empty or the current interval starts after the last one ends, it means there is no overlap, so just add it to the list.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute-Force Approach)**

**Idea:**
The main idea is to combine intervals that overlap with each other. To do this easily, we first sort the intervals by their starting point so that all overlapping intervals come next to each other. Then, for each interval, we try to see if the next ones overlap with it. If they do, we merge them into one bigger interval. We keep doing this until we find a non-overlapping interval, and then start the process again from that point.
Sort all intervals based on their starting points. This helps bring all overlapping intervals next to each other.
Go through each interval one by one and if the current interval is already covered by a previously merged interval, skip it. Else, pick the current interval as the starting point of a new merged interval.
Now run another loop to check if the following intervals overlap with the current one
If the start of next interval is less than or equal to the end of the current merged interval, it means they overlap. Therefore, extend the end of the merged interval to be the maximum of the two ends.
Keep doing this for the next intervals as long as they overlap. As soon as you find an interval that doesn't overlap, break the inner loop and move back to the outer loop to process the next non-overlapping interval.
Store each merged interval in the final answer list and after the loop ends, return the list of merged intervals.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to merge overlapping intervals using brute force
    public List<List<Integer>> merge(int[][] intervals) {

        // Sort intervals based on starting point
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

        List<List<Integer>> ans = new ArrayList<>();

        int n = intervals.length;
        int i = 0;

        // Loop through intervals
        while (i < n) {
            // Start of merged interval
            int start = intervals[i][0];
            int end = intervals[i][1];

            int j = i + 1;

            // Check all overlapping intervals
            while (j < n && intervals[j][0] <= end) {
                // Extend the end of current interval
                end = Math.max(end, intervals[j][1]);
                j++;
            }

            // Add merged interval to result
            ans.add(Arrays.asList(start, end));

            // Move to next non-overlapping interval
            i = j;
        }

        return ans;
    }
}

public class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[][] intervals = {{1, 3}, {2, 6}, {8, 10}, {15, 18}};
        List<List<Integer>> result = sol.merge(intervals);
        for (List<Integer> interval : result) {
            System.out.print(interval + " ");
        }
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
Imagine laying intervals out on a number line. If two intervals overlap, we can combine them into one, like merging blocks that touch or overlap.

Instead of checking each interval with every other one (as in brute-force), we first sort the intervals, so that any overlapping intervals will come one after the other. This way, we only need to compare each interval with the last one added to our answer. If they overlap, we merge them. If they don’t, we simply add the current interval as a new entry.
Sort the intervals based on their starting points. This ensures overlapping intervals come together.
Initialize an empty list to store the final merged intervals.
If the list is empty or the current interval starts after the last one ends, it means there is no overlap, so just add it to the list.
If the current interval starts before or exactly at the end of the last one, it means there is overlap. So, combine both by extending the end of the last one to the further end of the two.
Keep doing this until all intervals have been checked. The final list will now contain only non-overlapping, merged intervals.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to merge overlapping intervals
    public List<List<Integer>> merge(int[][] intervals) {
        // Sort intervals based on start time
        Arrays.sort(
            intervals,
            (a, b) -> Integer.compare(a[0], b[0])
        );

        // List to store merged intervals
        List<List<Integer>> merged = new ArrayList<>();

        // Traverse through all intervals
        for (int[] interval : intervals) {
            // If merged list is empty or no overlap
            if (
                merged.isEmpty() ||
                merged.get(merged.size() - 1).get(1) < interval[0]
            ) {
                // Add current interval as a new block
                merged.add(
                    Arrays.asList(interval[0], interval[1])
                );
            } else {
                // Overlapping: update end to max of both
                int last = merged.size() - 1;
                int maxEnd = Math.max(
                    merged.get(last).get(1),
                    interval[1]
                );
                merged.get(last).set(1, maxEnd);
            }
        }

        return merged;
    }
}

class Main {
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[][] intervals = {
            {1, 3}, {2, 6}, {8, 10}, {15, 18}
        };

        List<List<Integer>> result = sol.merge(intervals);

        for (List<Integer> interval : result) {
            System.out.print(
                "[" + interval.get(0) + "," + interval.get(1) + "] "
            );
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute-Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q36
# Merge two Sorted Arrays Without Extra Space

## 🔹 Problem Summary
Problem Statement: Given two sorted integer arrays nums1 and nums2, merge both the arrays into a single array sorted in non-decreasing order.
The final sorted array should be stored inside the array nums1 and it should be done in-place.
Array nums1 has a length of m + n, where the first m elements denote the elements of nums1 and rest are 0s whereas nums2 has a length of n.

**Examples:**
Examples
Input : nums1 = [-5, -2, 4, 5, 0, 0, 0], nums2 = [-3, 1, 8]
Output : [-5, -3, -2, 1, 4, 5, 8]
Explanation : The merged array is: [-5, -3, -2, 1, 4, 5, 8], where [-5, -2, 4, 5] are from nums1 and [-3, 1, 8] are from nums2

Input : nums1 = [0, 2, 7, 8, 0, 0, 0], nums2 = [-7, -3, -1]
Output :  [-7, -3, -1, 0, 2, 7, 8]
Explanation :  The merged array is: [-7, -3, -1, 0, 2, 7, 8], where [0, 2, 7, 8] are from nums1 and [-7, -3, -1] are from nums2

---

## 🔹 Key Observations & Intuition
* We are given two sorted arrays nums1 and nums2 and nums1 has enough space at the end (filled with zeros) to accommodate all elements from nums2. Now, if we try to insert elements from nums2 into nums1 from the beginning, we would need to shift elements in nums1 every time to make room which becomes time consuming and inefficient.
* Since both arrays are sorted in non-decreasing order, the largest elements will be at the end of each array. If we start comparing elements from the back of both arrays and place the largest one at the end of nums1, we won't need to shift anything.
* To efficiently insert elements at the end, we will use three pointers.
* Initialize three pointers: One points at the last valid index (excluding zeros) of nums1, one points at the last valid index of nums2 andd the last pointer points to last index of nums1.
* Compare the elements pointed by the first two pointers and whichever is larger, place it at the third pointer's index.

---

## 🔹 Approaches

### ➤ Brute Force
**(Approach)**

**Idea:**
We are given two sorted arrays nums1 and nums2 and nums1 has enough space at the end (filled with zeros) to accommodate all elements from nums2. Now, if we try to insert elements from nums2 into nums1 from the beginning, we would need to shift elements in nums1 every time to make room which becomes time consuming and inefficient.

Since both arrays are sorted in non-decreasing order, the largest elements will be at the end of each array. If we start comparing elements from the back of both arrays and place the largest one at the end of nums1, we won't need to shift anything.

To efficiently insert elements at the end, we will use three pointers.
Initialize three pointers: One points at the last valid index (excluding zeros) of nums1, one points at the last valid index of nums2 andd the last pointer points to last index of nums1.
Compare the elements pointed by the first two pointers and whichever is larger, place it at the third pointer's index.
Move the respective pointer one step back and also move the third pointer one step back.
If there are any remaining elements in nums2, then copy them in nums1. If any elements remain in nums1, they’re already in place
The result is a fully merged and sorted array stored in nums1 itself.

**Java Code:**
```java
class Solution {
    // Merges nums2 into nums1 in-place in sorted order.
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        // i: last valid index in nums1
        int i = m - 1;

        // j: last index in nums2
        int j = n - 1;

        // k: last index in nums1 including extra 0s
        int k = m + n - 1;

        // Fill nums1 from the back
        while (i >= 0 && j >= 0) {
            // Place larger element from end of nums1 or nums2
            if (nums1[i] > nums2[j]) {
                nums1[k--] = nums1[i--];
            } else {
                nums1[k--] = nums2[j--];
            }
        }

        // If nums2 has leftovers, copy them to nums1
        while (j >= 0) {
            nums1[k--] = nums2[j--];
        }

        // Remaining nums1 elements are already in correct position
    }
}

public class Main {
    public static void main(String[] args) {
        int[] nums1 = {1, 3, 5, 0, 0, 0};
        int[] nums2 = {2, 4, 6};
        int m = 3, n = 3;

        new Solution().merge(nums1, m, nums2, n);

        // Print the merged array
        for (int num : nums1) {
            System.out.print(num + " ");
        }
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **Refer to approach details** time complexity
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Approach** | Refer to approach details | Refer to approach details |

---

---
Q37
# Find the repeating and missing numbers

## 🔹 Problem Summary
Problem Statement: Given an integer array nums of size n containing values from [1, n] and each value appears exactly once in the array, except for A, which appears twice and B which is missing.
Return the values A and B, as an array of size 2, where A appears in the 0-th index and B in the 1st index.

Note: You are not allowed to modify the original array.

**Examples:**
Examples
Example 1:
Input:
 nums = [3, 5, 4, 1, 1]  

Output:
 [1, 2]  

Explanation:
 1 appears twice in the array, and 2 is missing from the array. So the output is [1, 2].


Example 2:
Input:
 nums = [1, 2, 3, 6, 7, 5, 7]  

Output:
 [7, 4]  

Explanation:
 7 appears twice in the array, and 4 is missing from the array. So the output is [7, 4].

---

## 🔹 Key Observations & Intuition
* First, iterate through the array and calculate the XOR of all the elements in the array and the numbers from 1 to N. Store the result in a variable called xr.
* To find the position of the first set bit from the right, perform a bitwise AND operation between xr and the negation of xr - 1, i.e., xr & ~(xr - 1). This will give the bit position of the first set bit.
* Initialize two variables, zero and one. For each element in the array and for each number from 1 to N, check the bit at the position found in the previous step.
* If the bit is 1, XOR the element with the variable one. If the bit is 0, XOR the element with the variable zero.
* After processing all the elements, you will have two variables, zero and one, which represent two numbers, one of which is the repeating number and the other is the missing number.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force)**

**Idea:**
Iterate through the array from index 1 to N, where N is the size of the array.
For each integer, i, use linear search to count its occurrence in the given array.
If an element has an occurrence of 2, store it as a candidate element.
If an element has an occurrence of 0, store it as another candidate element.
Finally, return the two elements that have occurrences of 2 and 0, respectively.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find repeating and missing numbers
    public int[] findMissingRepeatingNumbers(int[] nums) {
        int n = nums.length; // Size of the array
        int repeating = -1, missing = -1;

        // Find the repeating and missing number:
        for (int i = 1; i <= n; i++) {
            // Count the occurrences:
            int cnt = 0;
            for (int j = 0; j < n; j++) {
                if (nums[j] == i) cnt++;
            }

            // Check if i is repeating or missing
            if (cnt == 2) repeating = i;
            else if (cnt == 0) missing = i;

            // Stop early if both found
            if (repeating != -1 && missing != -1)
                break;
        }

        // Return {repeating, missing}
        return new int[]{repeating, missing};
    }
}

// Separate main class
public class Main {
    public static void main(String[] args) {
        int[] nums = {3, 1, 2, 5, 4, 6, 7, 5};

        // Create an instance of Solution class
        Solution sol = new Solution();

        int[] result = sol.findMissingRepeatingNumbers(nums);

        // Print the repeating and missing numbers found
        System.out.println("The repeating and missing numbers are: {" 
                            + result[0] + ", " + result[1] + "}");
    }
}
```

---

### ➤ Better Approach
**(Better Approach)**

**Idea:**
Declare a hash array of size N+1 where N is the range of numbers in the array (from 1 to N). This hash array will store the frequency of each element.
Iterate through the given array and for each element encountered, update the frequency in the hash array.
Once all elements are processed, iterate through the hash array and identify the two elements: one with frequency 2 and one with frequency 0.
Return the two elements that have frequencies of 2 and 0, respectively.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ or $O(N)$
* **Space Complexity:** $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find repeating and missing numbers
    public int[] findMissingRepeatingNumbers(int[] nums) {
        
        // Size of the array
        int n = nums.length;
        
        // Hash array to count occurrences
        int[] hash = new int[n + 1];
        
        // Update the hash array:
        for (int i = 0; i < n; i++) {
            hash[nums[i]]++;
        }

        int repeating = -1, missing = -1;
        
        // Find the repeating and missing number:
        for (int i = 1; i <= n; i++) {
            if (hash[i] == 2) {
                repeating = i;
            } else if (hash[i] == 0) {
                missing = i;
            }

            // Stop early if both found
            if (repeating != -1 && missing != -1) {
                break;
            }
        }
        
        // Return [repeating, missing]
        return new int[]{repeating, missing};
    }
}

// Separate main class
public class Main {
    public static void main(String[] args) {
        int[] nums = {3, 1, 2, 5, 4, 6, 7, 5};
        
        // Create an instance of Solution class
        Solution sol = new Solution();

        int[] result = sol.findMissingRepeatingNumbers(nums);
        
        // Print the repeating and missing numbers found
        System.out.println("The repeating and missing numbers are: {" 
                            + result[0] + ", " + result[1] + "}");
    }
}
```

---

### ➤ Better Approach
**(Optimal Approach 1)**

**Idea:**
First, calculate the sum of all elements in the given array, denoted as S, and the sum of natural numbers from 1 to N, denoted as Sn. The formula for Sn is (N * (N + 1)) / 2.
Now calculate S - Sn. This gives us X - Y, where X is the repeating number and Y is the missing number.
Next, calculate the sum of squares of all elements in the array, denoted as S2, and the sum of squares of the first N numbers, denoted as S2n. The formula for S2n is (N * (N + 1) * (2N + 1)) / 6.
Now calculate S2 - S2n. This gives us X2 - Y2.
From the equations S - Sn = X - Y and S2 - S2n = X2 - Y2, we can compute X + Y by the formula (S2 - S2n) / (S - Sn).
Using the values of X + Y and X - Y, we can solve for X and Y through simple addition and subtraction.
Finally, return the values of X (the repeating number) and Y (the missing number).

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find repeating and missing numbers
    public int[] findMissingRepeatingNumbers(int[] nums) {
        
        // Size of the array
        long n = nums.length;

        // Sum of first n natural numbers
        long SN = (n * (n + 1)) / 2;

        // Sum of squares of first n natural numbers
        long S2N = (n * (n + 1) * (2 * n + 1)) / 6;

        // Calculate actual sum (S) and sum of squares (S2) of array elements
        long S = 0, S2 = 0;
        for (int i = 0; i < n; i++) {
            S += nums[i];
            S2 += (long) nums[i] * (long) nums[i];
        }

        // Compute the difference values
        long val1 = S - SN; // X - Y

        // S2 - S2n = X^2 - Y^2
        long val2 = S2 - S2N;

        // Calculate X + Y
        val2 = val2 / val1;

        // Calculate X and Y
        long x = (val1 + val2) / 2; // repeating
        long y = x - val1;          // missing

        return new int[]{(int) x, (int) y};
    }
}

// Separate main class
public class Main {
    public static void main(String[] args) {
        int[] nums = {3, 1, 2, 5, 4, 6, 7, 5};

        // Create an instance of Solution class
        Solution sol = new Solution();

        int[] result = sol.findMissingRepeatingNumbers(nums);

        // Print the repeating and missing numbers found
        System.out.printf("The repeating and missing numbers are: {%d, %d}\n", result[0], result[1]);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach 2)**

**Idea:**
First, iterate through the array and calculate the XOR of all the elements in the array and the numbers from 1 to N. Store the result in a variable called xr.
To find the position of the first set bit from the right, perform a bitwise AND operation between xr and the negation of xr - 1, i.e., xr & ~(xr - 1). This will give the bit position of the first set bit.
Initialize two variables, zero and one. For each element in the array and for each number from 1 to N, check the bit at the position found in the previous step.
If the bit is 1, XOR the element with the variable one. If the bit is 0, XOR the element with the variable zero.
After processing all the elements, you will have two variables, zero and one, which represent two numbers, one of which is the repeating number and the other is the missing number.
To identify which is which, traverse the entire array and check how many times zero appears.
If zero appears twice, it is the repeating number; otherwise, it is the missing number. Based on the identity of zero, determine which category one belongs to.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {
    // Function to find repeating and missing numbers
    public int[] findMissingRepeatingNumbers(int[] nums) {
        // Size of the array
        int n = nums.length; 

        // XOR of all elements and numbers from 1 to n
        int xr = 0;
        for (int i = 0; i < n; i++) {
            xr = xr ^ nums[i];     // XOR with array element
            xr = xr ^ (i + 1);     // XOR with natural number
        }

        // Get the rightmost set bit in xr
        int number = (xr & ~(xr - 1));

        // Two groups based on this bit
        int zero = 0, one = 0;

        // Divide nums into groups and XOR within each group
        for (int i = 0; i < n; i++) {
            if ((nums[i] & number) != 0) {
                one ^= nums[i];
            } else {
                zero ^= nums[i];
            }
        }

        // Divide natural numbers 1 to n into groups and XOR
        for (int i = 1; i <= n; i++) {
            if ((i & number) != 0) {
                one ^= i;
            } else {
                zero ^= i;
            }
        }

        // Check which is repeating and which is missing
        int cnt = 0;
        for (int val : nums) {
            if (val == zero) cnt++;
        }

        if (cnt == 2) {
            return new int[]{zero, one}; // zero is repeating
        }
        return new int[]{one, zero}; // one is repeating
    }
}

// Separate main class
public class Main {
    public static void main(String[] args) {
        int[] nums = {3, 1, 2, 5, 4, 6, 7, 5};

        Solution sol = new Solution();
        int[] result = sol.findMissingRepeatingNumbers(nums);

        System.out.println("The repeating and missing numbers are: {" + result[0] + ", " + result[1] + "}");
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ or worse | $O(1)$ |
| **Better Approach** | $O(N \log N)$ or $O(N)$ | $O(N)$ |
| **Optimal Approach 1** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |
| **Optimal Approach 2** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q38
# Count inversions in an array

## 🔹 Problem Summary
Problem Statement: Given an array of N integers, count the inversion of the array (using merge-sort).

**Examples:**
Examples
Example 1:
Input Format: N = 5, array[] = {1,2,3,4,5}
Result: 0
Explanation: we have a sorted array and the sorted array has 0 inversions as for i < j you will never find a pair such that A[j] < A[i]. More clear example: 2 has index 1 and 5 has index 4 now 1 < 5 but 2 < 5 so this is not an inversion.

Example 2:
Input Format: N = 5, array[] = {5,4,3,2,1}
Result: 10
Explanation: we have a reverse sorted array and we will get the maximum inversions as for i < j we will always find a pair such that A[j] < A[i]. Example: 5 has index 0 and 3 has index 2 now (5,3) pair is inversion as 0 < 2 and 5 > 3 which will satisfy out conditions and for reverse sorted array we will get maximum inversions and that is (n)*(n-1) / 2.For above given array there is 4 + 3 + 2 + 1 = 10 inversions.

Example 3:
Input Format: N = 5, array[] = {5,3,2,1,4}
Result: 7
Explanation: There are 7 pairs (5,1), (5,3), (5,2), (5,4),(3,2), (3,1), (2,1) and we have left 2 pairs (2,4) and (1,4) as both are not satisfy our condition.

---

## 🔹 Key Observations & Intuition
* The brute force approach compares all pairs, but that takes O(N2) time. We can optimize this using the merge sort algorithm. While merging two sorted halves, if an element in the left half is greater than an element in the right half, then all remaining elements in the left half will also be greater than that right element. This allows us to count multiple inversions in one step, instead of checking each pair individually.
* Apply merge sort recursively to divide the array into two halves.
* During the merge step:
* If arr[left] <= arr[right], place arr[left] into the temp array and move left++.
* Otherwise, place arr[right] into the temp array. Since arr[left] > arr[right], all elements from arr[left] to arr[mid] form inversions with arr[right]. So add (mid - left + 1) to the inversion count.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
An inversion in an array is defined as a pair of indices (i, j) such that i < j and a[i] > a[j]. This measures how far the array is from being sorted. To count inversions, the brute force way is to compare every element with all elements to its right and increment the counter whenever we find an inversion.

Initialize a counter cnt = 0.
Use two nested loops:
Outer loop runs for each element a[i].
Inner loop checks all elements a[j] where j > i.
If a[i] > a[j], increment cnt.
After traversing all pairs, return cnt as the number of inversions.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class Main {
    // Function to count inversions
    static int numberOfInversions(int[] arr) {
        int cnt = 0; // Initialize count
        int n = arr.length;
        // Check all pairs
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (arr[i] > arr[j]) cnt++; // Increment if inversion found
            }
        }
        return cnt; // Return total inversions
    }

    public static void main(String[] args) {
        int[] arr = {5, 4, 3, 2, 1};
        int inversions = numberOfInversions(arr);
        System.out.println("The number of inversions is: " + inversions);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
The brute force approach compares all pairs, but that takes O(N2) time. We can optimize this using the merge sort algorithm. While merging two sorted halves, if an element in the left half is greater than an element in the right half, then all remaining elements in the left half will also be greater than that right element. This allows us to count multiple inversions in one step, instead of checking each pair individually.

Apply merge sort recursively to divide the array into two halves.
During the merge step:
If arr[left] <= arr[right], place arr[left] into the temp array and move left++.
Otherwise, place arr[right] into the temp array. Since arr[left] > arr[right], all elements from arr[left] to arr[mid] form inversions with arr[right]. So add (mid - left + 1) to the inversion count.
Copy the merged elements back into the original array.
The total inversion count is the sum of:
Inversions in the left half
Inversions in the right half
Inversions across the halves (counted during merge)

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

class Solution {

    // Function to merge two halves and count inversions
    public int merge(int[] arr, int low, int mid, int high) {
        // Temporary array
        int[] temp = new int[high - low + 1];

        // Starting indices of left and right halves
        int left = low;
        int right = mid + 1;
        int k = 0;

        // Variable to count inversions
        int cnt = 0;

        // Merge elements in sorted order
        while (left <= mid && right <= high) {
            if (arr[left] <= arr[right]) {
                temp[k++] = arr[left++];
            } else {
                temp[k++] = arr[right++];
                cnt += (mid - left + 1); // Count inversions
            }
        }

        // Copy remaining elements of left half
        while (left <= mid) {
            temp[k++] = arr[left++];
        }

        // Copy remaining elements of right half
        while (right <= high) {
            temp[k++] = arr[right++];
        }

        // Copy back to original array
        for (int i = low; i <= high; i++) {
            arr[i] = temp[i - low];
        }

        return cnt;
    }

    // Merge sort function
    public int mergeSort(int[] arr, int low, int high) {
        int cnt = 0;

        if (low >= high) return cnt;

        int mid = (low + high) / 2;

        // Count inversions in left half
        cnt += mergeSort(arr, low, mid);
        // Count inversions in right half
        cnt += mergeSort(arr, mid + 1, high);
        // Count inversions during merge
        cnt += merge(arr, low, mid, high);

        return cnt;
    }

    // Function to get number of inversions
    public int numberOfInversions(int[] arr) {
        return mergeSort(arr, 0, arr.length - 1);
    }
}

public class Main {
    public static void main(String[] args) {
        // Input array
        int[] a = {5, 4, 3, 2, 1};

        // Create Solution object
        Solution obj = new Solution();

        // Count inversions
        int cnt = obj.numberOfInversions(a);

        System.out.println("The number of inversions are: " + cnt);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q39
# Count Reverse Pairs

## 🔹 Problem Summary
Problem Statement: Given an array of numbers, you need to return the count of reverse pairs. Reverse Pairs are those pairs where i<j and arr[i]>2*arr[j].

**Examples:**
Examples
Example 1:
Input:
 N = 5, array[] = {1,3,2,3,1)

Output
: 2 

Explanation:
 The pairs are (3, 1) and (3, 1) as from both the pairs the condition arr[i] > 2*arr[j] is satisfied.


Example 2:
Input:
 N = 4, array[] = {3,2,1,4}

Output:
 1

Explaination: 
There is only 1 pair  ( 3 , 1 ) that satisfy the condition arr[i] > 2*arr[j]

---

## 🔹 Key Observations & Intuition
* In order to solve this problem we will use the merge sort algorithm like we used in the problem count inversion with a slight modification of the merge() function. But in this case, the same logic will not work. In order to understand this, we need to deep dive into the merge() function.
* Why the same logic of count inversion will not work?
* The merge function works by comparing two elements from two halves i.e. arr[left] and arr[right]. Now, the condition in the question was arr[i] > arr[j]. That is why we merged the logic. While comparing the elements, we counted the number of pairs.
* But in this case, the condition is arr[i] > 2*arr[j]. And, we cannot change the condition of comparing the elements in the merge() function. If we change the condition, the merge() function will fail to merge the elements. So, we need to check this condition and count the number of pairs separately.
* Here, our approach will be to check, for every element in the sorted left half(sorted), how many elements in the right half(also sorted) can make a pair. Let’s try to understand, using the following example:

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute Force Approach)**

**Idea:**
The naive approach is pretty straightforward. We will use nested loops to generate all possible pairs. We know index i must be smaller than index j. So, we will fix i at one index at a time through a loop, and with another loop, we will check(the condition a[i] > 2*a[j]) the elements from index i+1 to N-1  if they can form a pair with a[i].

Note: For a better understanding of intuition, please watch the video at the bottom of the page.

Approach:

The steps are as follows:

First, we will run a loop(say i) from 0 to N-1 to select the a[i].
As index j should be greater than index i, inside loop i, we will run another loop i.e. j from i+1 to N-1, and select the element a[j].
Inside this second loop, we will check if a[i] > 2*a[j] i.e. if a[i] and a[j] can be a pair. If they satisfy the condition, we will increase the count by 1.
Finally, we will return the count i.e. the number of such pairs.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
import java.util.*;

public class tUf {

    public static int countPairs(int[] a, int n) {

        // Count the number of pairs:
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if (a[i] > 2 * a[j])
                    cnt++;
            }
        }
        return cnt;
    }

    public static int team(int[] skill, int n) {
        return countPairs(skill, n);
    }

    public static void main(String[] args) {
        int[] a = {4, 1, 2, 3, 1};
        int n = 5;
        int cnt = team(a, n);
        System.out.println("The number of reverse pair is: " + cnt);
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach)**

**Idea:**
In order to solve this problem we will use the merge sort algorithm like we used in the problem count inversion with a slight modification of the merge() function. But in this case, the same logic will not work. In order to understand this, we need to deep dive into the merge() function.

Why the same logic of count inversion will not work?

The merge function works by comparing two elements from two halves i.e. arr[left] and arr[right]. Now, the condition in the question was arr[i] > arr[j]. That is why we merged the logic. While comparing the elements, we counted the number of pairs.
But in this case, the condition is arr[i] > 2*arr[j]. And, we cannot change the condition of comparing the elements in the merge() function. If we change the condition, the merge() function will fail to merge the elements. So, we need to check this condition and count the number of pairs separately.

Here, our approach will be to check, for every element in the sorted left half(sorted), how many elements in the right half(also sorted) can make a pair. Let’s try to understand, using the following example:

For the first element of the left half i.e. 6, we will start checking from index 0 of the right half i.e. arr2[]. Now, we can clearly see that the first two elements of arr2[] can make a pair with arr1[0] i.e. 6.

For the next element i.e. arr1[1], we will start checking from index 2(0-based indexing) i.e. where we stopped for the previous element. 

Note: This process will work because arr1[1] will always be greater than arr1[0] which concludes if arr2[0] and arr2[1] are making a pair with arr1[0], they will obviously make pairs with a number greater than arr1[0] i.e. arr1[1].

Thus before the merge step in the merge sort algorithm, we will calculate the total number of pairs each time.

Approach:

The steps are basically the same as they are in the case of the merge sort algorithm. The change will be just in the mergeSort() function:

In order to count the number of pairs, we will keep a count variable, cnt, initialized to 0 beforehand inside the mergeSort().
We will add the numbers returned by the previous mergeSort() calls.
Before the merge step, we will count the number of pairs using a function, named countPairs().
We need to remember that the left half starts from low and ends at mid, and the right half starts from mid+1 and ends at high.

The steps of the countPairs() function will be as follows:

We will declare a variable, cnt, initialized with 0.
We will run a loop from low to mid, to select an element at a time from the left half.
Inside that loop, we will use another loop to check how many elements from the right half can make a pair.
Lastly, we will add the total number of elements i.e. (right-(mid+1)) (where right = current index), to the cnt and return it.

Note: For a better understanding of intuition, please watch the video at the bottom of the page.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
import java.util.*;

public class tUf {

    private static void merge(int[] arr, int low, int mid, int high) {
        ArrayList<Integer> temp = new ArrayList<>(); // temporary array
        int left = low;      // starting index of left half of arr
        int right = mid + 1;   // starting index of right half of arr

        //storing elements in the temporary array in a sorted manner//

        while (left <= mid && right <= high) {
            if (arr[left] <= arr[right]) {
                temp.add(arr[left]);
                left++;
            } else {
                temp.add(arr[right]);
                right++;
            }
        }

        // if elements on the left half are still left //

        while (left <= mid) {
            temp.add(arr[left]);
            left++;
        }

        //  if elements on the right half are still left //
        while (right <= high) {
            temp.add(arr[right]);
            right++;
        }

        // transfering all elements from temporary to arr //
        for (int i = low; i <= high; i++) {
            arr[i] = temp.get(i - low);
        }
    }

    public static int countPairs(int[] arr, int low, int mid, int high) {
        int right = mid + 1;
        int cnt = 0;
        for (int i = low; i <= mid; i++) {
            while (right <= high && arr[i] > 2 * arr[right]) right++;
            cnt += (right - (mid + 1));
        }
        return cnt;
    }

    public static int mergeSort(int[] arr, int low, int high) {
        int cnt = 0;
        if (low >= high) return cnt;
        int mid = (low + high) / 2 ;
        cnt += mergeSort(arr, low, mid);  // left half
        cnt += mergeSort(arr, mid + 1, high); // right half
        cnt += countPairs(arr, low, mid, high); //Modification
        merge(arr, low, mid, high);  // merging sorted halves
        return cnt;
    }

    public static int team(int[] skill, int n) {
        return mergeSort(skill, 0, n - 1);
    }

    public static void main(String[] args) {
        int[] a = {4, 1, 2, 3, 1};
        int n = 5;
        int cnt = team(a, n);
        System.out.println("The number of reverse pair is: " + cnt);
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

---
Q40
# Maximum Product Subarray in an Array

## 🔹 Problem Summary
Problem Statement: Given an array that contains both negative and positive integers, find the maximum product subarray.

**Examples:**
Examples
Input: Nums = [1,2,3,4,5,0]
Output: 120
Explanation: 
In the given array, 1×2×3×4×5 gives maximum product value.

Input: Nums = [1,2,-3,0,-4,-5]
Output: 20
Explanation: 
In the given array, (-4)×(-5) gives maximum product value.

---

## 🔹 Key Observations & Intuition
* In a product-based subarray problem, a negative number can flip the sign, turning a big minimum into a potential maximum. So, we track both the maximum and minimum products at each step. This helps handle negative numbers effectively.
* Start by setting the answer, current max product, and current min product to the first number.
* For each number in the array starting from the second:
* If the number is negative, swap current max and min.
* If the product of the current number and previous max is larger than the number itself, update current max to that product; otherwise, set it to the number.

---

## 🔹 Approaches

### ➤ Brute Force
**(Brute-Force Approach)**

**Idea:**
In the brute force method, we generate all possible subarrays and calculate the product of each subarray. We track the maximum product found among all. Use two nested loops, the outer loop picks the starting index of the subarray and the inner loop picks the ending index. For every subarray defined by start and end, calculate the product and update the maximum product if the current subarray's product is larger.

**Complexity:**
* **Time Complexity:** $O(N^2)$ or worse
* **Space Complexity:** $O(1)$

**Java Code:**
```java
class Solution {
    // This function finds the maximum product
    // of any contiguous subarray using brute force
    public int maxProduct(int[] nums) {
        // Initialize the answer with the first element
        int maxProd = nums[0];

        // Outer loop picks the starting index
        for (int i = 0; i < nums.length; i++) {
            // Initialize current product to 1
            int prod = 1;

            // Inner loop picks the ending index
            for (int j = i; j < nums.length; j++) {
                // Multiply current number to product
                prod *= nums[j];

                // Update maximum product if needed
                maxProd = Math.max(maxProd, prod);
            }
        }

        // Return the result
        return maxProd;
    }
}

public class Main {
    public static void main(String[] args) {
        // Sample input
        int[] nums = {2, 3, -2, 4};

        // Create Solution object
        Solution sol = new Solution();

        // Print the result
        System.out.println(sol.maxProduct(nums));
    }
}
```

---

### ➤ Better Approach
**(Optimal Approach - 1)**

**Idea:**
The product of elements in a subarray can become large when there are positive numbers, but negative numbers and zeros make it tricky. A negative number can flip a large product into a negative one, but if we meet another negative later, the sign flips back to positive. Therefore, to capture all possible max products, we do two things:
Traverse the array from left to right (prefix) to build cumulative product.
Traverse the array from right to left (suffix) to catch subarrays ending at the back (helpful when max product is at the end or due to even negatives).
Reset the product to 1 whenever a zero is found, as it breaks the subarray continuity.
By comparing products in both directions at each step, we ensure we don’t miss any possible maximum.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
// This class contains the function to find maximum product subarray
// using prefix and suffix traversal
class Solution {
    public int maxProductSubArray(int[] arr) {
        // Get the length of the array
        int n = arr.length;

        // Initialize prefix and suffix product
        int pre = 1, suff = 1;

        // Initialize answer with smallest integer
        int ans = Integer.MIN_VALUE;

        // Traverse from both left and right
        for (int i = 0; i < n; i++) {
            // Reset prefix if zero
            if (pre == 0) pre = 1;

            // Reset suffix if zero
            if (suff == 0) suff = 1;

            // Multiply prefix with current element from front
            pre *= arr[i];

            // Multiply suffix with current element from back
            suff *= arr[n - i - 1];

            // Update maximum value so far
            ans = Math.max(ans, Math.max(pre, suff));
        }

        // Return the final result
        return ans;
    }
}

// Separate Main class for testing
class Main {
    public static void main(String[] args) {
        // Sample input
        int[] arr = {2, 3, -2, 4};

        // Create object of Solution
        Solution sol = new Solution();

        // Call the method and print the result
        System.out.println(sol.maxProductSubArray(arr));
    }
}
```

---

### ➤ Optimal Approach
**(Optimal Approach - 2)**

**Idea:**
In a product-based subarray problem, a negative number can flip the sign, turning a big minimum into a potential maximum. So, we track both the maximum and minimum products at each step. This helps handle negative numbers effectively.
Start by setting the answer, current max product, and current min product to the first number.
For each number in the array starting from the second:
If the number is negative, swap current max and min.
If the product of the current number and previous max is larger than the number itself, update current max to that product; otherwise, set it to the number.
Similarly, if the product of the current number and previous min is smaller, update current min; otherwise, set it to the number.
If the current max is greater than the answer so far, update the answer.
Return the answer at the end.

**Complexity:**
* **Time Complexity:** $O(N)$ or $O(N \log N)$
* **Space Complexity:** $O(1)$ or $O(N)$

**Java Code:**
```java
class Solution {
    // This function returns the maximum product
    // of any contiguous subarray using optimized approach
    public int maxProduct(int[] nums) {
        int res = nums[0];
        int maxProd = nums[0];
        int minProd = nums[0];

        // Traverse from second element
        for (int i = 1; i < nums.length; i++) {
            int curr = nums[i];

            // Swap if current is negative
            if (curr < 0) {
                int temp = maxProd;
                maxProd = minProd;
                minProd = temp;
            }

            // Update max and min product
            maxProd = Math.max(curr, maxProd * curr);
            minProd = Math.min(curr, minProd * curr);

            // Update result
            res = Math.max(res, maxProd);
        }

        return res;
    }
}

public class Main {
    public static void main(String[] args) {
        int[] nums = {2, 3, -2, 4};
        Solution sol = new Solution();
        System.out.println(sol.maxProduct(nums));
    }
}
```

---

## 🔹 Edge Cases
* Empty array or array with single element
* Array with all identical elements
* Array with negative numbers
* Very large array sizes

---

## 🔹 Important Notes / Takeaways
* The optimal approach achieves **$O(N)$ or $O(N \log N)$** time complexity
* Always start with brute force in interviews, then optimize
* Understanding the problem constraints helps pick the right approach

---

## 🔹 Complexity Summary Table

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Brute-Force Approach** | $O(N^2)$ or worse | $O(1)$ |
| **Optimal Approach - 1** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |
| **Optimal Approach - 2** | $O(N)$ or $O(N \log N)$ | $O(1)$ or $O(N)$ |

---

