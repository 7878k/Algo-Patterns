# bit manipulation

& 与运算： 两个位都是 1 时，结果才为 1，否则为 0

| 或运算： 两个位都是 0 时，结果才为 0，否则为 1

^ 异或运算： 两个位相同则为 0，不同则为 1

~ 取反运算：0 则变为 1，1 则变为 0

<< 左移运算：向左进行移位操作，高位丢弃，低位补 0 （每左移一位相当于乘一次2）

\>> 右移运算：向右进行移位操作，正数右移，高位用 0 补，负数右移，高位用 1 补（每右移一位相当于除一次2）

- 无符号右移 `>>>`当负数使用无符号右移时，用 0 进行补位

  

------

**（1）交换律**

**（2）结合律（即(a^b)^c == a^(b^c)）**

**（3）对于任何数x，都有x^x=0，x^0=x**

**（4）自反性 A ^ B ^ B = A ^ 0 = A**

------



**判断一个数的奇偶**

```java
i & 1
```

_最右位是1则是偶数，反之奇数_

```java
i & 1 == 0 偶数; i & 1 != 0 奇数
```



**lowbit(x):  返回x的最后一位1**

```c++
x & (-x) = x & (~x + 1)
```

usage: 统计x里面1的个数



**把最低位的1变成0**：

```c++
x & (x - 1)
```



**把最低位的0变成1**

```java
x | (x + 1)
```

**最低有效位 (the least significant bit, LSB)**

指一个二进制数字中的第0位（即最低位），具有权值为2^0，可以用它来检测数的奇偶性。

------

**设置值**

_将k位设置为1_

```java
A = A | (1 << (k - 1))
```

将k位设置位0

```java
A = A & ~(1 << (k - 1))
```

_将第k位取反_

```java
A = A ^ (1 << (k - 1))
```

**计算/判断**

 _计算m中1的数量_

```java
// 191. Number of 1 Bits
// Time: O(logn); Space: O(1)

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



_判断m是否是2的非负整数次幂_

1. ```c++
   n & (n - 1) == 0
   ```

2. ```
   (n & -n) == n
   ```



```java
// 231. Power of Two

// 如果N是2的幂次，那么N>0并且N的二进制只有一个1
// 用N & (N - 1）消去最后一个1后，只能返回0
class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && ((n & (n -1)) == 0);
    }
}

class Solution {
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & -n) == n;
    }
}
```



_删除最低有效位_

```
x >> 1
```



_遍历m中所有非空子集_

例如：m='101', return '001', '100', '101'

```c++
   int sub = k;
    do {
        sub = (sub - 1) & k;
    } while(sub != k);
```

```java
function get_subset(bitmask)
    subset = bitmask
    answer = [bitmask]
    while subset != 0
        subset = (subset - 1) & bitmask
        put subset into the answer list
    end while
    return answer
end function
```

其中bitmask表示一个二进制数，subset会遍历所有bitmask的子集，并将所有子集放入answer中

------



**获取**

_求n的第k位数字_

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



_最低有效位_

```
x & 1
```



_最高有效位_

```java
private static int mostSignificantBit(int myInt){
    int i = 0;
    while (myInt != 0) {
        ++i;
        myInt >>>= 1;
    }
    return i;
}
```

