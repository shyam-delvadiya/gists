# Problem Name: Longest Substring Without Repeating Characters
Link: https://leetcode.com/problems/longest-substring-without-repeating-characters

## Question

Given a string `s`, find the length of the longest
<span title="A contiguous non-empty sequence of characters within a string.">
substring
</span> without duplicate characters.
 

### Example 1:

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3. Note that "bca" and "cab" are also correct answers.
```

### Example 2:

```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

### Example 3:

```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

### Constraints:

- `0 <= s.length <= 5 * 104`
- `s` consists of English lettersGiven a string s, find the length of the longest substring without duplicate characters.

## Answer
Question is very simple. This problem is solved efficiently using the sliding window technique.

We maintain a window of characters that always contains unique characters only.
A HashMap is used to store the most recent index of each character.

Use two pointers:

- `left` → start of the window
- `right` → end of the window
- Traverse the string with right
- If a character repeats within the current window, move left to one position after the previous occurrence
- Update the maximum window size at each step

```Java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0, maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);

            // If character is already in map and inside current window
            if (map.containsKey(c) && map.get(c) >= left) {
                left = map.get(c) + 1; // move left pointer after duplicate
            }

            map.put(c, right); // update latest index of char
            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }
}
```
If you think there is any other better solution please share.