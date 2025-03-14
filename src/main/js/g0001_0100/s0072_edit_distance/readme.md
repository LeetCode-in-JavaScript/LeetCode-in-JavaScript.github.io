[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 72\. Edit Distance

Hard

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

*   Insert a character
*   Delete a character
*   Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"

**Output:** 3

**Explanation:** 

horse -> rorse (replace 'h' with 'r') 

rorse -> rose (remove 'r') 

rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"

**Output:** 5

**Explanation:** 

intention -> inention (remove 't') 

inention -> enention (replace 'i' with 'e') 

enention -> exention (replace 'n' with 'x') 

exention -> exection (replace 'n' with 'c') 

exection -> execution (insert 'u')

**Constraints:**

*   `0 <= word1.length, word2.length <= 500`
*   `word1` and `word2` consist of lowercase English letters.

## Solution

```javascript
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function(w1, w2) {
    const n1 = w1.length
    const n2 = w2.length

    if (n2 > n1) {
        return minDistance(w2, w1)
    }

    const dp = new Array(n2 + 1).fill(0)
    for (let j = 0; j <= n2; j++) {
        dp[j] = j
    }

    for (let i = 1; i <= n1; i++) {
        let pre = dp[0]
        dp[0] = i
        for (let j = 1; j <= n2; j++) {
            const tmp = dp[j]
            dp[j] =
                w1[i - 1] !== w2[j - 1]
                    ? 1 + Math.min(pre, Math.min(dp[j], dp[j - 1]))
                    : pre
            pre = tmp
        }
    }

    return dp[n2]
};

export { minDistance }
```