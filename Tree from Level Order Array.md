## Constructing Tree from Level Order Array

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) {
        val = x;
    }
}

public class BinaryTreeBuilder {
    public static TreeNode buildTree(int[] arr, int i) {
        if (i >= arr.length) return null;

        TreeNode node = new TreeNode(arr[i]);
        node.left = buildTree(arr, 2 * i + 1);
        node.right = buildTree(arr, 2 * i + 2);

        return node;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6};
        TreeNode root = buildTree(arr, 0);
        // Tree built with root at index 0
    }
}

```
