# LC - Two Pointer
<!-- GFM-TOC -->
- [LC - Two Pointer](#lc---two-pointer)
    - [167\. Two Sum II - Input array is sorted(Easy)](#167-two-sum-ii---input-array-is-sortedeasy)
    - [633. Sum of Square Numbers (Easy)](#633-sum-of-square-numbers-easy)
  - [345. Reverse Vowels of a String (Easy)](#345-reverse-vowels-of-a-string-easy)
  - [680. Valid Palindrome II (Easy)](#680-valid-palindrome-ii-easy)
  - [1695. Maximum Erasure Value](#1695-maximum-erasure-value)
  - [42. Trapping Rain Water](#42-trapping-rain-water)
  - [3. Longest Substring Without Repeating Characters](#3-longest-substring-without-repeating-characters)
  - [159. Longest Substring with At Most Two Distinct Characters](#159-longest-substring-with-at-most-two-distinct-characters)
  - [340. Longest Substring with At Most K Distinct Characters](#340-longest-substring-with-at-most-k-distinct-characters)
  - [76. Minimum Window Substring](#76-minimum-window-substring)
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

## [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)

```
Input: (int[]) n non-negative integers representing an elevation map where the width of each bar is 1.
Output: (int)Compute how much water it can trap after raining.
```

Solution:

```java
class Solution {
    public int trap(int[] height) {
        //TWO POINTERS
        int leftIdx = 0, rightIdx = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int volume = 0;
        while(leftIdx <= rightIdx) {
            leftMax = Math.max(leftMax, height[leftIdx]);
            rightMax = Math.max(rightMax, height[rightIdx]);
            if(leftMax <= rightMax) {
                volume += leftMax - height[leftIdx++];
            }
            else {
                volume += rightMax - height[rightIdx--];
            }
        }
        return volume;
    }
}
```
Time Complexity: O(N)
Space Complexity: O(1)

## [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```
Input:(String) Given a string s.
Output: (int) the length of the longest substring without repeating characters.
```
Note: One of the most popular LC problem.  
Solution: (Sliding window)  

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        //sliding window with hashset
        Set<Character> set = new HashSet<>();
        int left = 0;
        int res = 0;
        //three steps: 1.put in bucket 2. take out from bucket 3.update valid length
        for(int i = 0; i < s.length(); i++) {
            char c  = s.charAt(i);    
            while(!set.add(c)) // step1: put character in bucket
                set.remove(s.charAt(left++));  //step2: take out left side character
            res = Math.max(res, i - left + 1); //step3: calculate valid result
        }
        return res;
    }
}
```
Time complexity: **O(N)**
Space complexity: **O(N)**

## [159. Longest Substring with At Most Two Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)

```
Input:(String) Given a string s.
Output: (int)  Return the length of the longest substring that contains at most two distinct characters.
```

Note: The solution is analogous to LC#3, the difference is that this question require at most two distinct characters, so we need to maitain the size of the map <= 2.

Soltution: 

 ```java
 class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0;
        int res = 0;
        for(int i = 0; i < s.length(); i++) {
            char c1 = s.charAt(i);
            map.put(c1, map.getOrDefault(c1, 0) + 1); // put right pointer in
            while(map.size() > 2) {
                char c2 = s.charAt(left);
                map.put(c2, map.get(c2) - 1);         //take left pointer out
                if(map.get(c2) == 0)                  //and move left pointer
                    map.remove(c2);
                //update the left pointer
                left++;
            }
            res = Math.max(res, i - left + 1);
        }
        return res;
    }
}
 ```

 Time complexity: **O(N)**
 Space complexity: **O(N)**

 ## [340. Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/)

```
Input:(String, int ) Given a string s and integer k.
Output: (int) Return the length of the longest substring of s that contains at most k distinct characters.
```

Solution:

```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        Map<Character, Integer> map = new HashMap<>();
        int left = 0;
        int res = 0;
        for(int i = 0; i < s.length(); i++){
            char c1 = s.charAt(i);
            map.put(c1, map.getOrDefault(c1, 0) + 1);
            while(map.size() > k) {
                char c2 = s.charAt(left);
                map.put(c2, map.get(c2) - 1);
                if(map.get(c2) == 0)
                    map.remove(c2);
                left++;
            }
            res = Math.max(res, i - left + 1);
        }
        return res;
    }
}
```
 Time complexity: **O(N)**
 Space complexity: **O(N)**

## [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)


```
Input:(String, String)Given two strings s and t of lengths m and n respectively.

A substring is a contiguous sequence of characters within the string.

Output: (String) Return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".
```

Solution:

```java
class Solution {
    public String minWindow(String s, String t) {
        Map<Character, Integer> map = new HashMap<>();
        for(char c : t.toCharArray()) map.put(c, map.getOrDefault(c, 0) + 1);
        int left = 0, minLen = Integer.MAX_VALUE, minLeft = 0, count = 0;
        for(int i = 0; i < s.length(); i++){
            char c1 = s.charAt(i);
            if(map.containsKey(c1)) {
                if(map.get(c1) > 0) count++;
                map.put(c1, map.get(c1) - 1);
            }
            while(count == t.length()) {
                if(i - left + 1 < minLen) {
                    minLen = i - left + 1;
                    minLeft = left;
                }
                char c2 = s.charAt(left);
                if(map.containsKey(c2)) {
                    map.put(c2, map.get(c2) + 1);
                    if(map.get(c2) > 0) count--;
                }
                left++;
            }
        }
        if(minLen == Integer.MAX_VALUE) return "";
        return s.substring(minLeft, minLeft + minLen);
    }
}
```
Time complexity: **O(N)**
Space complexity: **O(N)**

