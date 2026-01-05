# Problem Name: Longest Palindromic Substring
Link: https://leetcode.com/problems/longest-palindromic-substring

## Question

Given a string `s`, return the longest 
<span title="A substring is a contiguous non-empty sequence of characters within a string.">
palindromic substring </span> in `s`.


### Example 1:
```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```
### Example 2:
```
Input: s = "cbbd"
Output: "bb"
```

### Constraints:

- `1 <= s.length <= 1000`
- `s consist of only digits and English letters.`

## Answer

- A palindrome always grows from the center.
- For every position in the string, I treat it as a possible center.
- I check two cases:
    
    odd length → center at the character

    even length → center between two characters

- From each center, I move left and right while the characters match.

- I keep track of the longest palindrome I find.

- Finally, I return that substring.

```Java

    public String longestPalindrome(String s) {
      int start = 0;      // starting index of longest palindrome
        int maxLen = 1;    // length of longest palindrome

        for (int i = 0; i < s.length(); i++) {

            // check odd length palindrome (center at i)
            int oddLen = stretch(s, i, i);

            // check even length palindrome (center between i and i+1)
            int evenLen = stretch(s, i, i + 1);

            int bestLen = Math.max(oddLen, evenLen);

            if (bestLen > maxLen) {
                maxLen = bestLen;
                start = i - (bestLen - 1) / 2;
            }
        }

        return s.substring(start, start + maxLen);
    }

    // this method stretches from the center and returns palindrome length
    private int stretch(String s, int left, int right) {

        while (left >= 0 && right < s.length()
                && s.charAt(left) == s.charAt(right)) {

            left--;
            right++;
        }

        // we went one step extra, so fix the length
        return right - left - 1;  
    }
```