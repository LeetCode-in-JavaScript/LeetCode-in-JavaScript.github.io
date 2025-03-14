[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 4\. Median of Two Sorted Arrays

Hard

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

**Example 1:**

**Input:** nums1 = [1,3], nums2 = [2]

**Output:** 2.00000

**Explanation:** merged array = [1,2,3] and median is 2. 

**Example 2:**

**Input:** nums1 = [1,2], nums2 = [3,4]

**Output:** 2.50000

**Explanation:** merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5. 

**Example 3:**

**Input:** nums1 = [0,0], nums2 = [0,0]

**Output:** 0.00000 

**Example 4:**

**Input:** nums1 = [], nums2 = [1]

**Output:** 1.00000 

**Example 5:**

**Input:** nums1 = [2], nums2 = []

**Output:** 2.00000 

**Constraints:**

*   `nums1.length == m`
*   `nums2.length == n`
*   `0 <= m <= 1000`
*   `0 <= n <= 1000`
*   `1 <= m + n <= 2000`
*   <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code>

## Solution

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function (nums1, nums2) {
    if (nums2.length < nums1.length) {
        return findMedianSortedArrays(nums2, nums1)
    }

    let n1 = nums1.length,
        n2 = nums2.length
    let low = 0,
        high = n1

    while (low <= high) {
        let cut1 = Math.floor((low + high) / 2)
        let cut2 = Math.floor((n1 + n2 + 1) / 2) - cut1

        let l1 = cut1 === 0 ? -Infinity : nums1[cut1 - 1]
        let l2 = cut2 === 0 ? -Infinity : nums2[cut2 - 1]
        let r1 = cut1 === n1 ? Infinity : nums1[cut1]
        let r2 = cut2 === n2 ? Infinity : nums2[cut2]

        if (l1 <= r2 && l2 <= r1) {
            if ((n1 + n2) % 2 === 0) {
                return (Math.max(l1, l2) + Math.min(r1, r2)) / 2.0
            }
            return Math.max(l1, l2)
        } else if (l1 > r2) {
            high = cut1 - 1
        } else {
            low = cut1 + 1
        }
    }

    return 0.0
}

export { findMedianSortedArrays }
```