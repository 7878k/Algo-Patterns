# bit operation

**求n的第k位数字**

```c++
n >> k & 1 
```

1, 先把第K位移到最后一位：

```
n >> k
```

2, 看个位是几, 

`x & 1` produces a value that is either `1` or `0`, depending on the least significant bit of `x`: if the last bit is `1`, the result of `x & 1` is `1`; otherwise, it is `0`. This is a bitwise AND operation.

```
x & 1
```



**lowbit(x):  返回x的最后一位1**

```c++
x & (-x) = x & (~x + 1)
```

usage: 统计x里面1的个数



把最低位的1变成0：

```c++
n & (n - 1)
```



example: 

191. Number of 1 Bits

     ```java
     public class Solution {
         // you need to treat n as an unsigned value
         public int hammingWeight(int n) {
             int res = 0;
             
             while (n != 0) {
                 n -= lowbit(n); // 每次减去n的最后一位1
                 res++;
             }
             
             return res;
         }
         
         private int lowbit(int x) {
             return x & -x;
         }
     }
     ```

     

