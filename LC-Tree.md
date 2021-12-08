# LC - Tree
Almost all problems of the problems are summerized by [古城算法](https://www.youtube.com/c/%E5%8F%A4%E5%9F%8E%E7%AE%97%E6%B3%95)
根据城主的分类算法笔记
- [LC - Tree](#lc---tree)
- [1. Tree Traversal](#1-tree-traversal)
  - [144. Binary Tree Preorder Traversal](#144-binary-tree-preorder-traversal)
  - [94. Binary Tree Inorder Traversal](#94-binary-tree-inorder-traversal)
- [2. Serialize/Deserialize/Construct Tree](#2-serializedeserializeconstruct-tree)
- [3. Binary Search Tree(BST)](#3-binary-search-treebst)
  - [270. Closest Binary Search Tree Value](#270-closest-binary-search-tree-value)
  - [450. Delete Node in a BST](#450-delete-node-in-a-bst)
  - [98. Validate Binary Search Tree](#98-validate-binary-search-tree)
  - [173. Binary Search Tree Iterator](#173-binary-search-tree-iterator)
  - [426. Convert Binary Search Tree to Sorted Doubly Linked List](#426-convert-binary-search-tree-to-sorted-doubly-linked-list)
  - [99. Recover Binary Search Tree](#99-recover-binary-search-tree)
  - [108. Convert Sorted Array to Binary Search Tree](#108-convert-sorted-array-to-binary-search-tree)
  - [1382. Balance a Binary Search Tree](#1382-balance-a-binary-search-tree)
  - [96. Unique Binary Search Trees](#96-unique-binary-search-trees)
  - [95. Unique Binary Search Trees II](#95-unique-binary-search-trees-ii)
- [4. LCA of Binary Tree](#4-lca-of-binary-tree)
  - [[235. Lowest Common Ancestor of a Binary Search Tree]](#235-lowest-common-ancestor-of-a-binary-search-tree)
  - [[236. Lowest Common Ancestor of a Binary Tree]](#236-lowest-common-ancestor-of-a-binary-tree)


# 1. Tree Traversal
## [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

```
Input: Given the root of a binary tree
Output: return the preorder traversal of its nodes' values.
```
思路：preorder traversal,有用stack的iterative 的方法，也可以recursive.

Solution : iterative using stack
```java
public List<Integer> preorderTraversal(TreeNode root) {
        //preoder-iterative template 1
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> s = new Stack<>();
        TreeNode curr = root;
        while(curr != null || !s.isEmpty()) {
            if(curr != null) {
                res.add(curr.val);
                s.push(curr);
                curr = curr.left;
            } else {
                curr = s.pop();
                curr = curr.right;
            }
        }
        return res;
    }
```

## [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

```
Given the root of a binary tree, return the inorder traversal of its nodes' values.
```
solution: /
# 2. Serialize/Deserialize/Construct Tree
# 3. Binary Search Tree(BST)

```
Basic operations: search in BST
```

## [270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/)

```
Input: (TreeNode, double)Given the root of a binary search tree and a target value.
Output:(int) Return the value in the BST that is closest to the target.
```

Solution:


```java
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

```
Basic operation: insert (N/A)
```
```
Basic operation: Delete
```

## [450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)


Input: (TreeNode, int) Given a root node reference of a BST and a key, delete the node with the given key in the BST. 
Output: (TreeNode) Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:
Search for a node to remove.
If the node is found, delete the node.

Solution:

```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root ==  null) return null;
        if(root.val < key)
            root.right =  deleteNode(root.right, key);
        else if(root.val > key)
            root.left = deleteNode(root.left, key);
        else if(root.right == null)
            return root.left;
        else if(root.left == null)
            return root.right;
        else {
            root.val = findMin(root.right);
            root.right = deleteNode(root.right, root.val);
        }
        return root;
    }
    public int findMin(TreeNode node) {
        while(node.left != null) node = node.left;
        return node.val;
    }
}
```

Time complexity: **O(log N)**  
Space complexity: O(1)

## [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)


```
Input:(TreeNode) Given the root of a binary tree

Output: (boolean)Determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
```

Solution1(recursive inorder traversal)


```java
class Solution {
    //8 byte long for corner testcase: [2^-31]
    private long prev = Long.MIN_VALUE;
    public boolean isValidBST(TreeNode root) {
        //inorder trasversal + recursive method
        //base csae
        if(root == null) return true;
        boolean left = isValidBST(root.left);
        if(!left) return false;
        if(root.val <= prev) return false;
        prev = root.val;
        return isValidBST(root.right);
    }
}
```

Time complexity: O(N)  
Space complexit: **O(N) for the space on the run-time stack**

Solution2:(Iterative inorder traversal)

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        TreeNode prev = null;
        Stack<TreeNode> stack = new Stack<>();
        while(root != null || !stack.isEmpty()) {
            while(root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            if(prev != null && root.val <= prev.val) return false;
            prev = root;
            root = root.right;
        }
        return true;
    }
```

Time complexity: O(N)
Space complexity: O(N)

Solution3: Recursive traversal with valid range

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        //upperbound + lowerbound
        return isValidBST(root, null, null);
    }
    public boolean isValidBST(TreeNode root, Integer max, Integer min) {
        if(root == null) return true;
        if(max != null && root.val >= max) return false;
        if(min != null && root.val <= min) return false;
        return isValidBST(root.left, root.val, min) && isValidBST(root.right, max, root.val);
    }
}
```

Time complexity: O(N)  
Space complexity: O(N)


## [173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)

```
Implement the BSTIterator class that represents an iterator over the in-order traversal of a binary search tree (BST):

BSTIterator(TreeNode root) Initializes an object of the BSTIterator class. The root of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.
boolean hasNext() Returns true if there exists a number in the traversal to the right of the pointer, otherwise returns false.
int next() Moves the pointer to the right, then returns the number at the pointer.
Notice that by initializing the pointer to a non-existent smallest number, the first call to next() will return the smallest element in the BST.
```

Solution:
```java

class BSTIterator {
    private Stack<TreeNode> stack;
    public BSTIterator(TreeNode root) {
        stack = new Stack<>();
        pushAllLeft(root);
    }
    public void pushAllLeft(TreeNode node) {
        while(node != null) {
            stack.push(node);
            node = node.left;
        }
    }
    public int next() {
        TreeNode root = stack.pop();
        pushAllLeft(root.right);
        return root.val;
    }
    
    public boolean hasNext() {
        return !stack.isEmpty();
    }
}
```

Time compleixty: O(N)  
Space complexity: O(N)


## [426. Convert Binary Search Tree to Sorted Doubly Linked List](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/)

```
Input: (Node) Convert a Binary Search Tree to a sorted Circular Doubly-Linked List in place.
Output:(Node) 

Left and right pointers as synonymous to the predecessor(prev) and successor(next) pointers in a doubly-linked list. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

We want to do the transformation in place. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. You should return the pointer to the smallest element of the linked list.
```

Solution(Recursive inorder):

```java
class Solution {
    Node head = null, prev = null;
    public Node treeToDoublyList(Node root) {
        //recursive
        if(root == null) return root;
        inorder(root);
        //connect head and tail 
        head.left = prev;
        prev.right = head;
        return head;
    }
    public void inorder(Node root) {
        if(root == null) return;
        inorder(root.left);
        if(head == null) head = root;
        if(prev != null) prev.right = root;
        root.left = prev;
        prev = root;
        inorder(root.right);
    }
}
```

Time complexity: O(N)  
Space complexity: O(N)


Solution(Iterative inorder):

```java
class Solution {
    public Node treeToDoublyList(Node root) {
        //iteraive inorder traversal
        if(root == null) return root;
        Node head = null, prev = null;
        Stack<Node> stack = new Stack<>();
        while(root != null || !stack.isEmpty()) {
            while(root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            //visit current node
            if(head == null) head = root;
            if(prev != null) {
                //connect prev and current node
                prev.right = root;
                root.left = prev;
            }
            prev = root;
            root = root.right;
        }
        head.left = prev;
        prev.right = head;
        return head;
  
 }
}
```  

Time complexity: O(N)
Space complexity: O(N)

## [99. Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)

```
Input: (TreeNode) Given the root of a binary search tree (BST), where exactly two nodes of the tree were swapped by mistake. 

Output(void) Recover the tree without changing its structure.
```


Solution (Iterative inorder traversal)

```java
class Solution {
    public void recoverTree(TreeNode root) {
        //iterative inorder traversal
        if(root == null) return;
        TreeNode first = null, second = null;
        TreeNode prev = new TreeNode(Integer.MIN_VALUE);
        Stack<TreeNode> stack = new Stack<>();
        while(root != null || !stack.isEmpty()) {
            while(root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            //visit current node and check it is inversed
            if(root.val < prev.val) {
                if(first == null) 
                    first = prev;
                second = root;
            }
            prev = root;
            root = root.right;
        }
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }
}
```

Time complexity: O(N)
Space complexity: O(N)

Note:
when we visit current node and check if it is inversed, we can intiate prev variable in two ways.

1. Initiate TreeNode prev as Integer.MIN_VALUE

   ```java
   TreeNode prev = new TreeNode(Integer.MIN_VALUE)
   //then when we check if node value in ascending order
   if(root.val < prev.val) {
       store nodes in buffer
   }
   ```

2. Initiate TreeNode prev as null value
   
    ```java
   TreeNode prev = null;
   //then when we check if node value in ascending order
   if(prev != null && root.val < prev.val) {
       store nodes in buffer
   }
   ```

Solution2: Recursive inorder traversal


```java
class Solution {
    TreeNode prev = null;
    TreeNode first = null, second = null;
    public void recoverTree(TreeNode root) {
        //recursive inorder traversal
        inorder(root);
        //swap first and second
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }
    public void inorder(TreeNode root) {
        if(root == null) return;
        inorder(root.left);
        //visit current node
        if(prev != null && root.val < prev.val) {
            if(first == null)
                first = prev;
            second = root;
        }
        //update prev and move to right subtree
        prev = root;
        inorder(root.right);
    }
}
```

Time complexity: O(N)
Space complexity: O(N)


Follow up: A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?  
Answer: **Morris Trasversal**


## [108. Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

```
Input: (int[])Given an integer array nums where the elements are sorted in ascending order.

Output: (TreeNode) Convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.
```

Solution:

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(nums, 0, nums.length - 1);
    }
    public TreeNode helper(int[] nums, int start, int end) {
        if(start > end) return null;
        //left mid point
        int mid = start + (end - start) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = helper(nums, start, mid - 1);
        root.right = helper(nums, mid + 1, end);
        return root;
    }
}
```
Time complexity: O(N)
Space complexity: O(N)


## [1382. Balance a Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree/)


```
Input: (TreeNode) Given a binary search tree, 

Output: (TreeNode) Return a balanced binary search tree with the same node values.

A binary search tree is balanced if and only if the depth of the two subtrees of every node never differ by more than 1.

If there is more than one answer, return any of them.
```

Solution(BST -> sorted numbers -> BST):

```java
class Solution {
    List<Integer> list;
    public TreeNode balanceBST(TreeNode root) {
        //same as 108, two pass method
        list = new ArrayList<>();
        inorder(list, root);
        return buildBST(list, 0, list.size() - 1);
    }
    public TreeNode buildBST(List<Integer> list, int start, int end) {
        //base case
        if(start > end) return null;
        int mid = start + (end - start) / 2;
        TreeNode root = new TreeNode(list.get(mid));
        root.left = buildBST(list, start, mid - 1);
        root.right = buildBST(list, mid + 1, end);
        return root;
    }
    public void inorder(List<Integer> list, TreeNode root) {
        //base case
        if(root == null) return;
        inorder(list, root.left);
        list.add(root.val);
        inorder(list, root.right);
    }
}
```

Time complexity: O(N)
Space complexity: O(N)


## [96. Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/)

```
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.
```

Solution1: Recursive

```java
class Solution {
    public int numTrees(int n) {
        //recursive method + memo
        Integer[] memo = new Integer[n + 1];
        return dfs(n, memo);
    }
    public int dfs(int num, Integer[] memo) {
        //base case
        if(num == 0 || num == 1) return 1;
        if(memo[num] != null) return memo[num];
        int sum = 0;
        for(int i = 1; i <= num; i++) {
            sum += dfs(i - 1, memo) * dfs(num - i, memo);
        }
        return memo[num] = sum;
    }
}
```

Time complexity: **O(N^2)**  
The recurrence Tree for n = 4:
```java
                                g(4)
                        /      |       |       \
                g(0)*g(3)  g(1)*g(2) g(2)*g(1) g(3)*g(1)  // 4
            /      |     \
    g(0)*g(2) g(1)*g(1) g(2)*g(2)                         //3
    /       \
g(0)*g(1)  g(1)*g(0)                                      //2
```
For the left most node, we use integer array to memorize calculated number of BST from 1 to N, which takes O(N).  
For each level, we need to do the production,which takes 2 + 3 + ... + N = O(N^2), so the total time complexity is O(N^2 + N) = O(N^2)  

Space complexity: **O(N)** for the call stack


Solution2: Dynamic programming

```java
class Solution {
    public int numTrees(int n) {
        //DP
        int[] G = new int[n + 1];
        G[0] = 1;
        G[1] = 1;
        
        for(int i = 2; i <= n; i++) {
            for(int j = 1; j <= i; j++) {
                G[i] += G[j - 1] * G[i - j];
            }
        }
        return G[n];
    }
}
```

Time complexity: **O(N^2)**
Space complexity: **O(N)**

## [95. Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

```
Input: (int)Given an integer n.

Output:(List<TreeNode>) Return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.
```

Solution: DFS + BST traversal

```java
class Solution {
    public List<TreeNode> generateTrees(int n) {
        List<TreeNode> res = new ArrayList<>();
        res = helper(1, n);
        return res;
    }
    public List<TreeNode> helper(int start, int end) {
        List<TreeNode> res = new ArrayList<>();
        if(start > end) res.add(null);
        for(int i = start; i <= end; i++) {
            List<TreeNode> leftList = helper(start, i - 1);
            List<TreeNode> rightList = helper(i + 1, end);
            for(TreeNode left : leftList) {
                for(TreeNode right : rightList) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    res.add(root);
                }
            }
        }
        return res;
    }
}
```

Time compleixity: **O(4^N / (N^(1/2)))** (Catalan Number)
Space complexity: **O(4^N / (N^(1/2)))** 



**Summary:**

1. Master BST inorder traversal(recursive + iterative)
2. Master the basic BST operations(search, delete and add)
3. Be familiar and comfortable with BST Iterator(always remember the default methods hasNext() and next())

# 4. LCA of Binary Tree

## [235. Lowest Common Ancestor of a Binary Search Tree]

```
Input:  binary search tree (BST), 
Output: the lowest common ancestor (LCA) of two given nodes in the BST.
```
思路：
    
    1. 如果p和q都在root的左子树上，那么LCA就在左子树
    2. 如果p和q都在root的右子树，那么recursively call 右子树
    3. 如果p和q各自一边，那么root就是LCA
   
code
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left, p, q);
        if(root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);
        return root;
    }
}
```

## [236. Lowest Common Ancestor of a Binary Tree]

描述

```
Input: binary tree
Output: lowest common ancestor (LCA) of two given nodes in the tree.
```

思路：

1. 初始一个hashmap和hashset，在遍历binary tree的时候记录parent和curr node的关系，key 为curr node, value 为 parent
2. 当遍历完binary tree之后，从p出发，自底向上，直到p为空，向上过程中存储当前节点p到hashset里面
3. 在从q出发，自底向上，向上过程中检查当前节点q是否在hashset里面，如果是，当前q即为LCA

code
```java
class Solution {
    Map<TreeNode, TreeNode> nodeToParent = new HashMap<>();
    Set<TreeNode> set = new HashSet<>();
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;
        dfs(root);
        while(p != null) {
            set.add(p);
            p = nodeToParent.get(p);
        }
        while(q != null) {
            if(set.contains(q)) {
                return q;
            }
            q = nodeToParent.get(q);
        }
        return null;
    }
    public void dfs(TreeNode root) {
        if(root == null) return;
        if(root.left != null) {
            nodeToParent.put(root.left, root);
            dfs(root.left);
        }
        if(root.right != null) {
            nodeToParent.put(root.right, root);
            dfs(root.right);
        }
    }
}
```

