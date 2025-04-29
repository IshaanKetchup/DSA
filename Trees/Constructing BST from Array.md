## Constructing BST from Array

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) {
        val = x;
    }
}

public class BSTBuilder {
    public static TreeNode insert(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        if (val < root.val)
            root.left = insert(root.left, val);
        else
            root.right = insert(root.right, val);
        return root;
    }

    public static TreeNode buildBST(int[] arr) {
        TreeNode root = null;
        for (int val : arr) {
            root = insert(root, val);
        }
        return root;
    }

    public static void main(String[] args) {
        int[] arr = {5, 3, 7, 2, 4, 6, 8};
        TreeNode root = buildBST(arr);
        // BST is now built
    }
}


```
