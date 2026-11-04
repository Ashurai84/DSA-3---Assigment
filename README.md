# Data Structures & Algorithms - Assignment 3

A collection of classic and advanced Data Structures and Algorithms problems implemented in modern C++. Each solution is fully self-contained, including optimized algorithmic logic, robust edge-case handling, and interactive test cases in `main()`.

---

## 📌 Problem Directory & Complexity Overview

| # | Problem | Primary Concept | File | Time Complexity | Space Complexity |
|---|---------|-----------------|------|-----------------|------------------|
| 1 | **Count of Smaller Numbers After Self** | Divide & Conquer / Merge Sort | [`Count_of_Smaller_Numbers_After_Self.cpp`](./Count_of_Smaller_Numbers_After_Self.cpp) | $\mathcal{O}(N \log N)$ | $\mathcal{O}(N)$ |
| 2 | **Course Schedule** | Graph / DFS Cycle Detection | [`Course_Schedule.cpp`](./Course_Schedule.cpp) | $\mathcal{O}(V + E)$ | $\mathcal{O}(V)$ |
| 3 | **Edit Distance** | 2D Dynamic Programming | [`Edit_Distance.cpp`](./Edit_Distance.cpp) | $\mathcal{O}(M \times N)$ | $\mathcal{O}(M \times N)$ |
| 4 | **Find Median from Data Stream** | Heaps (Min-Heap & Max-Heap) | [`Find_Median.cpp`](./Find_Median.cpp) | Add: $\mathcal{O}(\log N)$, Median: $\mathcal{O}(1)$ | $\mathcal{O}(N)$ |
| 5 | **LRU Cache** | Doubly Linked List + Hash Map | [`LRU_Cache.cpp`](./LRU_Cache.cpp) | Get: $\mathcal{O}(1)$, Put: $\mathcal{O}(1)$ | $\mathcal{O}(\text{capacity})$ |
| 6 | **Longest Palindromic Substring** | Two Pointers (Expand from Center) | [`Longest_Palindrome_SubString.cpp`](./Longest_Palindrome_SubString.cpp) | $\mathcal{O}(N^2)$ | $\mathcal{O}(1)$ |
| 7 | **Range Sum Query - Mutable** | Segment Tree (Array-based) | [`Range_sum_query.cpp`](./Range_sum_query.cpp) | Build: $\mathcal{O}(N)$, Query/Update: $\mathcal{O}(\log N)$ | $\mathcal{O}(N)$ |
| 8 | **Reverse Linked List** | Singly Linked List (In-place) | [`reversed_linked_list.cpp`](./reversed_linked_list.cpp) | $\mathcal{O}(N)$ | $\mathcal{O}(1)$ |
| 9 | **Word Break** | 1D Dynamic Programming | [`words_break.cpp`](./words_break.cpp) | $\mathcal{O}(N \times K \times L)$ | $\mathcal{O}(N)$ |

---

## 🚀 Solutions Breakdown

### 1. Count of Smaller Numbers After Self
- **File**: `Count_of_Smaller_Numbers_After_Self.cpp`
- **Approach**: Modified Merge Sort tracking the original indices of elements using `std::iota`. During the merge phase, whenever an element from the right partition is smaller than the current left element, a running counter increments. When placing the left element, its cumulative count is updated.
- **Complexity**:
  - **Time**: $\mathcal{O}(N \log N)$
  - **Space**: $\mathcal{O}(N)$

---

### 2. Course Schedule
- **File**: `Course_Schedule.cpp`
- **Approach**: Cycle detection in a directed graph representing course prerequisites using Depth-First Search (DFS). Tracks visited states and nodes currently in the active recursion call stack (`recPath`). If a back-edge is encountered, a dependency cycle exists, rendering completion impossible.
- **Complexity**:
  - **Time**: $\mathcal{O}(V + E)$ where $V$ is number of courses and $E$ is prerequisite relationships
  - **Space**: $\mathcal{O}(V)$ for recursion stack and visited arrays

---

### 3. Edit Distance (Levenshtein Distance)
- **File**: `Edit_Distance.cpp`
- **Approach**: Tabular bottom-up Dynamic Programming computing the minimum edits (insertion, deletion, or substitution) to transform `word1` into `word2`.
  $$\text{dp}[i][j] = \begin{cases} \text{dp}[i-1][j-1] & \text{if } word1[i-1] == word2[j-1] \\ 1 + \min(\text{dp}[i-1][j], \text{dp}[i][j-1], \text{dp}[i-1][j-1]) & \text{otherwise} \end{cases}$$
- **Complexity**:
  - **Time**: $\mathcal{O}(M \times N)$
  - **Space**: $\mathcal{O}(M \times N)$

---

### 4. Find Median from Data Stream
- **File**: `Find_Median.cpp`
- **Approach**: Two-Heap design pattern balancing dynamic incoming data:
  - **Max-Heap**: Stores the smaller half of numbers.
  - **Min-Heap**: Stores the larger half of numbers.
  - Maintains size invariants such that heaps differ by at most 1 element, enabling instant $\mathcal{O}(1)$ median extraction.
- **Complexity**:
  - **Insertion (`addNum`)**: $\mathcal{O}(\log N)$
  - **Median Query (`findMedian`)**: $\mathcal{O}(1)$
  - **Space**: $\mathcal{O}(N)$

---

### 5. LRU Cache (Least Recently Used)
- **File**: `LRU_Cache.cpp`
- **Approach**: High-performance cache design combining:
  - **Doubly Linked List**: Keeps items ordered by recency with dummy head and tail nodes to achieve $\mathcal{O}(1)$ node additions and removals.
  - **Hash Map (`unordered_map`)**: Provides $\mathcal{O}(1)$ key-to-node lookup.
  - Includes explicit destructor and deletion logic to prevent memory leaks during node replacement and eviction.
- **Complexity**:
  - **`get(key)`**: $\mathcal{O}(1)$
  - **`put(key, value)`**: $\mathcal{O}(1)$
  - **Space**: $\mathcal{O}(\text{capacity})$

---

### 6. Longest Palindromic Substring
- **File**: `Longest_Palindrome_SubString.cpp`
- **Approach**: Expand Around Center algorithm. Iterates through all possible $2N - 1$ centers, expanding symmetrically outwards for both odd-length (single character center) and even-length (two identical adjacent characters) palindromes with zero dynamic heap allocations.
- **Complexity**:
  - **Time**: $\mathcal{O}(N^2)$ worst-case, very fast in practice
  - **Space**: $\mathcal{O}(1)$ auxiliary space

---

### 7. Range Sum Query - Mutable
- **File**: `Range_sum_query.cpp`
- **Approach**: Canonical array-based iterative Segment Tree of size $2N$. Leaves reside at indices $[N, 2N-1]$, while internal nodes represent interval sums. Updates and range queries traverse bottom-up toward the root.
- **Complexity**:
  - **Tree Construction**: $\mathcal{O}(N)$
  - **Point Update (`update`)**: $\mathcal{O}(\log N)$
  - **Range Query (`sumRange`)**: $\mathcal{O}(\log N)$
  - **Space**: $\mathcal{O}(N)$

---

### 8. Reverse Linked List
- **File**: `reversed_linked_list.cpp`
- **Approach**: Iterative three-pointer approach (`prev`, `curr`, `nextNode`) reversing node pointers in a single pass without allocating additional list nodes. Includes dynamic test case generator and memory cleanup utilities.
- **Complexity**:
  - **Time**: $\mathcal{O}(N)$
  - **Space**: $\mathcal{O}(1)$ in-place

---

### 9. Word Break
- **File**: `words_break.cpp`
- **Approach**: 1D Dynamic Programming where boolean entry `dp[i]` indicates whether prefix `s[0...i]` can be segmented using valid words from the dictionary. Checks suffix matches against the word dictionary whenever the preceding state `dp[i - len]` is true.
- **Complexity**:
  - **Time**: $\mathcal{O}(N \times K \times L)$ where $N$ is string length, $K$ is dictionary size, and $L$ is word length
  - **Space**: $\mathcal{O}(N)$

---

## 🛠️ How to Compile & Run

Any modern C++ compiler supporting C++11 or higher (e.g. `g++`, `clang++`) can be used:

### Compile Individual Solution:
```bash
g++ -std=c++17 -O2 Count_of_Smaller_Numbers_After_Self.cpp -o solution
./solution
```

### Quick Run Any Program:
```bash
g++ -std=c++17 LRU_Cache.cpp && ./a.out
```

---

## 📂 Project Structure

```text
.
├── Count_of_Smaller_Numbers_After_Self.cpp
├── Course_Schedule.cpp
├── Edit_Distance.cpp
├── Find_Median.cpp
├── LRU_Cache.cpp
├── Longest_Palindrome_SubString.cpp
├── Range_sum_query.cpp
├── reversed_linked_list.cpp
├── words_break.cpp
└── README.md
```
