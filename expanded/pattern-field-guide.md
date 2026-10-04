# Expanded Pattern Field Guide

A field guide for the 41 coding interview patterns in this repo. Each card gives the signal, the invariant to protect while coding, a small example, and the trap that usually breaks first attempts.

## Core patterns

### 1. Two Pointers

**Read the signal.** The input is sorted, can be sorted, or asks for a pair, triplet, removal, partition, or in-place rewrite.

**Invariant.** The skipped region can never contain a better answer. On a sorted two-sum scan, if `arr[left] + arr[right]` is too small, every pair using that `left` with a smaller right is also too small, so `left` can move.

**Tiny example.** In `[-2, 1, 3, 5, 8]`, target `9`: `-2 + 8` is too small, so move left. `1 + 8` works.

**Use it for.** Pair with Target Sum, Triplet Sum to Zero, Squaring a Sorted Array, Dutch National Flag, Minimum Window Sort.

**Trap.** Do not use opposite-end pointers on unsorted input unless sorting is allowed and does not destroy required output positions.

[Pattern page](../patterns/two-pointers.md)

### 2. Fast and Slow Pointers

**Read the signal.** Linked list, cycle, middle node, kth from end, or sequence repetition with O(1) space.

**Invariant.** Fast advances farther than slow. If there is a cycle, the distance between them changes modulo the cycle length until they meet.

**Tiny example.** In `1 -> 2 -> 3 -> 4 -> 2`, slow moves one step and fast moves two. Once both enter the cycle, fast eventually lands on slow.

**Use it for.** Linked List Cycle, Start of Linked List Cycle, Middle of the Linked List, Happy Number.

**Trap.** Check `fast` and `fast.next` before advancing two steps.

[Pattern page](../patterns/fast-and-slow-pointers.md)

### 3. Sliding Window

**Read the signal.** Contiguous subarray or substring, longest, shortest, maximum, at most K, exactly K, or contains all characters.

**Invariant.** The current window summary matches exactly the elements between `start` and `end`. Every add on the right has a matching remove on the left when the window shrinks.

**Tiny example.** For smallest sum at least `8` in `[2, 1, 5, 2, 3, 2]`, grow until the sum is valid, record length, then shrink while valid.

**Use it for.** Maximum Sum Subarray of Size K, Fruits into Baskets, Smallest Window containing Substring, String Anagrams.

**Trap.** Dynamic windows usually shrink in a `while` loop, not a single `if`.

[Pattern page](../patterns/sliding-window.md)

### 4. Merge Intervals

**Read the signal.** Ranges, meetings, bookings, calendars, overlaps, conflicts, insertions, intersections, free time.

**Invariant.** After sorting by start, the merged output contains all finished intervals, and the current interval is the only one that may still absorb future intervals.

**Tiny example.** `[1,4]` followed by `[2,6]` becomes `[1,6]`. `[8,9]` starts after `6`, so it begins a new block.

**Use it for.** Merge Intervals, Insert Interval, Minimum Meeting Rooms, Employee Free Time.

**Trap.** Decide whether touching intervals like `[1,3]` and `[3,5]` overlap. The comparison changes from `<` to `<=`.

[Pattern page](../patterns/merge-intervals.md)

### 5. Cyclic Sort

**Read the signal.** Values are a dense range such as `1..n` or `0..n-1`, and a number is missing, duplicated, or misplaced.

**Invariant.** If a value belongs at an index and is not already there, swap it into place. When an index advances, it either holds the correct value or a duplicate that cannot be placed.

**Tiny example.** In `[3, 1, 2]`, value `3` belongs at index `2`, so swap to get `[2, 1, 3]`, then place `2`, then `1`.

**Use it for.** Missing Number, Find the Duplicate Number, Find all Missing Numbers, First Missing Positive.

**Trap.** After a swap, do not advance immediately. The new value at the same index may also need placement.

[Pattern page](../patterns/cyclic-sort.md)

### 6. In-place Reversal of a Linked List

**Read the signal.** Reverse a list, reverse a sub-list, reverse every K nodes, rotate, swap nodes, O(1) space.

**Invariant.** `prev` is the reversed part, `current` is the first unreversed node, and `next_node` saves the rest before rewiring.

**Tiny example.** For `1 -> 2 -> 3`, after one step `1 -> None`, `prev = 1`, `current = 2`.

**Use it for.** Reverse a Linked List, Reverse a Sub-list, Reverse Every K-element Sub-list, Reorder List.

**Trap.** Save `current.next` before assigning to it, or the rest of the list is lost.

[Pattern page](../patterns/in-place-reversal-of-a-linked-list.md)

### 7. Stacks

**Read the signal.** Nesting, matching brackets, undo, most recent item, path simplification, expression evaluation.

**Invariant.** The stack holds unfinished items in the only order that can be completed: most recent first.

**Tiny example.** For `([])`, push `(`, push `[`, see `]`, pop `[`, see `)`, pop `(`.

**Use it for.** Balanced Parentheses, Simplify Path, Min Stack, Evaluate Reverse Polish Notation.

**Trap.** Never pop before checking the stack is non-empty.

[Pattern page](../patterns/stacks.md)

### 8. Monotonic Stack

**Read the signal.** Next greater, next smaller, previous greater, nearest warmer day, stock span, histogram, trapped water.

**Invariant.** The stack is kept monotonic. When a new value breaks the order, it answers every value popped.

**Tiny example.** In temperatures `[70, 72, 71]`, `72` pops `70` and gives it answer `1` day. `71` waits.

**Use it for.** Daily Temperatures, Stock Span, Largest Rectangle in Histogram, Sum of Subarray Minimums.

**Trap.** Decide the direction first. Next greater to the right and previous greater to the left use different scans.

[Pattern page](../patterns/monotonic-stack.md)

### 9. Hash Maps

**Read the signal.** Seen before, duplicates, counts, groups by key, unsorted pair lookup, anagrams.

**Invariant.** The map summarizes exactly the useful facts about items already processed.

**Tiny example.** For two sum `[4, 7, 1]`, target `8`, when reading `1`, the complement `7` is already in the map.

**Use it for.** Two Sum, First Non-repeating Character, Group Anagrams, Longest Consecutive Sequence.

**Trap.** If positions matter, store indices, not just booleans.

[Pattern page](../patterns/hash-maps.md)

### 10. Tree Level Order Traversal

**Read the signal.** Per level output, minimum depth, nearest node, right side view, next pointer, zigzag.

**Invariant.** The queue contains exactly the next level frontier. Capture the level size before processing that level.

**Tiny example.** For root `1` with children `2` and `3`, queue starts `[1]`, then next level becomes `[2,3]`.

**Use it for.** Binary Tree Level Order Traversal, Minimum Depth, Level Averages, Right Side View.

**Trap.** If you do not freeze the level size, children get mixed into the same level as parents.

[Pattern page](../patterns/tree-level-order-traversal.md)

### 11. Tree Depth First Search

**Read the signal.** Root-to-leaf path, path sum, ancestor, subtree, height, diameter, max path.

**Invariant.** At each node, the recursive call owns the path or summary for the branch from the root to that node, or returns a summary of that node's subtree.

**Tiny example.** For path sum, subtract the node value before descending. At a leaf, check whether the remaining target is zero.

**Use it for.** Binary Tree Path Sum, Count Paths for a Sum, Tree Diameter, Lowest Common Ancestor.

**Trap.** Backtrack path lists after returning from a child, otherwise sibling branches share stale state.

[Pattern page](../patterns/tree-depth-first-search.md)

### 12. Graphs

**Read the signal.** Nodes and edges, routes, friends, networks, reachability, components, shortest hops.

**Invariant.** Every visited node is marked before its neighbors are explored, so cycles cannot cause repeated work.

**Tiny example.** In roads `A-B`, `B-C`, BFS from `A` reaches `B`, then `C`, and stops because visited blocks the return edges.

**Use it for.** Path Exists, Number of Provinces, Word Ladder, Bus Routes, Course Schedule.

**Trap.** Build the graph in the direction the problem means. Directed prerequisites are not the same as undirected friendships.

[Pattern page](../patterns/graphs.md)

### 13. Island Matrix Traversal

**Read the signal.** 2D grid, land and water, regions, flood fill, infection, rotting, maze.

**Invariant.** A visited land cell has been fully assigned to exactly one region or wave.

**Tiny example.** Counting islands: when an unvisited `1` appears, start DFS or BFS, mark all connected `1`s, and add one island.

**Use it for.** Number of Islands, Flood Fill, Rotting Oranges, Surrounded Regions, Shortest Path in Binary Matrix.

**Trap.** Clarify 4-directional versus 8-directional neighbors.

[Pattern page](../patterns/island-matrix-traversal.md)

### 14. Two Heaps

**Read the signal.** Median, middle of a stream, lower half and upper half, dynamic data with repeated middle queries.

**Invariant.** Max-heap holds the smaller half, min-heap holds the larger half, and their sizes differ by at most one.

**Tiny example.** Stream `5, 2, 8`: lower heap has `2`, upper heap has `5,8`, median is `5`.

**Use it for.** Median of a Number Stream, Sliding Window Median, Maximize Capital, Next Interval.

**Trap.** Insert and rebalance as one operation. A correct split with wrong sizes gives a wrong median.

[Pattern page](../patterns/two-heaps.md)

### 15. Subsets

**Read the signal.** Generate all subsets, permutations, combinations, all possible outputs, small input.

**Invariant.** Each partial result represents one unique set of choices made so far.

**Tiny example.** Starting with `[[]]`, add `1` to get `[[], [1]]`, then add `2` to get `[[], [1], [2], [1,2]]`.

**Use it for.** Subsets, Subsets With Duplicates, Permutations, Balanced Parentheses, Combination Sum.

**Trap.** Enumeration grows fast. If `n` is large, do not generate everything.

[Pattern page](../patterns/subsets.md)

### 16. Modified Binary Search

**Read the signal.** Sorted, rotated, peak, first or last occurrence, boundary, answer-space search, O(log n).

**Invariant.** The answer remains inside `[low, high]`, and each midpoint test discards a half that cannot contain it.

**Tiny example.** To find first true in `[False, False, True, True]`, if mid is true, keep the left half including mid.

**Use it for.** Search in Rotated Array, Ceiling of a Number, Number Range, Search in an Infinite Array.

**Trap.** Ensure the interval shrinks every loop. `low = mid` can loop forever.

[Pattern page](../patterns/modified-binary-search.md)

### 17. Bitwise XOR

**Read the signal.** Paired duplicates cancel, one single number, O(1) space with integers, bit manipulation.

**Invariant.** XOR of all processed numbers equals the XOR of the unpaired numbers seen so far.

**Tiny example.** `4 ^ 1 ^ 4` becomes `1` because `4 ^ 4 = 0`.

**Use it for.** Single Number, Two Single Numbers, Missing Number, Flip and Invert an Image.

**Trap.** XOR cancels pairs. If values appear three times, use bit counts instead.

[Pattern page](../patterns/bitwise-xor.md)

### 18. Top K Elements

**Read the signal.** K largest, K smallest, K closest, K most frequent, kth item, large input with small answer.

**Invariant.** A heap of size K holds the current best K candidates, and the root is the worst among those best candidates.

**Tiny example.** For three largest, a min-heap of size `3` discards any number less than the heap root.

**Use it for.** Top K Numbers, K Closest Points, Top K Frequent Numbers, Kth Largest in a Stream.

**Trap.** For K largest, use a min-heap of size K. For K smallest, use a max-heap of size K.

[Pattern page](../patterns/top-k-elements.md)

### 19. K-way Merge

**Read the signal.** Several sorted lists, rows, arrays, or streams must be merged or searched together.

**Invariant.** The heap contains the current smallest unconsumed item from each active sorted input.

**Tiny example.** Lists `[1,4]`, `[2,3]`: heap starts with `1` and `2`, emits `1`, then pushes `4` from the same list.

**Use it for.** Merge K Sorted Lists, Kth Smallest in Sorted Matrix, Smallest Number Range.

**Trap.** Push the next item from the same source as the popped item, not from every source.

[Pattern page](../patterns/k-way-merge.md)

### 20. Greedy Algorithms

**Read the signal.** Scheduling, assignments, limited resources, minimum moves, maximum count, an obvious local choice after sorting.

**Invariant.** The local choice leaves at least as much room for the future as any other choice.

**Tiny example.** Interval scheduling chooses the meeting that ends earliest, because it leaves the most remaining time.

**Use it for.** Non-overlapping Intervals, Assign Cookies, Jump Game, Gas Station, Remove Duplicate Letters.

**Trap.** Greedy needs a reason. If you cannot explain why the local choice is safe, it may be DP.

[Pattern page](../patterns/greedy-algorithms.md)

### 21. 0/1 Knapsack

**Read the signal.** Choose or skip each item once, under a capacity, target, or budget. Ask maximize, minimize, possible, or count ways.

**Invariant.** `dp[i][c]` or its compressed equivalent represents the best or possible result using only items processed so far.

**Tiny example.** With weights `[2,3]` and capacity `3`, item `2` fills capacity `2`, item `3` fills capacity `3`; neither can be reused.

**Use it for.** Equal Subset Sum Partition, Subset Sum, Target Sum, Minimum Subset Sum Difference.

**Trap.** In 1D 0/1 DP, iterate capacity backward so the same item is not reused.

[Pattern page](../patterns/0-1-knapsack.md)

### 22. Fibonacci Numbers DP

**Read the signal.** Position `n` depends on a fixed number of earlier positions, such as stairs, jumps, decoding, or house robber.

**Invariant.** Each state is final when computed from smaller states.

**Tiny example.** Ways to climb step `i` with 1 or 2 moves is `ways[i-1] + ways[i-2]`.

**Use it for.** Climbing Stairs, House Thief, Decode Ways, Minimum Jumps with Fee.

**Trap.** Define base cases before recurrence. Most wrong answers are off by one at `0`, `1`, or `2`.

[Pattern page](../patterns/fibonacci-numbers.md)

### 23. Palindromic Subsequence DP

**Read the signal.** Palindrome, compare a string with itself reversed, skip characters, range decisions from both ends.

**Invariant.** `dp[left][right]` answers the substring between those bounds, so smaller ranges must be ready first.

**Tiny example.** For `bbab`, if ends match, answer can include both ends plus the inside range.

**Use it for.** Longest Palindromic Subsequence, Count Palindromic Substrings, Minimum Deletions to Palindrome.

**Trap.** Subsequence and substring are different. Substrings must stay contiguous.

[Pattern page](../patterns/palindromic-subsequence.md)

### 24. Backtracking

**Read the signal.** Build a valid configuration, all solutions, puzzles, boards, partitions, placements, prune invalid partial states.

**Invariant.** The current path is valid under all constraints checked so far.

**Tiny example.** For parentheses with `n = 2`, never add `)` if it would exceed the number of `(` already placed.

**Use it for.** N-Queens, Sudoku Solver, Generate Parentheses, Word Search, Combination Sum.

**Trap.** Undo every mutation before returning to the caller.

[Pattern page](../patterns/backtracking.md)

### 25. Trie

**Read the signal.** Prefix search, dictionary, autocomplete, starts with, wildcard word search, many string lookups.

**Invariant.** Each node represents the prefix formed by the path from the root to that node.

**Tiny example.** Words `car` and `cat` share nodes for `c` and `a`, then split at `r` and `t`.

**Use it for.** Implement Trie, Search Suggestions, Word Search II, Replace Words.

**Trap.** Mark complete words separately from prefixes. Prefix `car` does not mean word `car` exists unless marked.

[Pattern page](../patterns/trie.md)

### 26. Topological Sort

**Read the signal.** Prerequisites, dependencies, build order, valid ordering, directed cycle detection.

**Invariant.** Nodes with indegree zero have no unmet prerequisites and can be safely placed next in the order.

**Tiny example.** If `A` must precede `B`, then `B` starts with indegree `1`. After placing `A`, decrement `B`.

**Use it for.** Task Scheduling, Course Schedule, Alien Dictionary, Sequence Reconstruction.

**Trap.** If the final order has fewer nodes than the graph, there is a cycle.

[Pattern page](../patterns/topological-sort.md)

### 27. Union Find

**Read the signal.** Connectivity groups change as edges are added, ask same group, number of groups, redundant connection.

**Invariant.** Every node points through parents to a representative for its current component.

**Tiny example.** Union `1-2`, union `2-3`: find of `1`, `2`, and `3` returns the same representative.

**Use it for.** Redundant Connection, Number of Provinces, Accounts Merge, Number of Islands II.

**Trap.** Without path compression and union by size or rank, worst-case chains get slow.

[Pattern page](../patterns/union-find.md)

### 28. Ordered Set

**Read the signal.** Need nearest greater or smaller value while inserting and deleting dynamically.

**Invariant.** The structure remains sorted after every update, so predecessor and successor queries are cheap.

**Tiny example.** To book `[10,20)`, find the meeting before it and after it. Only those neighbors can overlap.

**Use it for.** My Calendar, Contains Duplicate III, Sliding Window with ordered values.

**Trap.** A hash set cannot answer nearest-neighbor questions.

[Pattern page](../patterns/ordered-set.md)

### 29. Prefix Sum

**Read the signal.** Range sums, many sum queries, subarray sum equals K, pivot index, balances, fixed array.

**Invariant.** `prefix[i]` is the sum before index `i`, so range `l..r` is `prefix[r+1] - prefix[l]`.

**Tiny example.** In `[2,3,5]`, prefix is `[0,2,5,10]`; sum from index `1` to `2` is `10 - 2 = 8`.

**Use it for.** Subarray Sum Equals K, Range Sum Query Immutable, Product Except Self, Pivot Index.

**Trap.** For subarray count equals K, store frequencies of previous prefix sums, not just whether one exists.

[Pattern page](../patterns/prefix-sum.md)

### 30. Multi-threaded

**Read the signal.** Threads call methods in arbitrary order, output must be ordered, shared state must be protected.

**Invariant.** A thread may proceed only when the state says its turn or when capacity is available.

**Tiny example.** `foo` waits on a signal from `first`, then releases `bar` after printing.

**Use it for.** Print in Order, FooBar Alternately, Bounded Blocking Queue, Dining Philosophers.

**Trap.** Passing local tests without synchronization does not mean the code is safe.

[Pattern page](../patterns/multi-threaded.md)

## Advanced and specialist patterns

### 31. Counting

**Read the signal.** Frequency, occurrences, majority, anagrams, duplicates, small alphabet, count rather than position.

**Invariant.** Counts reflect exactly the current collection, window, or processed prefix.

**Tiny example.** For anagrams, two strings match if every character count matches.

**Use it for.** Majority Element, Group Anagrams, Top K Frequent Elements, Valid Anagram.

**Trap.** Remove zero counts when distinct-count logic depends on map size.

[Pattern page](../patterns/counting.md)

### 32. Monotonic Queue

**Read the signal.** Sliding window plus max or min for every window.

**Invariant.** The deque stores candidate indices in window order, and their values are monotonic. The front is the current extreme.

**Tiny example.** For window max in `[1,3,2]`, index of `1` is removed when `3` arrives because `1` can never be max later.

**Use it for.** Sliding Window Maximum, Shortest Subarray with Sum at Least K, Jump Game VI.

**Trap.** Store indices, not just values, so you can remove items that leave the window.

[Pattern page](../patterns/monotonic-queue.md)

### 33. Simulation

**Read the signal.** The statement gives process rules, constraints are small, and direct execution is acceptable.

**Invariant.** The simulated state after step `t` matches the real process after step `t`.

**Tiny example.** Robot bounded in circle: update position and direction for each command, then reason from the final state.

**Use it for.** Game of Life, Spiral Matrix, Walking Robot Simulation, Underground System.

**Trap.** Do not invent a formula when the constraints invite a direct simulation.

[Pattern page](../patterns/simulation.md)

### 34. Linear Sorting Algorithms

**Read the signal.** Integer keys in a small range, lowercase letters, digits, colors, or O(n) sorting requested.

**Invariant.** Counts or buckets preserve enough ordering information to rebuild sorted output.

**Tiny example.** Sort colors uses counts of `0`, `1`, and `2`, or three-way partitioning in one pass.

**Use it for.** Sort Colors, Relative Sort Array, Height Checker, H-Index.

**Trap.** Linear sort is only linear when the key range is not huge relative to `n`.

[Pattern page](../patterns/linear-sorting-algorithms.md)

### 35. Meet in the Middle

**Read the signal.** Subset search with `n` around 30 to 45, too large for `2^n`, values too large for knapsack DP.

**Invariant.** Every full subset is the union of one subset from the left half and one subset from the right half.

**Tiny example.** Split 40 numbers into two groups of 20, generate each side's sums, then search pairs of sums.

**Use it for.** Closest Subsequence Sum, subset sum ranges, balanced partition variants.

**Trap.** Sorting one side is what makes pair search efficient. Two unsorted sum lists still leave too much work.

[Pattern page](../patterns/meet-in-the-middle.md)

### 36. Mo's Algorithm

**Read the signal.** Many offline range queries on a static array, and the aggregate supports adding or removing one boundary item.

**Invariant.** The current maintained range and answer match the active query while pointers move one step at a time.

**Tiny example.** Reorder queries so `[L,R]` moves gradually from one query to the next instead of starting from scratch.

**Use it for.** Distinct Elements in a Subarray, Range Frequency Queries, Powerful Array.

**Trap.** Mo's algorithm is offline. If queries must be answered immediately in original order, use another structure.

[Pattern page](../patterns/mos-algorithm.md)

### 37. Serialize and Deserialize

**Read the signal.** Encode, decode, serialize, deserialize, store and restore a tree or graph.

**Invariant.** The serialized form includes enough boundaries or null markers to rebuild exactly one structure.

**Tiny example.** Preorder tree serialization needs null markers, otherwise different shapes can produce the same values.

**Use it for.** Serialize Binary Tree, Encode and Decode Strings, Verify Preorder Serialization.

**Trap.** Values alone are often not enough. Structure markers matter.

[Pattern page](../patterns/serialize-and-deserialize.md)

### 38. Clone

**Read the signal.** Deep copy, graph, random pointer, cross-links, cycles, independent copy required.

**Invariant.** The map from original node to cloned node contains exactly one clone per original node.

**Tiny example.** When cloning graph node `A`, create clone `A'`, store it, then recursively or iteratively clone neighbors.

**Use it for.** Clone Graph, Copy List with Random Pointer, Clone N-ary Tree.

**Trap.** Without the original-to-copy map, cycles recurse forever and shared nodes get duplicated incorrectly.

[Pattern page](../patterns/clone.md)

### 39. Articulation Points and Bridges

**Read the signal.** Critical connection, single point of failure, remove one edge or node, undirected network.

**Invariant.** DFS discovery time and low-link value show whether a child subtree can reach an ancestor without using the tree edge back to its parent.

**Tiny example.** If child `v` has `low[v] > disc[u]`, edge `u-v` is a bridge.

**Use it for.** Critical Connections in a Network, disconnecting grids, malware spread variants.

**Trap.** Treat the parent edge specially in undirected DFS, or every parent looks like a back edge.

[Pattern page](../patterns/articulation-points-and-bridges.md)

### 40. Segment Tree

**Read the signal.** Range queries and point or range updates, especially min, max, gcd, sum, or custom aggregates.

**Invariant.** Each tree node stores the aggregate for its interval, and parent values are recomputed from children after updates.

**Tiny example.** Updating index `5` changes leaf `5`, then every interval that contains `5` on the path to the root.

**Use it for.** Range Sum Query Mutable, Range Minimum Query, Falling Squares, My Calendar III.

**Trap.** Prefix sums handle range sums without updates. Segment trees are for changing arrays or non-reversible aggregates.

[Pattern page](../patterns/segment-tree.md)

### 41. Binary Indexed Tree

**Read the signal.** Dynamic prefix sums, point updates, inversion counts, count smaller after self, coordinate compression.

**Invariant.** Each Fenwick entry stores a fixed suffix block of a prefix determined by its lowest set bit.

**Tiny example.** To count smaller numbers to the right, scan from right to left, query how many ranks below current have appeared, then add current rank.

**Use it for.** Count of Smaller Numbers After Self, Reverse Pairs, Range Sum Query Mutable.

**Trap.** Fenwick trees are usually 1-indexed. Rank `0` breaks `i += i & -i` because it never moves.

[Pattern page](../patterns/binary-indexed-tree.md)
