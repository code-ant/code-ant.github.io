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



### 广度优先遍历



### 计算树的高度



### 计算树的直径



### 镜像二叉树



### 判断一个树是否镜像



### 二叉树转化为累加树

