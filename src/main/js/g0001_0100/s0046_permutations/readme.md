[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 46\. Permutations

Medium

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]

**Output:** [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]

**Output:** [[0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]

**Output:** [[1]]

**Constraints:**

*   `1 <= nums.length <= 6`
*   `-10 <= nums[i] <= 10`
*   All the integers of `nums` are **unique**.

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function(nums) {
    if (!nums || nums.length === 0) {
        return []
    }

    const finalResult = []
    const used = new Array(nums.length).fill(false)

    const permuteRecur = (nums, finalResult, currResult, used) => {
        if (currResult.length === nums.length) {
            finalResult.push([...currResult]) // Create a copy of currResult
            return
        }
        for (let i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue
            }
            currResult.push(nums[i])
            used[i] = true
            permuteRecur(nums, finalResult, currResult, used)
            used[i] = false
            currResult.pop() // Backtrack
        }
    }

    permuteRecur(nums, finalResult, [], used)
    return finalResult
};

export { permute }
```