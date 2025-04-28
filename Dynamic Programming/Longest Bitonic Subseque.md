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
