# LC - Two Pointer
<!-- GFM-TOC -->
- [LC - Two Pointer](#lc---two-pointer)
    - [167\. Two Sum II - Input array is sorted(Easy)](#167-two-sum-ii---input-array-is-sortedeasy)
    - [633. Sum of Square Numbers (Easy)](#633-sum-of-square-numbers-easy)
  - [345. Reverse Vowels of a String (Easy)](#345-reverse-vowels-of-a-string-easy)
  - [680. Valid Palindrome II (Easy)](#680-valid-palindrome-ii-easy)
  - [88. Merge Sorted Array](#88-merge-sorted-array)
  - [141. Linked List Cycle](#141-linked-list-cycle)
  - [524. Longest Word in Dictionary through Deleting](#524-longest-word-in-dictionary-through-deleting)
- [High frequency problems](#high-frequency-problems)
  - [42. Trapping Rain Water](#42-trapping-rain-water)
  - [15. 3Sum](#15-3sum)
  - [1695. Maximum Erasure Value](#1695-maximum-erasure-value)
- [Sliding window + Substring problems](#sliding-window--substring-problems)
  - [3. Longest Substring Without Repeating Characters](#3-longest-substring-without-repeating-characters)
  - [159. Longest Substring with At Most Two Distinct Characters](#159-longest-substring-with-at-most-two-distinct-characters)
  - [340. Longest Substring with At Most K Distinct Characters](#340-longest-substring-with-at-most-k-distinct-characters)
  - [76. Minimum Window Substring](#76-minimum-window-substring)
  - [395. Longest Substring with At Least K Repeating Characters](#395-longest-substring-with-at-least-k-repeating-characters)
  - [209. Minimum Size Subarray Sum](#209-minimum-size-subarray-sum)
  - [424. Longest Repeating Character Replacement](#424-longest-repeating-character-replacement)
  - [992. Subarrays with K Different Integers](#992-subarrays-with-k-different-integers)
  - [1248. Count Number of Nice Subarrays](#1248-count-number-of-nice-subarrays)
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

## [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)

```
Input:(int[], int[]) Given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Condition: Be stored inside the array nums1, change the array in-place
. 
Output:Merge nums1 and nums2 into a single array sorted in non-decreasing order.
```

Solution:

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        //merge sort
        int idx1 = m - 1, idx2 = n - 1;
        for(int i = m + n - 1; i >= 0; i--) {
            if(idx2 < 0) break;
            if(idx1 >= 0 && nums1[idx1] > nums2[idx2])
                nums1[i] = nums1[idx1--];
            else
                nums1[i] = nums2[idx2--];
        }
    }
}
```

Time complexity: **O(N)**
Space complexity: **O(1)**

When solve an array problem in-place, consider the possibility of iterating backwards instead of forwards through the array.

## [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

```
Input: (ListNode) Given head, the head of a linked list 
Output: (Boolean) Determine if the linked list has a cycle in it.
```

Solution:
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow) return true;
        }
        return false;
    }
}
```

Time compleixity: **O(N)** Space complexity: **O(1)**

## [524. Longest Word in Dictionary through Deleting](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/)

```
Input: (String, List<String>) Given a string s and a string array dictionary, 

Output: (String) Return the longest string in the dictionary that can be formed by deleting some of the given string characters. If there is more than one possible result, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.
```

Note: 
1. Use two pointer method to check if a string in the list is the substring of target string.
2. If it is, check if it is longer than maxLength or same length with the smallest lexicographical order. Update the maxLength string
3. findSubstring helper function is very useful and worth to remember for finding substring by deleting characters.(*)


Solution:
```java
class Solution {
    public String findLongestWord(String s, List<String> dictionary) {
        String maxLen = "";
        for(String str : dictionary) {
            if(findSubstring(s, str)) {
                if(str.length() > maxLen.length() || str.length() == maxLen.length() && str.compareTo(maxLen) < 0)
                    maxLen = str;
            }
        }
        return maxLen;
    }
    private boolean findSubstring(String s, String str) {
        int j = 0;
        for(int i = 0; i < s.length() && j < str.length(); i++) {
            if(s.charAt(i) == str.charAt(j))
                j++;
        }
        return j == str.length();
    }
}
```
Time complexity: **O(N * K)** where N is the number of strings in the list, and K is the length of target string.
Space complexity: **O(1)**

# High frequency problems
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
Time Complexity: **O(N)**
Space Complexity:**O(1)**

## [15. 3Sum](https://leetcode.com/problems/3sum/)

```
Input: (int[]) Given an integer array nums.

Output: (List<List<Integer>>) Return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.
```
Note:  
   1. To use two pointer method, the array need to be sorted first, then iterate through the array, if the curren number is greater than zero, break, since in ascending order, the first number in triplets should always be negative so that the sum of three could be zero.
   2. If current value is negative and previous value is not same(non-duplicate), then we can use two pointer method applied on two sum problem to find targeted pairs.
   3. In the two sum helper function, if we found the low and high value, we added to results list, make sure that increment low and decrease high pointers by 1. Check if current low pointer has duplicate(same value as previous low), then increase to a unique low value.
   4. One thing, if the 3Sum problem change sume equals to k, then when we iterate thought the array, termination is current value greater than k.
   5. Other approaches such as **hashset** and **no-sort** are also shown in the following setction.
   
Solution(Two pointers): 
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        //ensure the array is sorted first
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        for(int i = 0; i < nums.length && nums[i] <= 0; i++) {
            if(i == 0 || nums[i - 1] != nums[i]) {
                twoSum(nums, i, res);
            }
        }
        return res;
    }
    public void twoSum(int[] nums, int i, List<List<Integer>> res) {
        int lo = i + 1, hi = nums.length - 1;
        while(lo < hi) {
            int sum = nums[i] + nums[lo] + nums[hi];
            if(sum < 0)
                lo++;
            else if(sum > 0)
                hi--;
            else {
                res.add(Arrays.asList(nums[i], nums[lo++], nums[hi--]));
                //avoid duplicate answer
                while(lo < hi && nums[lo] == nums[lo - 1])
                    lo++;
            }
        }
    }
}
```
Time complexity: **O(N^2)** inner loop(two sum helper function) is O(N), and we iterate over the array, which take N times, So it is O(N^2).
We also sort the array at first, so it takes O(N* log(N)), so time complexity is O(N^2 + N* log(N)) = **O(N^2)**
Space complexity: **O(1)** **>> NOT SURE <<**

Solution2(Hashset):

main method is same as two pointers, the only difference is two sum helper function.

```java
public void twoSum(int[] nums, int i, List<List<Integer>> res) {
        //HashSet method
        Set<Integer> set = new HashSet<>();
        for(int j = i + 1; j < nums.length; j++) {
            int complement = -nums[i] - nums[j];
            if(set.contains(complement)) {
                res.add(Arrays.asList(nums[i], nums[j], complement));
                //the following termination condition ensure nums[j] is still same value, we just move to the right most duplicate.
                while(j  + 1 < nums.length && nums[j] == nums[j + 1])
                    j++;
            }
            //nums[j] has same value as the left-most duplicate.
            set.add(nums[j]);
        }
    }
```

Time complexity: **O(N^2)**
Space complexity: 

Solution3(No-sort):

If the interviewer ask not to modify the origina array(sorting is not allowed).

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





# Sliding window + Substring problems

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
Notes:
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

## [395. Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)


```
Input: (String ,int) Given a string s and an integer k.
Output (int) Return the length of the longest substring of s such that the frequency of each character in this substring is greater than or equal to k.
```

Soluiton:

```java
class Solution {
    public int longestSubstring(String s, int k) {
        //sliding window 
        int res = 0;
        for(int unique = 1; unique <= 26; unique++) {
            Map<Character, Integer> map = new HashMap<>();
            int left = 0, validCount = 0;
            for(int i = 0; i < s.length(); i++) {
                char c1 = s.charAt(i);
                map.put(c1, map.getOrDefault(c1, 0) + 1);
                if(map.get(c1) == k) validCount++;
                while(map.keySet().size() > unique) {
                    char c2 = s.charAt(left);
                    if(map.getOrDefault(c2, 0) == k) validCount--;
                    map.put(c2, map.getOrDefault(c2, 0) - 1);
                    if(map.get(c2) == 0) map.remove(c2);
                    left++;
                }
                int count = map.keySet().size();
                if(count == unique && count == validCount) res = Math.max(res, i - left + 1);
            }
        }
        return res;
    }
}
```

Time complexity: **O(26 * N) = O(N)**
Space complexity: **O(N)**

## [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)


```
Input:(int, int[]) Given an array of positive integers nums and a positive integer target.

Output: (int) Return the minimal length of a contiguous subarray [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.
```

Solution:

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int left = 0, N = nums.length, res = Integer.MAX_VALUE, sum = 0;
        for(int i = 0; i < N; i++) {
            sum += nums[i];
            while(sum >= target) {
                res = Math.min(res, i - left + 1);
                sum -= nums[left++];
            }
        }
        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```

## [424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)



```
Input: (String, int) Given a string s and an integer k.

Condition: You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Output: (int) Return the length of the longest substring containing the same letter you can get after performing the above operations.
```

Solution:

```java
class Solution {
    public int characterReplacement(String s, int k) {
        int N = s.length();
        
        int[] arr = new int[26];
        int left = 0, res = 0;
        for(int i = 0; i < s.length(); i++) {
            arr[s.charAt(i) - 'A']++;
            while(i - left + 1 - findMax(arr) > k) {
                arr[s.charAt(left) - 'A']--;
                left++;
            }
            res = Math.max(res, i - left + 1);
        }
        return res;
    }
    private int findMax(int[] arr) {
        return Arrays.stream(arr).max().getAsInt();
    }
}
```

Time complexity: **O(N)**
Space complexity: **O(N)**

## [992. Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)

```
 Input:(String, int) Given an array nums of positive integers, call a (contiguous, not necessarily distinct) subarray of nums good if the number of different integers in that subarray is exactly k.

 (For example, [1,2,3,1,2] has 3 different integers: 1, 2, and 3.)

Output: (int) Return the number of good subarrays of nums.
```

Solution:

```java
class Solution {
    // exactly k = atMost(k) - atMost(k - 1)
    public int subarraysWithKDistinct(int[] nums, int k) {
        return atMost(nums, k) - atMost(nums, k - 1);
    }
    private int atMost(int[] nums, int k) {
        int res = 0;
        int n = nums.length;
        int left = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < n; i++){
            if(map.getOrDefault(nums[i], 0) == 0) k--;
            map.put(nums[i], map.getOrDefault(nums[i], 0) + 1);
            while(k < 0) {
                map.put(nums[left], map.get(nums[left]) - 1);
                if(map.get(nums[left]) == 0) k++;
                left++;
            }
            res += i - left + 1;
        }
        return res;
    }
}
```

## [1248. Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/)


```
Input:(int[], int) Given an array of integers nums and an integer k. A continuous subarray is called nice if there are k odd numbers on it.

Output:(int) Return the number of nice sub-arrays.
```

```java
Solution:

class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        return atMost(nums, k) - atMost(nums, k - 1);
    }
    private int atMost(int[] nums, int k) {
        int res = 0;
        int left = 0;
        for(int i = 0; i < nums.length; i++) {
            k -= nums[i] % 2;
            while(k < 0) {
                k += nums[left++] % 2;
            }
            res += i - left + 1;
        }
        return res;
    }
}
```
