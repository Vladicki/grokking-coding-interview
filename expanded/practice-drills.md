# Practice Drills

Use these for recognition practice. Hide the answer line first. Say the pattern and the cue before thinking about code.

## Warmup recognition

| Prompt | Pattern | Cue |
|---|---|---|
| Given a sorted array, find two values that add to a target. | Two Pointers | sorted plus pair sum |
| Given an unsorted array, find two indices whose values add to a target. | Hash Maps | unsorted lookup for complement |
| Find the longest substring with no repeated character. | Sliding Window | contiguous substring plus longest valid range |
| Merge all overlapping meeting times. | Merge Intervals | ranges and overlap |
| Find one duplicate in numbers from `1..n`. | Cyclic Sort | dense range plus duplicate |
| Reverse nodes from position `p` to `q` in a linked list. | In-place Reversal | linked list partial reverse |
| Check whether parentheses are balanced. | Stacks | nesting and matching |
| For each day, find the next warmer day. | Monotonic Stack | next greater to the right |
| Group words that are anagrams. | Hash Maps / Counting | group by character counts |
| Return nodes level by level from a binary tree. | Tree Level Order Traversal | per-level output |
| Count paths from root to leaf with a given sum. | Tree DFS | root-to-leaf path |
| Find whether city A can reach city B by roads. | Graphs | reachability over edges |
| Count islands in a grid. | Island Traversal | connected components in matrix |
| Maintain median as numbers arrive. | Two Heaps | stream median |
| Generate all subsets of a small list. | Subsets | all possible subsets |
| Search a rotated sorted array in `O(log n)`. | Modified Binary Search | rotated sorted plus logarithmic |
| Find the only integer not appearing twice. | Bitwise XOR | pairs cancel, O(1) space |
| Return K most frequent numbers. | Top K Elements | K best by frequency |
| Merge K sorted linked lists. | K-way Merge | many sorted inputs |
| Pick maximum number of non-overlapping intervals. | Greedy / Merge Intervals | scheduling by earliest finish |
| Partition an array into two equal-sum subsets. | 0/1 Knapsack | choose subset to hit target |
| Count ways to climb stairs taking 1 or 2 steps. | Fibonacci DP | state depends on previous states |
| Find longest palindromic subsequence. | Palindromic Subsequence DP | palindrome plus skipping allowed |
| Solve N-Queens. | Backtracking | build valid board with pruning |
| Implement autocomplete by prefix. | Trie | repeated prefix lookup |
| Find a valid order for courses with prerequisites. | Topological Sort | directed dependencies |
| Count connected components as edges are added. | Union Find | dynamic connectivity |
| Book calendar intervals with predecessor and successor checks. | Ordered Set | nearest neighbors in changing sorted set |
| Count subarrays with sum K. | Prefix Sum | subarray sum count |
| Print `foo` then `bar` from different threads. | Multi-threaded | thread ordering |
| Count anagrams in a sliding string window. | Counting / Sliding Window | frequency in window |
| Return max for every window of size K. | Monotonic Queue | sliding window extreme |
| Simulate robot movement commands. | Simulation | direct process rules |
| Sort colors `0`, `1`, `2`. | Linear Sorting / Two Pointers | tiny integer range |
| Subset sum with `n = 40` and huge values. | Meet in the Middle | too large for `2^n`, values too big for DP |
| Answer many offline range frequency queries on static array. | Mo's Algorithm | offline static range queries |
| Encode and decode a binary tree. | Serialize and Deserialize | store and rebuild structure |
| Deep copy graph with cycles. | Clone | deep copy plus cycles |
| Find critical connections in network. | Articulation Points and Bridges | removing an edge disconnects graph |
| Range minimum query with updates. | Segment Tree | changing array plus range aggregate |
| Count smaller numbers after self. | Binary Indexed Tree | dynamic prefix counts over ranks |

## Drill set A: similar-looking prompts

### A1

You need the longest substring with at most two distinct characters.

**Answer.** Sliding Window. Contiguous substring, longest, at most K distinct.

### A2

You need the longest subsequence where adjacent chosen numbers differ by at most one.

**Answer.** Not sliding window by default. Subsequence is not contiguous. Look for DP, counting, or sorting depending on constraints.

### A3

You need a pair of values in a sorted array that sum to target.

**Answer.** Two Pointers. Sorted pair sum gives a direction rule.

### A4

You need a pair of original indices in an unsorted array that sum to target.

**Answer.** Hash Maps. Preserve indices and lookup complement.

### A5

You need a shortest path in an unweighted grid maze.

**Answer.** BFS through grid, under Island / Matrix Traversal or Graphs. Shortest unweighted path means level-order expansion.

### A6

You need any path from start to end in a maze.

**Answer.** DFS or BFS graph traversal. Shortest is not required.

### A7

You need all valid paths from start to end in a small maze.

**Answer.** Backtracking. Generate all configurations or paths.

### A8

You need to know whether all tasks can be scheduled with prerequisites.

**Answer.** Topological Sort. Directed dependency cycle detection.

### A9

You need to know whether two users are in the same friend group after many friendship additions.

**Answer.** Union Find. Dynamic connectivity.

### A10

You need to find next greater element for every item.

**Answer.** Monotonic Stack. Nearest greater relation.

## Drill set B: constraints as clues

### B1

`n <= 10^5`, array unsorted, return whether duplicates exist.

**Answer.** Hash Set / Hash Maps. O(n) expected time.

### B2

`n <= 10^5`, array sorted, return pair sum.

**Answer.** Two Pointers. O(n) and O(1) space.

### B3

`n <= 20`, generate all subsets.

**Answer.** Subsets / Backtracking. Output itself is exponential.

### B4

`n <= 40`, choose subset closest to target, values up to `10^9`.

**Answer.** Meet in the Middle. DP over sum impossible, full enumeration too large.

### B5

`n <= 10^5`, `q <= 10^5`, static array, many range sum queries.

**Answer.** Prefix Sum. O(n) preprocess, O(1) query.

### B6

`n <= 10^5`, `q <= 10^5`, point updates and range sum queries.

**Answer.** Binary Indexed Tree or Segment Tree. Dynamic prefix or range query.

### B7

`n <= 10^5`, values in `0..100` need sorted output.

**Answer.** Counting Sort / Linear Sorting. Small value range.

### B8

`n <= 10^5`, find median after every insertion.

**Answer.** Two Heaps. Dynamic median.

### B9

`n <= 10^5`, return K largest, K is 10.

**Answer.** Top K Elements. Heap of size K.

### B10

`n <= 10^5`, many queries for distinct count in `[l,r]`, array static, offline allowed.

**Answer.** Mo's Algorithm or Fenwick with offline sorting, depending on query type. The phrase offline range queries is the clue.

## Drill set C: say the invariant

For each prompt, answer with pattern and invariant.

1. Smallest subarray with sum at least S.
   - Pattern: Sliding Window.
   - Invariant: window sum equals the values between `start` and `end`; shrink while valid.

2. Merge K sorted streams.
   - Pattern: K-way Merge.
   - Invariant: heap holds the next unconsumed item from each stream.

3. Count connected components in an undirected graph.
   - Pattern: Graphs or Union Find.
   - Invariant for DFS/BFS: every visited node belongs to exactly one counted component.
   - Invariant for Union Find: each node's representative identifies its component.

4. Lowest common ancestor in binary tree.
   - Pattern: Tree DFS.
   - Invariant: each recursive call returns whether its subtree contains either target, or the ancestor if already found.

5. Copy linked list with random pointers.
   - Pattern: Clone.
   - Invariant: map from original node to clone is reused for `next` and `random` links.

6. Range max query with point updates.
   - Pattern: Segment Tree.
   - Invariant: every segment node stores max for its interval.

7. Search first bad version.
   - Pattern: Modified Binary Search.
   - Invariant: first bad version remains in the active interval.

8. Course order from alien dictionary words.
   - Pattern: Topological Sort.
   - Invariant: zero-indegree letters have no remaining prerequisites.

9. N-Queens placements.
   - Pattern: Backtracking.
   - Invariant: current board has no attacking queens.

10. Longest palindromic subsequence.
    - Pattern: Palindromic Subsequence DP.
    - Invariant: `dp[l][r]` is correct for the substring `s[l:r+1]` once shorter ranges are known.

## Drill set D: common misreads

| If you see | Do not assume | Check instead |
|---|---|---|
| `substring` | subsequence DP | substring is contiguous, often sliding window |
| `subsequence` | sliding window | subsequence can skip, often DP/backtracking/greedy |
| `sorted` | always binary search | pair/triplet often two pointers |
| `tree` | always DFS | shortest/minimum depth/per-level often BFS |
| `graph` | always BFS | dependency order needs topological sort, dynamic connectivity needs union find |
| `K` | always heap | K distinct in a substring is sliding window |
| `range query` | always prefix sum | updates need Fenwick or segment tree |
| `all possible` | DP | if output lists every configuration, use subsets/backtracking |
| `minimum` | greedy | prove local choice, else DP/BFS/binary search may fit |
| `frequency` | counting only | frequency plus top K needs heap, frequency plus window needs sliding window |
