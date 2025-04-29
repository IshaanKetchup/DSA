## BFS and DFS for Tree

```java
public static void dfs(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    dfs(root.left);
    dfs(root.right);
}

public static void bfs(TreeNode root){
    if(root == null) return;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while(!queue.isEmpty()){
        TreeNode curr = queue.poll();
        System.out.print(curr.val + " ");
        if(curr.left != null) queue.add(curr.left);
        if(curr.right != null) queue.add(curr.right);
    }
}
```
