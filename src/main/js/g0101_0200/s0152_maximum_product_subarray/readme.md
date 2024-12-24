[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 152\. Maximum Product Subarray

Medium

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.

**Example 1:**

**Input:** nums = [2,3,-2,4]

**Output:** 6

**Explanation:** [2,3] has the largest product 6.

**Example 2:**

**Input:** nums = [-2,0,-1]

**Output:** 0

**Explanation:** The result cannot be 2, because [-2,-1] is not a subarray.

**Constraints:**

*   <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
*   `-10 <= nums[i] <= 10`
*   The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function(nums) {
    let overAllMaxProd = Number.MIN_SAFE_INTEGER
    let n = nums.length
    let start = 1
    let end = 1

    for (let i = 0; i < n; i++) {
        // Reset `start` and `end` to 1 if they become 0
        if (start === 0) {
            start = 1
        }
        if (end === 0) {
            end = 1
        }

        start *= nums[i]
        end *= nums[n - i - 1]

        overAllMaxProd = Math.max(overAllMaxProd, Math.max(start, end))
    }

    return overAllMaxProd
};

export { maxProduct }
```