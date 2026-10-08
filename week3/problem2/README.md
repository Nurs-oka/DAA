# Problem 2: Linked List Cycle

## 1. Problem

The goal here is to figure out if a linked list has a loop or cycle in it. A cycle happens when you keep following the `.next` pointers and eventually end up looping back to a node you already visited instead of reaching the end (where `next` is `null`). We just need to return `true` if there's a cycle, and `false` if it's a normal straight-line list.

## 2. Approach

To solve this efficiently without using extra memory, I used the **Tortoise and Hare (Two-Pointer)** algorithm:

1. **Edge cases:** First, I check if the list is completely empty (`head == null`) or only has one node with no loop (`head.next == null`). If so, it's impossible to have a cycle, so we return `false`.

2. **Setting up pointers:** I create two pointers, `slow` and `fast`, and set both of them to start at the `head` of the list.

3. **Moving at different speeds:** Inside a `while` loop, the `slow` pointer moves forward by **1 step** (`slow = slow.next`), while the `fast` pointer moves forward by **2 steps** (`fast = fast.next.next`).

4. **Checking for a meeting point:** If there is a cycle, the fast pointer will eventually loop around and "lap" the slow pointer, meaning `slow == fast`. When that happens, we know for sure there's a cycle and we return `true`.

5. **Reaching the end:** If there is no cycle, the `fast` pointer will eventually hit `null` at the end of the list, breaking the loop, and we return `false`.

### Trace / Example Walkthrough

Let's test it with a list like `[3, 2, 0, -4]` where the tail `-4` points back to node `2` (index 1).

* **Start:** `slow` is at `3`, `fast` is at `3`.
* **Step 1:** 
  * `slow` moves 1 step to `2`.
  * `fast` moves 2 steps to `0`.
  * Are they equal? `2 != 0`, keep going.
* **Step 2:** 
  * `slow` moves 1 step to `0`.
  * `fast` moves 2 steps: goes from `0` to `-4`, and then loops back to `2`. So `fast` is now at `2`.
  * Are they equal? `0 != 2`, keep going.
* **Step 3:** 
  * `slow` moves 1 step to `-4`.
  * `fast` moves 2 steps: goes from `2` to `0`, then to `-4`. So `fast` is now at `-4`.
  * Are they equal? `slow` and `fast` are both at `-4`! Match found!
* **Result:** Return `true`.

## 3. Time Complexity

**Time Complexity:** $O(n)$

### Explanation:

* In the worst-case scenario (with a cycle), the fast pointer goes around the cycle until it catches up to the slow pointer. 
* The number of steps depends directly on the number of nodes $n$ in the list, so the time grows linearly as the list gets bigger.

## 4. Space Complexity

**Space Complexity:** $O(1)$

### Explanation:

* We only created two pointer variables (`slow` and `fast`), which take up a constant amount of memory. 
* We didn't use any extra data structures like a HashSet to track visited nodes, so our memory usage stays at $O(1)$ constant space, matching the follow-up requirement!

## 5. Reflection / Improvement

* **Is there a more efficient approach?**
  No, $O(n)$ time and $O(1)$ space is already the optimal and standard solution for this problem. 

* **What would you need to change?**
  Alternatively, you could use a `HashSet` to store every node as you visit it. If you hit a node that is already in the set, you found a cycle. 

* **What complexity could the alternative solution achieve?**
  The HashSet approach has a time complexity of $O(n)$, but its space complexity would be $O(n)$ because you have to store every single node in the set. That's why the Two-Pointer approach is much better!