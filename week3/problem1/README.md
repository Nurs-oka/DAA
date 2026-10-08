# Problem 1: Merge Two Sorted Lists

## 1. Problem

Basically, we have two linked lists that are already sorted from smallest to largest. The goal is to squish them together into one single sorted list. We aren't supposed to make brand-new nodes from scratch; we just need to rearrange the `.next` pointers so they point to each other in the correct order. If one of the lists is empty, we just return whatever is left in the other list.

## 2. Approach

To solve this, I used a loop with a helper node called a "dummy" node. Here is how it works step-by-step:

1. **Setting up:** I create a dummy node at the very beginning with a value of `-1` and a pointer called `current` pointing at it. This makes it way easier to keep track of the new list without worrying about edge cases with the head.
2. **Comparing nodes:** I run a `while` loop as long as both `list1` and `list2` still have nodes left. Inside the loop, I check whether `list1.val` or `list2.val` is smaller.
3. **Linking them:** Whichever value is smaller gets attached to `current.next`. Then I move that list's pointer forward, and also move my `current` pointer forward.
4. **Finishing up:** Once one of the lists runs out of nodes, the loop stops. Whatever is left in the other list gets attached right to the end of our new list.
5. **Returning the result:** Finally, I return `dummy.next` because that is where the actual merged list starts.

### Trace / Example Walkthrough

Let's test it with `list1 = [1, 2, 4]` and `list2 = [1, 3, 4]`.

* **Start:** `dummy` points to `-1`, `current` is at `dummy`. `list1` is at `1`, `list2` is at `1`.
* **Step 1:** `list1.val (1)` and `list2.val (1)` are the same. Let's take `list1`. `current.next` points to `1`. `list1` moves to `2`, `current` moves to `1`.
* **Step 2:** Compare `list1 (2)` and `list2 (1)`. Since `1` is smaller, we take `list2` (`1`). `current.next` points to `1`. `list2` moves to `3`, `current` moves to `1`.
* **Step 3:** Compare `list1 (2)` and `list2 (3)`. `2` is smaller, so we take `list1` (`2`). `list1` moves to `4`, `current` moves to `2`.
* **Step 4:** Compare `list1 (4)` and `list2 (3)`. `3` is smaller, so we take `list2` (`3`). `list2` moves to `4`, `current` moves to `3`.
* **Step 5:** Compare `list1 (4)` and `list2 (4)`. They are equal, so we take `list1` (`4`). `list1` becomes `null`, `current` moves to `4`.
* **End of loop:** `list1` is empty, so we just attach the rest of `list2` (which is `4`) to `current.next`.
* **Final output:** `[1, 1, 2, 3, 4, 4]`.

## 3. Time Complexity

**Time Complexity:** $O(n + m)$

### Explanation:

* Let $n$ be the length of `list1` and $m$ be the length of `list2`.
* In each turn of the loop, we check at least one node and move our pointer forward. 
* In the worst case, we have to walk through every single node in both lists until one runs out. So the number of steps depends directly on the total size of both lists combined ($n + m$).

## 4. Space Complexity

**Space Complexity:** $O(1)$

### Explanation:

* We only use a couple of pointers (`dummy` and `current`), which takes up a constant amount of memory no matter how big the input lists are.
* We aren't creating any new nodes in memory; we're just changing existing pointers around.

## 5. Reflection / Improvement

* **Is there a more efficient approach?**
  No, $O(n + m)$ is already the best we can do because you have to look at every single element at least once to merge them properly.
* **What would you need to change?**
  You could write this recursively instead of using a `while` loop. But recursion uses up extra memory on the call stack, making the space complexity $O(n + m)$ instead of $O(1)$. 
* **What complexity could the improved solution achieve?**
  The time complexity would stay the same ($O(n + m)$), but the space complexity would actually get worse because of the recursion stack. So this iterative approach is definitely the way to go.