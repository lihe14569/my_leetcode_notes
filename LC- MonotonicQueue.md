# Monotonic Queue

- [Monotonic Queue](#monotonic-queue)
  - [239. Sliding Window Maximum](#239-sliding-window-maximum)
  - [862. Shortest Subarray with Sum at Least K](#862-shortest-subarray-with-sum-at-least-k)


## [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

```
Input: (int[], int) Given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Output: (int[]) Return the max sliding window.(max value in sliding window ))
```

Solution: Brute Focre

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        //brute force
        int n = nums.length;
        if(n * k == 0) return new int[0];
        int[] res = new int[n - k + 1];
        for(int i = 0; i < n - k + 1; i++) {
            int max = Integer.MIN_VALUE;
            for(int j = i; j < i + k; j++) {
                max = Math.max(max, nums[j]);
            } 
            res[i] = max;
        }
        return res;
    }
}
```

Time complexity: O(N * K) (TLE)
Space complexity: O(1)

Solution2: Deque(Monotonic Queue)

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        //deque method
        int n = nums.length;
        Deque<Integer> q = new ArrayDeque<>();
        int[] res = new int[n - k + 1];
        for(int i = 0; i < n; i++) {
            int qStart = i - k + 1;
            //left start out if the range of sliding window is greater than k(size of sliding window is k - 1)
            while(!q.isEmpty() &&  i - q.peekFirst() >= k) q.pollFirst();
            //right end out if the current element is greater than the right end lement in queue
            while(!q.isEmpty() && nums[i] >= nums[q.peekLast()]) q.pollLast();
            q.offerLast(i);
            if(qStart >= 0) res[qStart] = nums[q.peekFirst()];
        }
        return res;
    }
}
```
Time complexity: O(N)
Space complexity: O(N)

## [862. Shortest Subarray with Sum at Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/)

```
Input: (int[], int) Given an array nums and a number k

Output: (int) Return the length of the shortest, non-empty, contiguous subarray of nums with sum at least k.

If there is no non-empty subarray with sum at least k, return -1.
```

Solution:






