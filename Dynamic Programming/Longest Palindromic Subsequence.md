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
