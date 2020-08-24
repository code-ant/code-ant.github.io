---
title: 二叉树
date: 2020-08-21 14:50:03
tags: [算法,树,二叉树,数据结构]
categories: [算法与数据结构]
---

数据结构总结——二叉树

总结常见的二叉树相关的算法以及代码实现

<!--more-->

**二叉树定义**

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int x) {
        val = x;
    }
}
```



###  前序遍历

- 递归

```java
//递归方法(同理可得中序遍历和后序遍历的递归方法)
List<Integer> result = new ArrayList<>();

public List<Integer> preorderTraversal(TreeNode root) {
    if (root != null) {
        result.add(root.val);
        preorderTraversal(root.left);
        preorderTraversal(root.right);
    }
    return result;
}
```

- 迭代

```java
    //迭代方法
    public static List<Integer> preOrderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        LinkedList<Integer> result = new LinkedList<>();
        if (root == null) {
            return result;
        }

        stack.push(root);
        while (!stack.isEmpty()){
            TreeNode temp = stack.pop();
            result.add(temp.val);
            if(temp.right!=null){
                stack.push(temp.right);
            }
            if(temp.left!=null){
                stack.push(temp.left);
            }
        }
        return result;
    }
```








### 中序遍历

```java
//递归
List<Integer> result = new ArrayList<>();

public List<Integer> inorderTraversal(TreeNode root) {
    if (root != null) {
        inorderTraversal(root.left);
        result.add(root.val);
        inorderTraversal(root.right);
    }
    return result;
} 
//迭代方法同前序遍历
```



### 后序遍历

```java
    //递归
    List<Integer> result = new ArrayList<>();

    public List<Integer> postorderTraversal(TreeNode root) {
        if (root != null) {
            postorderTraversal(root.left);
            postorderTraversal(root.right);
            result.add(root.val);
        }
        return result;
    }
    //迭代方法同前序遍历
```

### 深度优先遍历

```java
//DFS
同前序遍历
```

### 广度优先遍历

```java
    //BFS
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new LinkedList<>();
            for (int i = 0; i < size; ++i) {
                TreeNode cur = q.peek();
                q.poll();
                if (cur == null) {
                    continue;
                }
                level.add(cur.val);
                q.offer(cur.left);
                q.offer(cur.right);
            }
            if (!level.isEmpty()) {
                res.add(level);
            }
        }
        return res;
    }
```



### 计算树的高度

```java
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        int leftde = maxDepth(root.left);
        int rightde = maxDepth(root.right);
        return Math.max(leftde, rightde) +1;
    }
```



### 计算树的直径

- [leetcode-543](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

```java
    int result;
    public int diameterOfBinaryTree(TreeNode root) {
        depth(root);
        return result>0?result-1:0;
    }

    public int depth(TreeNode node){
        if(node == null){
            return 0;
        }
        int L = depth(node.left);
        int R = depth(node.right);
        result = Math.max(result,L+R+1);
        return Math.max(R,L) +1;
    }
```



### 镜像二叉树

- [leetcode](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

```java
    public TreeNode mirrorTree(TreeNode root) {
        if (root == null)
            return null;

        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        mirrorTree(root.left);
        mirrorTree(root.right);
        return root;
    }
```



### 判断一个树是否镜像

- [leetcode-101](https://leetcode-cn.com/problems/symmetric-tree/)

```java
    public boolean isSymmetric(TreeNode root) {
        if(root ==null){
            return true;
        }
        return compare(root.left,root.right);
    }
    public boolean compare(TreeNode mleft, TreeNode mright){
        if(mleft ==null&& mright == null){
            return true;
        }
        if(mleft == null || mright == null || mleft.val != mright.val) {
            return false;
        }
        return compare(mleft.left, mright.right) && compare(mleft.right, mright.left);
    }
```



### 二叉搜索树转化为累加树

- [leetcode-538](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

```java
    int sum = 0;
    public TreeNode convertBST(TreeNode root) {

        if(root != null) {
            convertBST(root.right);
            sum += root.val;
            root.val = sum;
            convertBST(root.left);
        }
        return root;
    }
```

