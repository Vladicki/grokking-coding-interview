# Worked Examples

Original examples that show how to turn a problem statement into a pattern choice. These are approach-level walkthroughs, not copied course solutions.

## 1. Pair with target sum

**Problem shape.** Given an array and a target, return two numbers or indices whose values add to the target.

**Pattern choice.** If the array is unsorted and indices must be preserved, use a [hash map](../patterns/hash-maps.md). If the array is sorted, use [two pointers](../patterns/two-pointers.md).

**Example.** `nums = [4, 1, 9, 7]`, `target = 8`.

**Walkthrough.**

1. Read `4`. Need `4`, not seen yet. Store `4 -> index 0`.
2. Read `1`. Need `7`, not seen yet. Store `1 -> index 1`.
3. Read `9`. Need `-1`, not seen yet. Store `9 -> index 2`.
4. Read `7`. Need `1`, which is already stored. Return indices `1` and `3`.

**Invariant.** The map contains all earlier values and their usable positions.

**Why not sorting?** Sorting loses original indices unless you carry them with each value. If the problem asks only for values, sorting may be fine.

## 2. Remove duplicates from sorted array

**Problem shape.** Given a sorted array, rewrite it in place so each value appears once, and return the length of the unique prefix.

**Pattern choice.** [Two pointers](../patterns/two-pointers.md). One pointer scans, the other marks where the next unique value should be written.

**Example.** `[1, 1, 2, 2, 3]`.

**Walkthrough.**

1. Keep `write = 1`, because the first value is already unique.
2. Scan from index `1`.
3. Skip `1`, because it equals the previous value.
4. See `2`, write it at index `1`, move `write` to `2`.
5. Skip the second `2`.
6. See `3`, write it at index `2`, move `write` to `3`.
7. The unique prefix is `[1, 2, 3]`.

**Invariant.** Everything before `write` is the compacted unique prefix.

## 3. Longest substring without repeating characters

**Problem shape.** Find the longest contiguous substring where each character appears at most once.

**Pattern choice.** [Sliding window](../patterns/sliding-window.md). Contiguous substring plus longest valid range is the signal.

**Example.** `abcaef`.

**Walkthrough.**

1. Grow right while characters are new: `a`, `ab`, `abc`.
2. Add another `a`. The window is invalid.
3. Move left until the previous `a` leaves. The window becomes `bca`.
4. Continue with `e`, `f`, reaching `bcaef` length `5`.

**Invariant.** The window contains no duplicate characters after the shrink loop finishes.

**Common variation.** Instead of moving left one step at a time, store the last index of each character and jump left forward.

## 4. Minimum window containing all pattern characters

**Problem shape.** Find the shortest substring of a string that contains every character from a pattern, including duplicates.

**Pattern choice.** [Sliding window](../patterns/sliding-window.md) with a frequency map.

**Example.** String `ADOBECODEBANC`, pattern `ABC`. The answer is `BANC`.

**Walkthrough.**

1. Count required characters: `A:1`, `B:1`, `C:1`.
2. Grow right until all required counts are satisfied.
3. Once valid, shrink left while the window stays valid.
4. Record the shortest valid window seen during shrinking.
5. If removing a required character makes its count unsatisfied, stop shrinking and grow again.

**Invariant.** `matched` tells how many distinct required characters currently meet their required counts.

**Trap.** A set is not enough when the pattern has repeated characters, such as `AABC`.

## 5. Merge meeting times

**Problem shape.** Given intervals, combine all overlapping intervals.

**Pattern choice.** [Merge intervals](../patterns/merge-intervals.md). Sort by start, then sweep.

**Example.** `[[1,4], [2,5], [7,9], [8,10]]`.

**Walkthrough.**

1. Sort by start. The example is already sorted.
2. Start current interval as `[1,4]`.
3. `[2,5]` overlaps, so current becomes `[1,5]`.
4. `[7,9]` does not overlap, so output `[1,5]` and start `[7,9]`.
5. `[8,10]` overlaps, so current becomes `[7,10]`.
6. Output the final current interval.

**Invariant.** The current interval is the merged form of all overlapping intervals in the active block.

## 6. Minimum meeting rooms

**Problem shape.** Given meeting intervals, return the minimum number of rooms needed so no meetings in the same room overlap.

**Pattern choice.** [Merge intervals](../patterns/merge-intervals.md) plus a min-heap of ending times.

**Example.** `[[1,4], [2,5], [7,9]]` needs `2` rooms.

**Walkthrough.**

1. Sort meetings by start time.
2. Keep a min-heap of end times for rooms currently in use.
3. Before placing a meeting, remove every room whose end time is not greater than the new start.
4. Add the new meeting end time.
5. The largest heap size seen is the number of rooms required.

**Invariant.** The heap contains exactly the meetings that are active at the current start time.

## 7. Linked list cycle

**Problem shape.** Determine whether a linked list contains a cycle without extra memory.

**Pattern choice.** [Fast and slow pointers](../patterns/fast-and-slow-pointers.md).

**Example.** `1 -> 2 -> 3 -> 4 -> 2`.

**Walkthrough.**

1. Slow moves one step, fast moves two.
2. If fast reaches `None`, no cycle exists.
3. If slow and fast meet, a cycle exists.

**Invariant.** In an acyclic list, fast eventually reaches the end. In a cyclic list, fast eventually catches slow inside the loop.

## 8. Number of islands

**Problem shape.** Count connected groups of land cells in a grid.

**Pattern choice.** [Island matrix traversal](../patterns/island-matrix-traversal.md), which is graph traversal on a grid.

**Example.**

```text
1 1 0
0 1 0
1 0 1
```

With 4-directional neighbors, there are `3` islands.

**Walkthrough.**

1. Scan the grid.
2. When an unvisited land cell appears, count one new island.
3. DFS or BFS from that cell, marking every connected land cell visited.
4. Continue scanning.

**Invariant.** Every visited land cell belongs to exactly one already-counted island.

**Trap.** Diagonal cells count only if the problem says 8-directional adjacency.

## 9. Daily temperatures

**Problem shape.** For each day, return how many days until a warmer temperature.

**Pattern choice.** [Monotonic stack](../patterns/monotonic-stack.md). The phrase "next warmer" is next greater element.

**Example.** `[73, 74, 71, 76]` gives `[1, 2, 1, 0]`.

**Walkthrough.**

1. Store indices on a decreasing stack of temperatures.
2. Read `74`, which is warmer than `73`, so pop index `0` and answer `1`.
3. Read `71`, not warmer than `74`, so push it.
4. Read `76`, pop `71` and answer `1`, then pop `74` and answer `2`.
5. Any index left in the stack has no warmer future day.

**Invariant.** Stack indices are waiting for a warmer value to their right.

## 10. Find median from a stream

**Problem shape.** Numbers arrive over time, and after each insertion you need the median.

**Pattern choice.** [Two heaps](../patterns/two-heaps.md).

**Example.** Stream `5, 2, 8, 1`.

**Walkthrough.**

1. Insert `5`. Median is `5`.
2. Insert `2`. Lower half is `[2]`, upper half is `[5]`, median is `(2 + 5) / 2`.
3. Insert `8`. Upper half has `[5, 8]`, lower has `[2]`, median is `5`.
4. Insert `1`. Rebalance to two and two, median is `(2 + 5) / 2`.

**Invariant.** Lower half has the largest small value available at its root. Upper half has the smallest large value available at its root.

## 11. Course schedule

**Problem shape.** Given courses and prerequisites, decide whether all courses can be finished.

**Pattern choice.** [Topological sort](../patterns/topological-sort.md). Prerequisites form a directed graph.

**Example.** `A -> B`, `B -> C` can finish as `A, B, C`. `A -> B`, `B -> A` cannot.

**Walkthrough.**

1. Build adjacency lists and indegree counts.
2. Put every course with indegree zero into a queue.
3. Repeatedly take one course, count it, and decrement indegree of courses depending on it.
4. Any course whose indegree becomes zero enters the queue.
5. If the count equals the number of courses, the schedule is possible. Otherwise a cycle remains.

**Invariant.** The queue contains courses whose prerequisites are already satisfied.

## 12. Subarray sum equals K

**Problem shape.** Count contiguous subarrays whose sum equals a target.

**Pattern choice.** [Prefix sum](../patterns/prefix-sum.md) with a hash map of prefix frequencies.

**Example.** `nums = [1, 2, 1, 2]`, `k = 3` gives `3`: `[1,2]`, `[2,1]`, `[1,2]`.

**Walkthrough.**

1. Maintain running prefix sum.
2. A subarray ending here sums to `k` when an earlier prefix equals `current_sum - k`.
3. Add the number of earlier prefixes with that value to the answer.
4. Store the current prefix sum frequency.

**Invariant.** The map counts prefix sums that occurred before the current position.

**Trap.** Initialize prefix frequency with `0: 1`, so subarrays starting at index `0` are counted.

## 13. K closest points to origin

**Problem shape.** Return the K points with the smallest distance to the origin.

**Pattern choice.** [Top K elements](../patterns/top-k-elements.md).

**Example.** Points `(1,1)`, `(3,3)`, `(0,2)`, K `2`. Distances squared are `2`, `18`, `4`, so return `(1,1)` and `(0,2)`.

**Walkthrough.**

1. Use squared distance. No square root is needed because ordering is the same.
2. Keep a max-heap of size K.
3. If a new point is closer than the farthest point in the heap, replace the farthest.
4. At the end, the heap contains the K closest points.

**Invariant.** The heap stores the best K points seen so far.

## 14. Search in rotated sorted array

**Problem shape.** Find a target in a sorted array that has been rotated.

**Pattern choice.** [Modified binary search](../patterns/modified-binary-search.md).

**Example.** `[6, 7, 1, 2, 3, 4, 5]`, target `3`.

**Walkthrough.**

1. Pick the middle.
2. At least one side of the midpoint is sorted.
3. Check whether the target lies inside the sorted side.
4. Keep that side if it does, otherwise keep the other side.
5. Repeat until found or empty.

**Invariant.** The target, if present, remains inside the current search range.

## 15. Clone graph

**Problem shape.** Return a deep copy of a graph where nodes point to neighbors.

**Pattern choice.** [Clone](../patterns/clone.md) plus graph traversal.

**Example.** Node `1` connected to `2`, and `2` connected back to `1`.

**Walkthrough.**

1. Create a map from original node to cloned node.
2. Start from the given node, create its clone, and store the mapping.
3. Traverse neighbors. If a neighbor has no clone yet, clone it and continue traversal.
4. Add cloned neighbors to the cloned node's neighbor list.

**Invariant.** Each original node has exactly one clone, reused wherever that original is referenced.

**Trap.** A graph can cycle, so recursive cloning without a visited map does not terminate.
