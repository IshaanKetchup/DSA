## Longest Bitonic Subsequence

Create two arrays, I to count longest increasing subsequence, and D to count longest decreasing subsequence (reverse array, find increasing subsequence)

Basically a prefix/suffix problem, solution is given by max(I[i], D[i]) in array -1

```java
public static int LBS(int[] nums){
        int n = nums.length;
        if(n==0) return 0;
        int[] I = new int[n];
        int[] D = new int[n];
        I[0]=1;
        for(int i=1; i<n; i++){
            for(int j=0; j<i; j++){
                if(nums[j]<nums[i] && I[j]>I[i]) I[i] = I[j];
            }
            I[i]++;
        }
        D[n-1] = 1;
        D[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--) {
          for (int j = n - 1; j > i; j--) {
            if (nums[j] < nums[i] && D[j] > D[i]) {
              D[i] = D[j];
            }
          }
          D[i]++;
        }
        int lbs = 1;
        for(int i=0; i<n; i++){
            lbs = Integer.max(lbs, I[i]+D[i]-1);
        }
        return lbs;
    }
```


## Longest Palindromic Subsequence
Recursive + Memoization solution, 
Create memo to store, and fill with -1 initially
Iterate start = 0, end = n-1
if `str[start] == str[end]`, then `memo[start][end] = start++, end-- `
else, find max between `helper(start+1, end)` and `helper(start, end-1)`
	Basically move both individually, and see which performs better

```java
public static int LPS(String str){
       int n = str.length();
       int[][] memo = new int[n][n];
       for(int[] row: memo){
           Arrays.fill(row, -1);
       }
       return helper(str, 0, n-1, memo);
    }
public static int helper(String s, int start, int end, int[][] memo){
        if(start>end) return 0;
        if(start == end) return 1;
        if(memo[start][end] != -1) return memo[start][end];
        
        if(s.charAt(start) == s.charAt(end)) memo[start][end] = 2+helper(s, start+1, end-1, memo);
        else{
            memo[start][end] = Integer.max(helper(s, start+1, end, memo), helper(s, start, end -1, memo));
        }
        return memo[start][end];
    }
```

## Subset Sum
Recursive solution
the value of n holds the *last index* of the array, meaning this solution recursively finds the solution from last to first.

if `last element > targetSum` then you skip it by reducing n to n-1
else, try both cases, skipping and not skipping
`sS(arr, target - arr[n-1], n-1)` to include current element, 
`sS(arr, target, n-1)` to skip element

```java
public static boolean subsetSum(int[] arr, int targetSum, int n){
    if (targetSum == 0) return true;
    if (n==0) return false;
    
    if(arr[n-1]>targetSum) return subsetSum(arr, targetSum, n-1);
    return subsetSum(arr, targetSum - arr[n-1], n-1) || subsetSum(arr, targetSum, n-1);
}
```

## 0/1 Knapsack
Create custom class ItemValue which holds each item weight, value and cost
Array of ItemValues, which is easy to sort descending using `Arrays.sort(items, (a,b) -> Double.compare(b.cost,a.cost))`

Then iterate through sorted array, 
1. Compare `capacity` with `item.weight`
	2. if `capacity > item.weight` then add to knapsack: `total += item.value`, `capacity -= item.weight`
	3. else, try to add fractional portion, `fraction = capacity/item.weight` and `total += fraction * item.value` 

```java
public static double knapsack(int[] weights, int[] values, int capacity){
    ItemValue[] items = new ItemValue[weights.length];
    for(int i=0; i<weights.length; i++){
        items[i] = new ItemValue(values[i], weights[i]);
    }
    Arrays.sort(items, (a,b) -> Double.compare(b.cost, a.cost));
    double totalValue = 0.0;
    for(ItemValue item: items){
        if(capacity>= item.weight){
            capacity -= item.weight;
            totalValue += item.value;
        }
        else{
            double fraction = (double) capacity/item.weight;
            totalValue += fraction*item.value;
            break;
        }
    }
    return totalValue;
}

```
## Minimum Stack
Finding minimum element of stack
Basically keeping track of minimum element by logic:
PUSH: if smaller element than top of `minStack`, push it to minstack
POP: if top of `stack` == top of `minStack`, pop from both

```java
Stack<Integer>stack ;
Stack<Integer> minStack;
public Main(){
    stack = new Stack<>();
    minStack = new Stack<>();
}
public void push(int element){
    stack.push(element);
    if(minStack.isEmpty() || element<= minStack.peek()) minStack.push(element);
}
public void pop(){
    if(!stack.isEmpty()){
        int popped = stack.pop();
        if (popped == minStack.peek()) minStack.pop();
    }
}
public int top(){
    if(!stack.isEmpty()) return stack.peek();
    return -1;
}

public int getMin(){
    if(!minStack.isEmpty()) return minStack.peek();
    return -1;
}
```
## Stock Span
Creating array which shows number of passed days that current day is value is greater than
Logic:
1. Create stack, which holds the indices of previous days which had higher price than current
2. Remove all stock prices lower than current day from stack (while loop)
3. if stack empty, then no higher price exists -> `days = span[current] = current+1` (0 indexed)
4. else, `days = current - stack.top()`
5. push current day to stack, `stack.push(curr)`

```java
public static int[] calculateSpan(int[] arr){
    Stack<Integer> stack = new Stack<>();
    int n=arr.length;
    int[] span= new int[n];
    
    for(int i=0; i<n; i++){
        while(!stack.isEmpty() && arr[i] >= arr[stack.peek()]) stack.pop();
        span[i] = (stack.isEmpty())? (i+1) : (i-stack.peek());
        stack.push(i);
    }
    return span;

}
```

## Maximum Element in k-size sliding window - BRUTE FORCE
```java
public class Main {
    public static void printMaxInWindows(int[] arr, int k) {
        int n = arr.length;
        for (int i = 0; i <= n - k; i++) {
            int max = arr[i];
            for (int j = 1; j < k; j++) {
                if (arr[i + j] > max) {
                    max = arr[i + j];
                }
            }
            System.out.print(max + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 1, 2, 0, 5};
        int k = 3;
        printMaxInWindows(arr, k);
    }
}
```

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
