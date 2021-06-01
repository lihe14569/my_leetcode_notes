# LC - Two Pointer
<!-- GFM-TOC -->
- [LC - Two Pointer](#lc---two-pointer)
    - [167\. Two Sum II - Input array is sorted(Easy)](#167-two-sum-ii---input-array-is-sortedeasy)
    - [633. Sum of Square Numbers (Easy)](#633-sum-of-square-numbers-easy)
  - [345. Reverse Vowels of a String (Easy)](#345-reverse-vowels-of-a-string-easy)
  - [680. Valid Palindrome II (Easy)](#680-valid-palindrome-ii-easy)
  - [1695. Maximum Erasure Value](#1695-maximum-erasure-value)
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

### [633. Sum of Square Numbers (Easy)](https://leetcode.com/problems/sum-of-square-numbers/)

```java
Input: (int)a non-negative integer c
Output: (boolean) decide whether there're two integers a and b such that a^2 + b^2 = c.
```

Solution:

```java
class Solution {
    public boolean judgeSquareSum(int c) {
        //two number can be same
        int l = 0, r = (int) Math.sqrt(c);
        while(l <= r) {
            int sum = l * l + r * r;
            if(sum == c)
                return true;
            else if(sum < c)
                l++;
            else
                r--;
        }
        return false;
    }
}
```
Time complexity: **_O(N)_**  
Space complexity: **_O(1)_**

## [345. Reverse Vowels of a String (Easy)](https://leetcode.com/problems/reverse-vowels-of-a-string/)

```java
Input: (String) a string
Output: (String) reverse only all the vowels in the string and return it.
```

Solution:

```java
class Solution {
    private Set<Character> vowels = new HashSet<>(Arrays.asList('a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'));
    public String reverseVowels(String s) {
        int l = 0, r = s.length() - 1;
        StringBuilder sb = new StringBuilder(s);
        while(l < r) {
            if(!vowels.contains(s.charAt(l)))
                l++;
            else if(!vowels.contains(s.charAt(r)))
                r--;
            else {
                swap(sb, l++, r--);
            }
        }
        return sb.toString();
    }
    public void swap(StringBuilder sb, int l, int r) {
        char c = sb.charAt(l);
        sb.setCharAt(l, sb.charAt(r));
        sb.setCharAt(r, c);
    }
}
```
Time complexity: **_O(N)_**  
Space complexity: **_O(N)_**

**Note**:

Write if-else statements as above as template is concise and logically easier.

## [680. Valid Palindrome II (Easy)](https://leetcode.com/problems/valid-palindrome-ii/)

```java
Input:(String) A string s
Output: (boolean)  Return true if the s can be palindrome after deleting at most one character from it.
```

Solution:

```java
class Solution {
    public boolean validPalindrome(String s) {
        int l = 0, r = s.length() - 1;
        
        while(l < r) {
            if(s.charAt(l) != s.charAt(r)) {
                return isPalindrome(s, l + 1, r) || isPalindrome(s, l, r - 1);
            }
            l++;
            r--;
        }
        return true;
    }
    
    public boolean isPalindrome(String s, int l, int r) {
        while(l < r) {
            if(s.charAt(l++) != s.charAt(r--))
                return false;
        }
        return true;
    }
}
```
Time complexity: **_O(N)_**
Space complexity: **_O(1)_**


## [1695. Maximum Erasure Value](https://leetcode.com/problems/maximum-erasure-value/)

```java
Input: (int[]) integer array nums
Output: (int) Return the maximum score you can get by erasing exactly one subarray.
```

Solution:

```java
class Solution {
    public int maximumUniqueSubarray(int[] nums) {
        int res = 0;
        int currSum = 0;
        Set<Integer> set = new HashSet<>();
        int start = 0;
        for(int end = 0; end < nums.length; end++) {
            while(set.contains(nums[end])) {
                set.remove(nums[start]);
                currSum -= nums[start];
                start++;
            }
            set.add(nums[end]);
            currSum += nums[end];
            res = Math.max(res, currSum);
        }
        return res;
    }
}
```
Time complexity: **_O(N)_**
Space complexity: **_O(N)_**

