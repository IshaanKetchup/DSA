Iterate from right to left (so as to store "future" elements)
Pop elements of stack that are less than current element arr[i]
If stack.empty(), nge[i] = -1, else nge[i] = stack.top()
Push arr[i] to stack

```cpp
vector<int> nextGreaterElementRight(vector<int>& arr) {
    int n = arr.size();
    vector<int> nge(n);
    stack<int> st; // store values

    for (int i = n - 1; i >= 0; i--) {
        while (!st.empty() && st.top() <= arr[i]) {
            st.pop();
        }
        nge[i] = st.empty() ? -1 : st.top();
        st.push(arr[i]);
    }
    return nge;
}
```
