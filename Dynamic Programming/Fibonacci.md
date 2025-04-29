## Fibonacci

```java
public static void main(String[] args) {
    int n=10;
    int[] memo = new int[n+1];
    Arrays.fill(memo, -1);
    memo[0] =0;
    memo[1] = 1;
    System.out.println(fib(n, memo));
    for(int i: memo){
        System.out.print(i+" ");
    }
}

public static int fib(int x, int[] memo){
    if(memo[x] != -1) return memo[x];
    memo[x] = fib(x-1, memo) + fib(x-2, memo);
    return memo[x];
}

```
