# LC - Two Pointer
<!-- GFM-TOC -->
- [LC - Two Pointer](#lc---two-pointer)
    - [167\. Two Sum II - Input array is sorted(Easy)](#167-two-sum-ii---input-array-is-sortedeasy)
<!-- GFM-TOC -->

Two pointer method is an effective algorithm to find target/pair in array/list data strucure.


### [167\. Two Sum II - Input array is sorted(Easy)](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

```java
Input sorted array, Output is  a pair of numbers that equals to given target value.
```

Soluiton: 

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int l = 0, r = numbers.length - 1;
        while(l < r) {
            if(numbers[l] + numbers[r] == target)
                return new int[]{ l + 1, r + 1};
            else if(numbers[l] + numbers[r] < target)
                l++;
            else
                r--;
        }
        return new int[]{-1, -1};
    }
}
```

###. 633. Sum of Square Numbers (Easy)