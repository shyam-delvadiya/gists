# Problem Name: Median of Two Sorted Arrays
Link: https://leetcode.com/problems/median-of-two-sorted-arrays

## Question

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

### Example 1:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

### Example 2:
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

### Constraints:
- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-106 <= nums1[i], nums2[i] <= 106`

## Answer
- Very Simple we have to find median.
- If we have odd numbers in list then median is - length/2 index element sort term center element.
- If we have even numbers in listn then median is average of two center numbers.
- So simple merge two array in sorted order.

```Java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int l1 = nums1.length;
        int l2 = nums2.length;
        int[] result = new int[l1+l2];
        int i = 0,j = 0,k = 0;
        double output = 0;
        while(i < l1 && j < l2){
            if(nums1[i] <=nums2[j]){
                result[k++] = nums1[i++];
            }
            else{
                result[k++] = nums2[j++];
            }
        }

        while(i < l1){
            result[k++] = nums1[i++];
        }

        while(j < l2){
            result[k++] = nums2[j++];
        }
        
        
        if(((l1+l2) %2) == 1){
            int median = (l1+l2)/2;
            output = result[median];
            return output;
        }
        else{
            int median = (l1+l2)/2;
            output = result[median - 1] + result[median];
            return output / 2;
        }
    }
}
```

After I solved this problem then i noticed question asked specific time complexity should be `O(log(m+n))`.

This solution merges two sorted arrays and finds the median from the merged result.
While it is easy to understand and correct, it runs in `O(m+n)` time and does not meet the problem’s required `O(log(m+n))` complexity.

```Java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {

        // Always binary search on the smaller array
        if (nums1.length > nums2.length) {
            return findMedianSortedArrays(nums2, nums1);
        }

        int m = nums1.length;
        int n = nums2.length;

        int low = 0;
        int high = m;

        while (low <= high) {
            int cutA = (low + high) / 2;
            int cutB = (m + n + 1) / 2 - cutA;

            // Handle edges using min/max values
            int leftA  = (cutA == 0) ? Integer.MIN_VALUE : nums1[cutA - 1];
            int rightA = (cutA == m) ? Integer.MAX_VALUE : nums1[cutA];

            int leftB  = (cutB == 0) ? Integer.MIN_VALUE : nums2[cutB - 1];
            int rightB = (cutB == n) ? Integer.MAX_VALUE : nums2[cutB];

            // Check if we found the correct partition
            if (leftA <= rightB && leftB <= rightA) {

                // Odd total length
                if ((m + n) % 2 == 1) {
                    return Math.max(leftA, leftB);
                }

                // Even total length
                return (Math.max(leftA, leftB) + Math.min(rightA, rightB)) / 2.0;
            }
            // Too many elements from A on the left
            else if (leftA > rightB) {
                high = cutA - 1;
            }
            // Too few elements from A on the left
            else {
                low = cutA + 1;
            }
        }
    }
}

```

If you think there is any other better solution please share.