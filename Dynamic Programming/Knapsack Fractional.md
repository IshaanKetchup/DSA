## Fractional Knapsack
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
