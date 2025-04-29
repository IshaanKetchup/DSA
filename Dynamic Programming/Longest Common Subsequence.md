## Longest Common Subsequence of 2 Strings

```java
import java.util.*;
class Main {
    static int[][]dp;
    public static void main(String[] args) {
        String x = "ABCD";
        String y = "ACFD";
        dp = new int[x.length()+1][y.length()+1];
        for(int[] row: dp) Arrays.fill(row, -1);
        System.out.print(LCS(x,y));
    }
    
    public static String LCS(String x, String y){
        StringBuilder lcsStr = new StringBuilder();
        int i = x.length(), j = y.length();
        int temp = findLen(x,y,i,j);
        while(i>0 && j>0){
            if(x.charAt(i-1) == y.charAt(j-1)){
                lcsStr.append(x.charAt(i-1));
                i--; j--;
            }
            else if (dp[i-1][j] > dp[i][j-1]) i--;
            else j--;
        }
        return lcsStr.reverse().toString();
    }
    
    public static int findLen(String x, String y, int i,  int j){
        if(i==0 || j==0) return 0;
        if(dp[i][j] != -1) return dp[i][j];
        
        if(x.charAt(i-1) == y.charAt(j-1)) {
            dp[i][j] = 1+ findLen(x,y, i-1, j-1);
        }
        else{
            dp[i][j] = Math.max(findLen(x,y, i-1,j), findLen(x,y,i,j-1));
        }
        return dp[i][j];
        
    }
   
}
```
