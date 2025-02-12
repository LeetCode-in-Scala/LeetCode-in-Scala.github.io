[![](https://img.shields.io/github/stars/LeetCode-in-Scala/LeetCode-in-Scala?label=Stars&style=flat-square)](https://github.com/LeetCode-in-Scala/LeetCode-in-Scala)
[![](https://img.shields.io/github/forks/LeetCode-in-Scala/LeetCode-in-Scala?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-Scala/LeetCode-in-Scala/fork)

## 41\. First Missing Positive

Hard

Given an unsorted integer array `nums`, return the smallest missing positive integer.

You must implement an algorithm that runs in `O(n)` time and uses constant extra space.

**Example 1:**

**Input:** nums = [1,2,0]

**Output:** 3 

**Example 2:**

**Input:** nums = [3,4,-1,1]

**Output:** 2 

**Example 3:**

**Input:** nums = [7,8,9,11,12]

**Output:** 1 

**Constraints:**

*   <code>1 <= nums.length <= 5 * 10<sup>5</sup></code>
*   <code>-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

## Solution

```scala
import scala.annotation.tailrec

object Solution {
    def firstMissingPositive(nums: Array[Int]): Int = {
        for (i <- nums.indices) {
            if (nums(i) > 0 && nums(i) < nums.length && nums(i) != i + 1) {
                dfs(nums, nums(i))
            }
        }

        var result = nums.length + 1
        var found = false
        for (i <- nums.indices if !found) {
            if (nums(i) != i + 1) {
                result = i + 1
                found = true
            }
        }

        result
    }

    @tailrec
    private def dfs(nums: Array[Int], value: Int): Unit = {
        if (value <= 0 || value > nums.length || value == nums(value - 1)) {
            return
        }
        val temp = nums(value - 1)
        nums(value - 1) = value
        dfs(nums, temp)
    }
}
```