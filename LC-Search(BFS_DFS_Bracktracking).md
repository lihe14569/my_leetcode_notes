# LC - Search(BFS, DFS and Backtracking)

- [LC - Search(BFS, DFS and Backtracking)](#lc---searchbfs-dfs-and-backtracking)
- [DFS](#dfs)
  - [270. Closest Binary Search Tree Value](#270-closest-binary-search-tree-value)
  - [51. N-Queens(Hard)](#51-n-queenshard)


# DFS

## [270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/)

```
Input: (TreeNode, double)Given the root of a binary search tree and a target value.
Output:(int) Return the value in the BST that is closest to the target.
```

Solution:
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    int res = 0;
    double min = Double.MAX_VALUE;
    public int closestValue(TreeNode root, double target) {
        //dfs
        dfs(root, target);
        return res;
    }
    public void dfs(TreeNode root, double target) {
        //base case
        if(root == null) return;
        if(Math.abs(root.val - target) < min) {
            min = Math.abs(root.val - target);
            res = root.val;
        }
        if(root.val > target) 
            dfs(root.left, target);
        else
            dfs(root.right, target);
    }
}
```
Time complexity: **O(h)**, where h is the height of BST
Space complexity: O(1)




## [51. N-Queens(Hard)](https://leetcode.com/problems/n-queens/)

```java
Input:(int) n, the size of 2d-matrix is  n x n.

Condition:  Placing n queens on an n x n chessboard such that no two queens attack each other.

Output: (List<List<String>>) return all distinct solutions to the n-queens puzzle.
```

**Solution:**

```java
class Solution {
    private char[][] board;
    private boolean[] cols;
    private boolean[] diagonal;
    private boolean[] antidiagonal;
    
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();
        board =new char[n][n];
        for(char[] row : board) {
            Arrays.fill(row, '.');
        }
        cols = new boolean[n];
        diagonal = new boolean[2 * n - 1] ;
        antidiagonal = new boolean[2 * n - 1];
        backtracking(board, 0, n, res);
        return res;
    }
    public void backtracking(char[][] board, int row, int n, List<List<String>> res) {
        if(row == n) {
            List<String> list = new ArrayList<>();
            for(char[] str : board) {
                list.add(new String(str));
            }
            res.add(list);
            return;
        }
        
        for(int col = 0; col  < n; col++) {
            int diagonalIdx = row + col;
            int antidiagonalIdx = n - 1 - (row - col);
            if(cols[col] || diagonal[diagonalIdx] || antidiagonal[antidiagonalIdx]) continue;
            board[row][col] = 'Q';
            cols[col] = diagonal[diagonalIdx] = antidiagonal[antidiagonalIdx] = true;
            backtracking(board, row + 1, n, res);
            board[row][col] = '.';
            cols[col] = diagonal[diagonalIdx] = antidiagonal[antidiagonalIdx] = false;
        }
    }
}
```
Time complexity: *O(N!)* 
For the first row, we have N options. For the second row, since we can not place the column and diagonal that previous occupied, we have only N-2 options .....Therefore, we have approximate N! time.

Based on the LC official solution 
>While it costs O(N^2)O(N 
2
 ) to build each valid solution, the amount of valid solutions S(N)S(N) does not grow nearly as fast as N!N!, so O(N! + S(N) * N^2) = O(N!)O(N!+S(N)∗N^2)=O(N!)

Space complexity : *O(N^2)*

Similar Problem: 52.


