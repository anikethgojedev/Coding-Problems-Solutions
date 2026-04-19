Sorting Techniques - 
Q1
# Selection Sort 

## 🔹 Problem Summary
The **Selection Sort** algorithm sorts an array by repeatedly finding the **minimum element** from the unsorted part and putting it at the beginning. It divides the array into two parts: a sorted part at the left and an unsorted part at the right.

## 🔹 Key Observations & Intuition
* **The "Select and Swap" Strategy:** In every pass, we select the smallest element from the unsorted segment and swap it with the element at the current starting index.
* **Incremental Progress:** After the $i^{th}$ iteration, the first $i$ elements are guaranteed to be in their final sorted positions.
* **Fixed Iterations:** Unlike Bubble Sort, which might stop early if the array is sorted, Selection Sort always performs the same number of comparisons regardless of the initial order.

---

## 🔹 Approaches

Since Selection Sort is a straightforward algorithm, it is generally presented as a single approach. The tutorial focuses on this standard implementation.

### 🔸 Optimal Approach (Standard Selection Sort)

**Detailed Explanation:**
1.  **Outer Loop ($i$):** Runs from $0$ to $n-2$. It marks the start of the unsorted part of the array.
2.  **Inner Loop ($j$):** Scans the unsorted part (from $i+1$ to $n-1$) to find the index of the minimum value.
3.  **Swap:** Once the minimum element's index (`mini`) is found, swap it with the element at index $i$.
4.  **Repeat:** Move to the next index and repeat until the entire array is processed.

**Why it is used:**
It is optimal in terms of **swaps**. It performs at most $O(N)$ swaps, which is better than Bubble Sort or Insertion Sort in scenarios where memory write operations are significantly more expensive than reads.

**Complexity:**
* **Time Complexity:** $O(N^2)$ for Best, Average, and Worst cases. This is because there are two nested loops.
* **Space Complexity:** $O(1)$ as no extra data structures are used.

**Java Code:**
```java
import java.util.*;

public class Main {
    static void selection_sort(int arr[], int n) {
        for (int i = 0; i < n - 1; i++) {
            int mini = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[mini]) {
                    mini = j;
                }
            }
            //swap
            int temp = arr[mini];
            arr[mini] = arr[i];
            arr[i] = temp;
        }

        System.out.println("After selection sort:");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }

    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before selection sort:");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
        selection_sort(arr, n);
    }
}
```

---

## 🔹 Edge Cases
* **Already Sorted Array:** The algorithm will still perform $O(N^2)$ comparisons to verify the minimums.
* **Reverse Sorted Array:** Performs the same number of comparisons and the maximum number of swaps.
* **Array with Duplicate Elements:** Selection sort is **not stable** by default (it may change the relative order of equal elements during swaps).
* **Single Element Array:** The loops will naturally handle this as the outer loop condition `i < n - 1` will not be met.

---

## 🔹 Important Notes / Takeaways
* **Unstable Sorting:** Selection sort is generally not a stable sorting algorithm because the swapping step can move an element past another equal element.
* **In-place Algorithm:** It does not require additional memory proportional to the input size.
* **Comparison-based:** It relies on comparing elements to find the minimum.

---

## 🔹 Complexity Summary Table

| Case | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Best Case** | $O(N^2)$ | $O(1)$ |
| **Average Case** | $O(N^2)$ | $O(1)$ |
| **Worst Case** | $O(N^2)$ | $O(1)$ |

---
Q2
# Bubble Sort

## 🔹 Problem Summary
**Bubble Sort** is a sorting algorithm that works by repeatedly swapping adjacent elements if they are in the wrong order. In each pass, the largest remaining element "bubbles up" to its correct position at the end of the array.

## 🔹 Key Observations & Intuition
* **Adjacent Comparison:** The algorithm only compares two neighbors at a time.
* **Right-to-Left Sorting:** After the first iteration, the largest element is at the last index. After the second, the second-largest is at the second-to-last index, and so on.
* **Range Reduction:** The unsorted part of the array shrinks by one from the right after every full pass of the inner loop.

---

## 🔹 Approaches

### 🔸 Brute Force
**Idea:**
Use two nested loops. The outer loop controls the range of the unsorted array (starting from $N-1$ down to $0$), and the inner loop performs the adjacent swaps to push the maximum element to the end of that range.

**Time & Space Complexity:**
* **Time Complexity:** $O(N^2)$ for Best, Average, and Worst cases.
* **Space Complexity:** $O(1)$.

**Java Code:**
```java
import java.util.*;

public class Main {
    static void bubble_sort(int[] arr, int n) {
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j <= i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }

        System.out.println("After Using Bubble Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using Bubble Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
        bubble_sort(arr, n);
    }

}
```

---

### 🔸 Optimal Approach
**Detailed Explanation:**
In the brute force version, even if the array is already sorted, the algorithm continues to run $O(N^2)$ comparisons. We can optimize this by introducing a `didSwap` flag. If no swaps occur during an entire pass of the inner loop, the array is already sorted, and we can break out of the loop early.

**Why it is optimal:**
It improves the **Best Case** time complexity to $O(N)$ because it recognizes a sorted array after just one pass.

**Complexity:**
* **Time Complexity:** $O(N^2)$ for Worst and Average cases; **$O(N)$ for Best Case**.
* **Space Complexity:** $O(1)$.

**Java Code:**
```java
import java.util.*;

public class Main {
    static void bubble_sort(int[] arr, int n) {
        for (int i = n - 1; i >= 0; i--) {
            int didSwap = 0;
            for (int j = 0; j <= i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    didSwap = 1;
                }
            }
            if (didSwap == 0) {
                break;
            }
        }

        System.out.println("After Using Bubble Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using Bubble Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
        bubble_sort(arr, n);
    }
}
```

---

## 🔹 Edge Cases
* **Already Sorted Array:** The optimized approach handles this in $O(N)$ time.
* **Reverse Sorted Array:** This remains the worst-case scenario requiring $O(N^2)$ swaps and comparisons.
* **All Elements Identical:** Handled efficiently by the `didSwap` check in $O(N)$.

---

## 🔹 Important Notes / Takeaways
* **Stability:** Bubble Sort is **stable**; it does not change the relative order of elements with equal values.
* **In-place:** It sorts the array without requiring extra space ($O(1)$ auxiliary space).
* **Interview Insight:** While rarely used in production due to $O(N^2)$ complexity, it is a classic example of an algorithm that can be optimized from $O(N^2)$ to $O(N)$ for the best case.

---

## 🔹 Complexity Summary Table

| Approach | Best Case | Average Case | Worst Case | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Brute Force** | $O(N^2)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ |
| **Optimal (Optimized)** | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ |


---

Q3
# Insertion sort 

## 🔹 Problem Summary
**Insertion Sort** works similarly to the way you sort playing cards in your hands. It builds a sorted array one element at a time by taking an element from the unsorted part and **inserting** it into its correct position in the sorted part.

## 🔹 Key Observations & Intuition
* **Sorted & Unsorted Partition:** The array is virtually split into a sorted part (left) and an unsorted part (right).
* **Shifting, not just Swapping:** Instead of just swapping, the algorithm finds the correct "slot" and shifts all larger elements one position to the right to make room.
* **The "Key" Concept:** In each step, the current element (the "key") is compared with elements in the sorted part to its left.

---

## 🔹 Approaches

### 🔸 Standard Approach (Iterative)
**Idea:**
1. Start from the second element ($i=1$).
2. Compare the current element ($arr[i]$) with the elements in the sorted part ($arr[0...i-1]$).
3. If the element in the sorted part is larger, swap/shift it to the right.
4. Repeat until the entire array is sorted.

**Time & Space Complexity:**
* **Time Complexity:** $O(N^2)$ for Average and Worst cases; **$O(N)$ for Best Case** (when the array is already sorted).
* **Space Complexity:** $O(1)$ (In-place sorting).

**Java Code:**
```java
import java.util.*;

public class Main {
    static void insertion_sort(int[] arr, int n) {
        for (int i = 0; i <= n - 1; i++) {
            int j = i;
            while (j > 0 && arr[j - 1] > arr[j]) {
                int temp = arr[j - 1];
                arr[j - 1] = arr[j];
                arr[j] = temp;
                j--;
            }
        }

        System.out.println("After insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
        insertion_sort(arr, n);
    }
}
```

---

### 🔸 Recursive Approach
**Idea:**
1. **Base Case:** If array size is $\le 1$, return.
2. **Recursion:** Recursively sort the first $n-1$ elements.
3. **Insertion:** Insert the last element ($n^{th}$ element) at its correct position in the sorted array.

**Complexity:**
* **Time Complexity:** $O(N^2)$.
* **Space Complexity:** $O(N)$ due to the recursion stack.

**Java Code:**
```java
import java.util.*;

public class Main {
    static void insertion_sort(int[] arr, int i, int n) {

        // Base Case: i == n.
        if (i == n) return;

        int j = i;
        while (j > 0 && arr[j - 1] > arr[j]) {
            int temp = arr[j - 1];
            arr[j - 1] = arr[j];
            arr[j] = temp;
            j--;
        }

        insertion_sort(arr, i + 1, n);

    }

    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();

        insertion_sort(arr, 0, n);

        System.out.println("After insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```

---

## 🔹 Edge Cases
* **Already Sorted Array:** The `while` loop condition `arr[j-1] > arr[j]` fails immediately, resulting in $O(N)$ overall.
* **Reverse Sorted Array:** Maximum number of shifts/swaps ($O(N^2)$).
* **Duplicates:** Handled naturally; Insertion Sort is a **stable** algorithm.

---

## 🔹 Important Notes / Takeaways
* **Adaptive:** It is very efficient for arrays that are already "nearly sorted."
* **Stable:** It maintains the relative order of equal elements.
* **Online:** It can sort a list as it receives it (useful for data streams).

---

## 🔹 Complexity Summary Table

| Approach | Best Case | Average Case | Worst Case | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Iterative** | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ |
| **Recursive** | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(N)$ |

---

Q4
# Merge Sort 

These notes are based on the **Merge Sort Algorithm** tutorial from [takeuforward](https://takeuforward.org/data-structure/merge-sort-algorithm).

---

## 🔹 Problem Summary
**Merge Sort** is a **Divide and Conquer** algorithm. It works by repeatedly dividing an array into two halves until each subarray contains only one element (which is inherently sorted). Then, it merges those sorted halves back together in the correct order to produce the final sorted array.

## 🔹 Key Observations & Intuition
* **Divide and Conquer:** Breaking a large, complex problem into smaller, simpler sub-problems.
* **Recursion:** The algorithm uses a recursive function to split the array at the `mid` point.
* **The "Merge" Step:** This is the heart of the algorithm. It takes two sorted arrays and combines them into one sorted array using a temporary storage (list/array) and two pointers.

---

## 🔹 Approaches

### 🔸 Optimal Approach (Recursive Merge Sort)

**Detailed Explanation:**
1.  **Divide:** Find the middle index $mid = (low + high) / 2$ and split the array into two halves: `left` ($low$ to $mid$) and `right` ($mid+1$ to $high$).
2.  **Conquer:** Recursively call `mergeSort` on both halves until the base case ($low \ge high$) is reached.
3.  **Merge:** Use a `merge` function to combine the sorted halves.
    * Compare elements from both halves using two pointers (`left` and `right`).
    * Pick the smaller element and add it to a temporary list.
    * Once one half is exhausted, copy the remaining elements from the other half.
    * Transfer the elements from the temporary list back into the original array.

**Why it is optimal:**
Unlike Bubble or Selection Sort, Merge Sort consistently performs at $O(N \log N)$ regardless of the initial order of elements. It is highly predictable and efficient for large datasets.

**Complexity:**
* **Time Complexity:** $O(N \log N)$ in all cases (Best, Average, Worst).
    * *Explanation:* Dividing takes $\log N$ steps, and at each level, we perform $N$ comparisons to merge.
* **Space Complexity:** $O(N)$.
    * *Explanation:* We use a temporary `ArrayList` to store elements during the merge step.

**Java Code (Exactly as on website):**
```java
import java.util.*;

class Solution {
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

    public static void mergeSort(int[] arr, int low, int high) {
        if (low >= high) return;
        int mid = (low + high) / 2 ;
        mergeSort(arr, low, mid);  // left half
        mergeSort(arr, mid + 1, high); // right half
        merge(arr, low, mid, high);  // merging sorted halves
    }
}

public class Main {
    public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        int n = 7;
        int arr[] = { 9, 4, 7, 6, 3, 1, 5 };
        System.out.println("Before sorting array: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
        Solution.mergeSort(arr, 0, n - 1);
        System.out.println("After sorting array: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }

}
```

---

## 🔹 Edge Cases
* **Single Element:** If `low == high`, the base case returns immediately; a single element is already sorted.
* **Array with Duplicates:** Merge Sort is **Stable**, meaning it preserves the relative order of duplicate elements because we use `arr[left] <= arr[right]` in the merge logic.
* **Empty Array:** The initial call `mergeSort(arr, 0, n-1)` would result in `low > high`, handling it gracefully.

---

## 🔹 Important Notes / Takeaways
* **Stability:** Merge Sort is **Stable**.
* **Not In-Place:** It requires $O(N)$ extra space, making it less memory-efficient than Quick Sort or Heap Sort.
* **External Sorting:** It is preferred for sorting large data that doesn't fit into RAM (External Merge Sort).
* **Interview Tip:** When asked about complexity, emphasize that the $O(N \log N)$ is guaranteed even in the worst case.

---

## 🔹 Complexity Summary Table

| Approach | Best Case | Average Case | Worst Case | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Recursive Merge Sort** | $O(N \log N)$ | $O(N \log N)$ | $O(N \log N)$ | $O(N)$ |

---

Q5
# Recursive Bubble Sort

## 🔹 Problem Summary

**Recursive Sorting** aims to implement traditional sorting algorithms (Bubble and Insertion) using recursion instead of nested loops. This helps in understanding how the call stack can replace iterative loops.

## 🔹 Key Observations & Intuition

  * **State Compression:** In recursion, the outer loop is replaced by the function call itself, where the size of the array effectively "shrinks" in each call.
  * **Base Case:** The recursion stops when the array size becomes 1 (as a single element is already sorted).
  * **Work per Call:** Each call performs one "pass" of the sort (bubbling the max or inserting the element) and then delegates the rest of the array to the next recursive call.

-----

## 🔹 Approaches

### 🔸 Recursive Bubble Sort

**Idea:**

1.  **Base Case:** If $n == 1$, return.
2.  **One Pass:** Iterate through the array once and swap adjacent elements to push the maximum to the end.
3.  **Recurse:** Call the function for $n-1$ elements.

**Time & Space Complexity:**

  * **Time Complexity:** $O(N^2)$ (Worst/Average); $O(N)$ (Best case with optimization).
  * **Space Complexity:** $O(N)$ due to the auxiliary recursion stack.

**Java Code (Exactly as on website):**

```java
import java.util.*;

public class Main {
    static void bubble_sort(int[] arr, int n) {
        // Base Case: range == 1.
        if (n == 1) return;

        for (int j = 0; j <= n - 2; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }

        //After 1 iteration, the last element is at its correct position
        //So, reduce the range and call the function again.
        bubble_sort(arr, n - 1);
    }
    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using Bubble Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
        bubble_sort(arr, n);
        System.out.println("After Using Bubble Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```

-----

### 🔸 Recursive Insertion Sort

**Idea:**

1.  **Base Case:** If $i == n$, return.
2.  **Insert:** Take the element at index $i$ and place it in its correct position in the sorted part ($0$ to $i-1$) using a `while` loop.
3.  **Recurse:** Call the function for index $i+1$.

**Complexity:**

  * **Time Complexity:** $O(N^2)$ (Worst); $O(N)$ (Best).
  * **Space Complexity:** $O(N)$ (Stack space).

**Java Code (Exactly as on website):**

```java
import java.util.*;

public class Main {
    static void insertion_sort(int[] arr, int i, int n) {

        // Base Case: i == n.
        if (i == n) return;

        int j = i;
        while (j > 0 && arr[j - 1] > arr[j]) {
            int temp = arr[j - 1];
            arr[j - 1] = arr[j];
            arr[j] = temp;
            j--;
        }

        insertion_sort(arr, i + 1, n);

    }

    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();

        insertion_sort(arr, 0, n);

        System.out.println("After insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```

-----

## 🔹 Edge Cases

  * **$n=0$ or $n=1$:** The base cases handle these immediately.
  * **Stack Overflow:** For very large $N$ (e.g., $10^5$), recursive sorts will throw a `StackOverflowError` in Java, unlike their iterative counterparts.

-----

## 🔹 Important Notes / Takeaways

  * **Recursion vs. Iteration:** While these recursive versions don't improve time complexity, they are excellent for practicing recursion logic.
  * **Optimization:** Just like iterative Bubble Sort, you can add a `swapped` check in Recursive Bubble Sort to achieve $O(N)$ best-case time.
  * **Key Difference:** Iterative sorting uses $O(1)$ space, while Recursive sorting uses $O(N)$ space due to the stack.

-----

## 🔹 Complexity Summary Table

| Algorithm | Best Case (Time) | Worst Case (Time) | Space (Stack) |
| :--- | :--- | :--- | :--- |
| **Recursive Bubble** | $O(N)$ (if optimized) | $O(N^2)$ | $O(N)$ |
| **Recursive Insertion** | $O(N)$ | $O(N^2)$ | $O(N)$ |

---
Q6

# Recursive Insertion Sort 

## 🔹 Problem Summary
**Recursive Insertion Sort** is a variation of the standard Insertion Sort that uses recursion instead of an outer loop. The algorithm picks an element and places it in its correct position among the already sorted part of the array, repeating this process until the entire array is sorted.

## 🔹 Key Observations & Intuition
* **Recursive Structure:** Each recursive call represents one "pass" of the sort. The base case stops the recursion when we have processed all elements.
* **Building the Sorted Part:** The algorithm assumes the first $i$ elements are sorted and then takes the $(i+1)^{th}$ element to insert it into the correct position.
* **The "Shift" Logic:** Inside each recursive call, a `while` loop (or another recursion) shifts elements to the right to make space for the current element.

---

## 🔹 Approaches

### 🔸 Optimal Approach (Recursive)

**Detailed Explanation:**
1.  **Base Case:** If the current index $i$ equals the size of the array $n$, return (the array is sorted).
2.  **Insertion Logic:**
    * Start with the element at index $i$ (let's call the pointer $j = i$).
    * While $j > 0$ and the element to the left ($arr[j-1]$) is greater than the current element ($arr[j]$), swap them.
    * Decrement $j$ to keep moving the element left until it finds its correct spot.
3.  **Recursive Step:** Call the function again for the next index $i + 1$.

**Why it is optimal:**
It performs the same number of comparisons as iterative insertion sort but demonstrates how the call stack handles the "outer loop" progression.

**Complexity:**
* **Time Complexity:** $O(N^2)$ for Worst and Average cases. $O(N)$ for the Best case (already sorted array).
* **Space Complexity:** $O(N)$ due to the auxiliary recursion stack space.

**Java Code (Exactly as on website):**
```java
import java.util.*;

public class Main {
    static void insertion_sort(int[] arr, int i, int n) {

        // Base Case: i == n.
        if (i == n) return;

        int j = i;
        while (j > 0 && arr[j - 1] > arr[j]) {
            int temp = arr[j - 1];
            arr[j - 1] = arr[j];
            arr[j] = temp;
            j--;
        }

        insertion_sort(arr, i + 1, n);

    }

    public static void main(String args[]) {
        int arr[] = {13, 46, 24, 52, 20, 9};
        int n = arr.length;
        System.out.println("Before Using insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();

        insertion_sort(arr, 0, n);

        System.out.println("After insertion sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}
```

---

## 🔹 Edge Cases
* **Already Sorted Array:** The `while` loop condition fails immediately in every call, leading to $O(N)$ time.
* **Reverse Sorted Array:** Maximum comparisons and swaps occur ($O(N^2)$).
* **Single Element Array:** The base case handles this correctly if $n=1$.

---

## 🔹 Important Notes / Takeaways
* **In-place & Stable:** Like its iterative counterpart, it is stable (maintains relative order of equal elements) and in-place (no extra temporary array).
* **Stack Depth:** In interviews, always mention that while the logic is the same, recursion introduces $O(N)$ space overhead which the iterative version ($O(1)$) does not have.
* **Recursive Bubble vs. Insertion:** In Bubble, we fix the **end** of the array first; in Insertion, we fix the **beginning** of the array first.

---

## 🔹 Complexity Summary Table

| Case | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Best Case** | $O(N)$ | $O(N)$ (Stack) |
| **Average Case** | $O(N^2)$ | $O(N)$ (Stack) |
| **Worst Case** | $O(N^2)$ | $O(N)$ (Stack) |

---
Q7
# Quick Sort 

## 🔹 Problem Summary
**Quick Sort** is a **Divide and Conquer** algorithm. It works by picking an element as a **pivot** and placing it in its correct sorted position. The array is then partitioned such that all elements smaller than the pivot are moved to its left, and all elements larger than the pivot are moved to its right. This process is then applied recursively to the subarrays.

## 🔹 Key Observations & Intuition
* **Pivot Selection:** While any element can be a pivot (first, last, middle, or random), this implementation typically selects the **first element** of the range.
* **The Core Task:** Unlike Merge Sort which divides first and merges later, Quick Sort does the work of "placing" the pivot first and then divides. 
* **Partitioning:** The `partition` function is the engine of the algorithm. It returns the index where the pivot is finally placed (`pIndex`).

---

## 🔹 Approaches

### 🔸 Optimal Approach (Recursive Quick Sort)

**Idea:**
1.  **Pick a Pivot:** Select the first element of the array/subarray.
2.  **Two Pointers:** Use two pointers, `i` starting from the left and `j` starting from the right.
    * Move `i` forward until you find an element **greater** than the pivot.
    * Move `j` backward until you find an element **smaller** than or equal to the pivot.
    * Swap `arr[i]` and `arr[j]` if `i < j`.
3.  **Place Pivot:** Once `i` and `j` cross, swap the pivot (`arr[low]`) with `arr[j]`.
4.  **Recurse:** Call the function for the left part (`low` to `j-1`) and the right part (`j+1` to `high`).

**Why it is optimal:**
It is an **in-place** sorting algorithm (unlike Merge Sort, which requires $O(N)$ extra space). It is generally faster in practice due to its $O(N \log N)$ average case performance and lower constant factors.

**Complexity:**
* **Time Complexity:** * **Best & Average Case:** $O(N \log N)$
    * **Worst Case:** $O(N^2)$ (occurs when the array is already sorted and the pivot is always the smallest or largest element).
* **Space Complexity:** $O(1)$ auxiliary space (ignoring the $O(N)$ recursive stack space).

**Java Code (Exactly as on website):**
```java
import java.util.*;

class Solution {
    static int partition(List<Integer> arr, int low, int high) {
        int pivot = arr.get(low);
        int i = low;
        int j = high;

        while (i < j) {
            while (arr.get(i) <= pivot && i <= high - 1) {
                i++;
            }

            while (arr.get(j) > pivot && j >= low + 1) {
                j--;
            }
            if (i < j) {
                int temp = arr.get(i);
                arr.set(i, arr.get(j));
                arr.set(j, temp);
            }
        }
        int temp = arr.get(low);
        arr.set(low, arr.get(j));
        arr.set(j, temp);
        return j;
    }

    static void qs(List<Integer> arr, int low, int high) {
        if (low < high) {
            int pIndex = partition(arr, low, high);
            qs(arr, low, pIndex - 1);
            qs(arr, pIndex + 1, high);
        }
    }
    public static List<Integer> quickSort(List<Integer> arr) {
        // Write your code here.
        qs(arr, 0, arr.size() - 1);
        return arr;
    }
}

public class Main {
    public static void main(String args[]) {
        List<Integer> arr = new ArrayList<>();
        arr = Arrays.asList(new Integer[] {4, 6, 2, 5, 7, 9, 1, 3});
        int n = arr.size();
        System.out.println("Before Using quick Sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr.get(i) + " ");
        }
        System.out.println();
        arr = Solution.quickSort(arr);
        System.out.println("After quick sort: ");
        for (int i = 0; i < n; i++) {
            System.out.print(arr.get(i) + " ");
        }
        System.out.println();
    }
}
```

---

## 🔹 Edge Cases
* **Already Sorted Array:** Without a random pivot, this leads to the $O(N^2)$ worst case.
* **Array with all same elements:** The code handles this via the `<=` check in the partition logic.
* **Array with only 1 element:** Handled by the base case `if (low < high)`.

---

## 🔹 Important Notes / Takeaways
* **Unstable Sort:** Quick Sort is **not stable**; the relative order of equal elements may not be preserved.
* **Space Advantage:** Preferred over Merge Sort when memory is limited.
* **Pivot Logic:** In competitive programming, picking a random pivot or the median-of-three can prevent the $O(N^2)$ worst case.

---

## 🔹 Complexity Summary Table

| Case | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Best Case** | $O(N \log N)$ | $O(\log N)$ (Stack) |
| **Average Case** | $O(N \log N)$ | $O(\log N)$ (Stack) |
| **Worst Case** | $O(N^2)$ | $O(N)$ (Stack) |

---

