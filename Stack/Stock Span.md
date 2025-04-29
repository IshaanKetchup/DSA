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
