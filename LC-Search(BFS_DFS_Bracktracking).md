# LC - Search(BFS, DFS and Backtracking)

- [LC - Search(BFS, DFS and Backtracking)](#lc---searchbfs-dfs-and-backtracking)
- [51. N-Queens(Hard)](#51-n-queenshard)



# [51. N-Queens(Hard)](https://leetcode.com/problems/n-queens/)

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

