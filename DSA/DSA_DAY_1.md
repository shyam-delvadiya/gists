# Problem Name: Two Sum 
Link: https://leetcode.com/problems/two-sum

## Question
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

### Example 1:
- Input: nums = [2,7,11,15], target = 9
- Output: [0,1]
- Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

### Example 2:
- Input: nums = [3,2,4], target = 6
- Output: [1,2]


### Example 3:
- Input: nums = [3,3], target = 6
- Output: [0,1]
 

### Constraints:

- 2 <= nums.length <= 104
- -109 <= nums[i] <= 109
- -109 <= target <= 109
- Only one valid answer exists.
 

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

## Answer

After reading the question first solution comes in my mind is simple two nested for loop (brute-force: We will iterate all elements one by one) that solution I am giving below.

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {

                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[]{}; // At least one solution exists, so this line is never reached
    }
}
```

but in this solution time complexity will be O(n2). we want better then this because if number is too big then this solution is not effective.

So lets go through again to the question when i read question again I noted that at least one solution is going to exist always and that is unique like num[i] + num[j] = target only happens for only one unique pair then we just have to find that unique pair and for that we can use Hashmap because HashMap stores unique keys, so we can quickly check whether the required complement already exists.
so, finally i come up with down given solution. 

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }
            map.put(nums[i], i);
        }
        return new int[]{}; // should never happen (guaranteed one solution)
    }
}
```

If you think there is any other better solution please share.