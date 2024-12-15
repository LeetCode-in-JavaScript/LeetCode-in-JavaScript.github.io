[![](https://img.shields.io/github/stars/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Stars&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript)
[![](https://img.shields.io/github/forks/LeetCode-in-JavaScript/LeetCode-in-JavaScript?label=Fork%20me%20on%20GitHub%20&style=flat-square)](https://github.com/LeetCode-in-JavaScript/LeetCode-in-JavaScript/fork)

## 139\. Word Break

Medium

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

**Note** that the same word in the dictionary may be reused multiple times in the segmentation.

**Example 1:**

**Input:** s = "leetcode", wordDict = ["leet","code"]

**Output:** true

**Explanation:** Return true because "leetcode" can be segmented as "leet code".

**Example 2:**

**Input:** s = "applepenapple", wordDict = ["apple","pen"]

**Output:** true

**Explanation:** Return true because "applepenapple" can be segmented as "apple pen apple". 

Note that you are allowed to reuse a dictionary word.

**Example 3:**

**Input:** s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]

**Output:** false

**Constraints:**

*   `1 <= s.length <= 300`
*   `1 <= wordDict.length <= 1000`
*   `1 <= wordDict[i].length <= 20`
*   `s` and `wordDict[i]` consist of only lowercase English letters.
*   All the strings of `wordDict` are **unique**.

## Solution

```javascript
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function(s, wordDict) {
    const memo = new Array(s.length + 1).fill(null)

    const dp = (i) => {
        if (i === s.length) {
            return true
        }
        if (memo[i] !== null) {
            return memo[i]
        }
        for (const word of wordDict) {
            const len = word.length
            if (i + len > s.length || s.substring(i, i + len) !== word) {
                continue
            }
            if (dp(i + len)) {
                memo[i] = true
                return true
            }
        }
        memo[i] = false
        return false
    }

    return dp(0)
};

export { wordBreak }
```