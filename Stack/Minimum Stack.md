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
