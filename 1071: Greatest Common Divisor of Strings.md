## #1071: Greatest Common Divisor of Strings

### Logic:
1. If str1 is n concatenations of str2, then str1 + str2 == str2 + str1
*  Example: str1 - ABABAB , str2 - AB
	* str1+ str2 = ABABAB / AB
	* str2 + str1 =  AB / ABABAB
	*  thus equal
2. If both are equal, it means that there is n-concatenations in the longer string
* Now we find GCD of lengths of both strings EZ
	
```cpp
class Solution {
    public:
        int gcd(int a, int b){
            if(a==0)
                return b;
            if(b==0)
                return a;
            if(a==b)
                return a;
            if(a>b)
                return gcd(a-b,b);
            return gcd(a, b-a);
        }
        string gcdOfStrings(string str1, string str2) {
            return (str1 + str2 == str2 + str1)? 
            str1.substr(0, gcd(size(str1),size(str2))): "";
        }
    };
```
