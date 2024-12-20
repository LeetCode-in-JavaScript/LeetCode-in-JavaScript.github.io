[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 45\. Jump Game II

Medium

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example 1:**

**Input:** nums = [2,3,1,1,4]

**Output:** 2

**Explanation:** The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

**Input:** nums = [2,3,0,1,4]

**Output:** 2

**Constraints:**

*   <code>1 <= nums.length <= 10<sup>4</sup></code>
*   `0 <= nums[i] <= 1000`

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var getMax = function(nums, l, r) {
    let max = -1
    for (let i = l; i <= r; i++) {
        max = Math.max(max, i + nums[i])
    }
    return max
};

var jump = function(nums) {
    let l = 0
    let r = 0
    let jumps = 0

    while (r < nums.length - 1) {
        let prev = r
        r = getMax(nums, l, r)
        l = prev + 1
        jumps++
    }

    return jumps
};

export { jump }
```