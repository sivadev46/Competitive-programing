# Design and Analysis of Algorithms - Competitive Programming

This repository contains verified C language solutions for fundamental algorithmic problems focusing on optimizing **Time Complexity** and **Space Complexity**. The solutions cover duplicate detection, array intersections, and target pair variance techniques.

---

## 🚀 Problems Overview & Complexity Matrix

| Problem ID | Problem Statement | Optimization Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Question 1** | Find Duplicate in Array | Brute Force (Nested Loops) | $O(n^2)$ | $O(1)$ |
| **Question 2** | Find Duplicate in Array | Floyd's Tortoise and Hare (Cycle Detection) | $O(n)$ | $O(1)$ |
| **Question 3** | Intersection of 2 Sorted Arrays | Brute Force (Nested Loops) | $O(m \times n)$ | $O(1)$ |
| **Question 4** | Intersection of 2 Sorted Arrays | Two-Pointer Approach | $O(m + n)$ | $O(1)$ |
| **Question 5** | Pair with Given Difference | Brute Force Check | $O(n^2)$ | $O(1)$ |
| **Question 6** | Pair with Given Difference | Optimized Pointer Window | $O(n)$ | $O(1)$ |

---

## 🛠️ Detailed Implementations

### Question 1: Finding Duplicates — $O(n^2)$ Time, $O(1)$ Space
Given a read-only array of $n$ integers between $1$ and $n$, find one number that repeats by comparing every element with all subsequent elements.

```c
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);
    int a[n];

    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }

    // Compare every element with the elements after it
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (a[i] == a[j]) {
                printf("%d", a[i]);
                return 0;
            }
        }
    }
    return 0;
}
```

### Question 2: Finding Duplicates — $O(n)$ Time, $O(1)$ Space
An optimized version utilizing **Floyd's Cycle Detection algorithm** (pointer tracking) to find the repeating integer within linear time without modifying the read-only constraints.

```c
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);
    int a[n];

    for (int i = 0; i < n; i++)
        scanf("%d", &a[i]);

    int slow = a[0];
    int fast = a[0];

    do {
        slow = a[slow];
        fast = a[a[fast]];
    } while (slow != fast);

    slow = a[0];
    while (slow != fast) {
        slow = a[slow];
        fast = a[fast];
    }

    printf("%d", slow);
    return 0;
}
```

### Question 3: Intersection of 2 Sorted Arrays — $O(m \times n)$ Time, $O(1)$ Space
Find elements common to two sorted arrays by matching every element of the first array exhaustively across the second array.

```c
#include <stdio.h>

int main() {
    int T;
    scanf("%d", &T);

    while (T--) {
        int m, n;
        scanf("%d", &m);
        int a[m];
        for (int i = 0; i < m; i++)
            scanf("%d", &a[i]);

        scanf("%d", &n);
        int b[n];
        for (int i = 0; i < n; i++)
            scanf("%d", &b[i]);

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (a[i] == b[j]) {
                    printf("%d ", a[i]);
                    break;
                }
            }
        }
        printf("\n");
    }
    return 0;
}
```

### Question 4: Intersection of 2 Sorted Arrays — $O(m + n)$ Time, $O(1)$ Space
An optimized linear scanning algorithm leveraging a **Two-Pointer technique** to seamlessly crawl through both sorted arrays simultaneously.

```c
#include <stdio.h>

int main() {
    int T;
    scanf("%d", &T);

    while (T--) {
        int m, n;
        scanf("%d", &m);
        int a[m];
        for (int i = 0; i < m; i++)
            scanf("%d", &a[i]);

        scanf("%d", &n);
        int b[n];
        for (int i = 0; i < n; i++)
            scanf("%d", &b[i]);

        int i = 0, j = 0;
        while (i < m && j < n) {
            if (a[i] == b[j]) {
                printf("%d ", a[i]);
                i++;
                j++;
            } else if (a[i] < b[j]) {
                i++;
            } else {
                j++;
            }
        }
        printf("\n");
    }
    return 0;
}
```

### Question 5: Pair with Given Difference — $O(n^2)$ Time, $O(1)$ Space
Checks whether a pair of indices $(i, j)$ exists such that $A[j] - A[i] = k$ (where $i \neq j$) using standard nested loops.

```c
#include <stdio.h>

int main() {
    int n, k;
    scanf("%d", &n);
    int a[n];

    for (int i = 0; i < n; i++)
        scanf("%d", &a[i]);

    scanf("%d", &k);

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i != j && a[j] - a[i] == k) {
                printf("1");
                return 0;
            }
        }
    }
    printf("0");
    return 0;
}
```

### Question 6: Pair with Given Difference — $O(n)$ Time, $O(1)$ Space
*(Note: To achieve true $O(n)$ optimization on a sorted array, implement this two-pointer window setup to avoid redundant iterations).*

```c
#include <stdio.h>

int main() {
    int n, k;
    scanf("%d", &n);
    int a[n];

    for (int i = 0; i < n; i++)
        scanf("%d", &a[i]);

    scanf("%d", &k);

    int i = 0, j = 1;
    while (i < n && j < n) {
        if (i != j && a[j] - a[i] == k) {
            printf("1");
            return 0;
        } else if (a[j] - a[i] < k) {
            j++;
        } else {
            i++;
        }
    }
    printf("0");
    return 0;
}
```

---

## 📋 Compilation & Execution

Use a standard C compiler (like `gcc`) to run any of the file samples:

```bash
# Compile the target file
gcc question2.c -o solution

# Execute and pipe inputs
./solution
```
