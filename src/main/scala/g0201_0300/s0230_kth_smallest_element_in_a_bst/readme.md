[![](https://img.shields.io/github/stars/LeetCode-in-Scala/LeetCode-in-Scala?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Scala/LeetCode-in-Scala)
[![](https://img.shields.io/github/forks/LeetCode-in-Scala/LeetCode-in-Scala?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Scala/LeetCode-in-Scala/fork)

## 230\. Kth Smallest Element in a BST

Medium

Given the `root` of a binary search tree, and an integer `k`, return _the_ <code>k<sup>th</sup></code> _smallest value (**1-indexed**) of all the values of the nodes in the tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

**Input:** root = [3,1,4,null,2], k = 1

**Output:** 1 

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg)

**Input:** root = [5,3,6,2,4,null,null,1], k = 3

**Output:** 3 

**Constraints:**

*   The number of nodes in the tree is `n`.
*   <code>1 <= k <= n <= 10<sup>4</sup></code>
*   <code>0 <= Node.val <= 10<sup>4</sup></code>

**Follow up:** If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?

## Solution

```scala
import com_github_leetcode.TreeNode

object Solution {
    var index = 0
    var value = -1

    def kthSmallest(root: TreeNode, k: Int): Int = {
        index = 0
        value = -1
        if (root == null) -1
        else inorder(root, k)
        value
    }

    // Using In order
    def inorder(root: TreeNode, k: Int): Unit = {
        if (root != null && index < k) {
            inorder(root.left, k)
            index += 1
            if (index == k) value = root.value
            inorder(root.right, k)
        }
    }
}
```