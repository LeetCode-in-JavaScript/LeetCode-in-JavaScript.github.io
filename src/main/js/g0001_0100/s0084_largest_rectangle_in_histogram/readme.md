[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 84\. Largest Rectangle in Histogram

Hard

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return _the area of the largest rectangle in the histogram_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

**Input:** heights = [2,1,5,6,2,3]

**Output:** 10

**Explanation:** The above is a histogram where width of each bar is 1. 

The largest rectangle is shown in the red area, which has an area = 10 units.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

**Input:** heights = [2,4]

**Output:** 4

**Constraints:**

*   <code>1 <= heights.length <= 10<sup>5</sup></code>
*   <code>0 <= heights[i] <= 10<sup>4</sup></code>

## Solution

```javascript
/**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function(heights) {
    let stack = []
    let maxArea = 0
    let index = 0

    while (index < heights.length) {
        if (stack.length === 0 || heights[stack[stack.length - 1]] <= heights[index]) {
            stack.push(index++)
        } else {
            let top = stack.pop()
            let area = heights[top] * (stack.length === 0 ? index : index - stack[stack.length - 1] - 1)
            maxArea = Math.max(maxArea, area)
        }
    }

    while (stack.length > 0) {
        let top = stack.pop()
        let area = heights[top] * (stack.length === 0 ? index : index - stack[stack.length - 1] - 1)
        maxArea = Math.max(maxArea, area)
    }

    return maxArea
};

export { largestRectangleArea }
```