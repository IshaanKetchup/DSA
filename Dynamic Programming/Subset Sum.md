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
