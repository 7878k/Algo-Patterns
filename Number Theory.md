# Number Theory

###### 快速幂 (Binary Exponentiation)

我们将取幂的任务按照指数的二进制表示来分割成更小的任务

3^13^ = 3^(1001)^~2~= 3^8^ * 3^4^ * 3^1^  

```python
# Python Version
def binpow(a, b):
    if b == 0:
        return 1
    res = binpow(a, b // 2)
    if (b % 2) == 1:
        return res * res * a
    else:
        return res * res
```

```python
# Python Version 2
def binpow(a, b):
    res = 1
    while b > 0:
        if (b & 1):
            res = res * a
        a = a * a
        b >>= 1
    return res
```

example: 

```java
// 50. Pow(x, n)
// Time: O(logn); Space: O(1)

class Solution {
    public double myPow(double x, int n) {
        long num = n;
		// 如果x是负数，指数变复数，然后再去倒数
        return num > 0 ? fastPow(x, num) : 1.0 / fastPow(x, -num);
    }
    
	// 快速幂
    private double fastPow(double x, long n) {
        if (n == 0) {
            return 1.0;
        }
        
        double res = 1.0;
        
        while (n > 0) {
			// 如果次方是奇数，就要多乘1个
            if ((n & 1) == 1) {
                res *= x;
            }
            x *= x;
			// 除以2
            n >>= 1;
        }
        return res;
    }
}
```

------

###### 进位制 (base)

二进制：只有0，1两个数字。

八进制：有0，1，2，3，4，5，6，7八个数字。 一般情况下，八进制数以```oxx``` (其中*o*为八进制的前缀，

*xx*是八进制数)的形式来表示。

十六进制：有十六个数字。一般情况下，十六进制数以 `0xdbf`（其中 `0x` 为十六进制数的前缀）的形式来表示。



### 十进制转二进制/八进制/十六进制[¶](https://oi-wiki.org/math/base/#_5)

这里以二进制为例来演示，其他进制的原理与其类似。

整数部分，把十进制数不断执行除 2 操作，直至商数为 0。读余数从下读到上，即是二进制的整数部分数字。小数部分，则用其乘 2，取其整数部分的结果，再用计算后的小数部分依此重复计算，算到小数部分全为 0 为止，之后从上到下，读所有计算后整数部分的数字，即为二进制的小数部分数字



```
将33.25转化为二进制数
整数部分：
33/2=16 ......1
16/2=8  ......0
8/2=4   ......0
4/2=2   ......0
2/2=1   ......0
1/2=0   ......1
小数部分：
0.25*2=0.5  0
0.5*2=1     1
```

```java
    public String base2(int N) {
        StringBuilder res = new StringBuilder();
        while (N != 0) {
            res.append(N & 1);
            N = N >> 1;
        }
        return res.length() > 0 ? res.reverse().toString() : "0";
    }

```

```java
    public String baseNeg2(int N) {
        StringBuilder res = new StringBuilder();
        while (N != 0) {
            res.append(N & 1);
            N = -(N >> 1);
        }
        return res.length() > 0 ? res.reverse().toString() : "0";
    }
```



### 二进制/八进制/十六进制转十进制[¶](https://oi-wiki.org/math/base/#_6)

还是以二进制为例。

二进制数转换为十进制数，只需将每个位的值，乘以 次即可，其中 为当前位的位数，个位的位数为 0。

```
将11010.01(2)转换为十进制数
11010.01(2)=1*2^4+1*2^3+0*2^2+1*2^1+0*2^0+0*2^(-1)+1*2(-2)
        =26.25
```



### 二进制/八进制/十六进制间的相互转换[¶](https://oi-wiki.org/math/base/#_7)

一个八进制位可以用 3 个二进制位来表示（因为 ），一个十六进制位可以用 4 个二进制位来表示（），反之同理。

------

###### 辗转相除法 (Euclidean algorithm)/最大公约数 gcd

两个整数的最大公约数等于其中较小的数和两数相除余数的最大公约数 (a > b)

时间复杂度是```log(n)```

```python
def gcd(a, b)
	while b != 0
    	t = a % b
        a = b
        b = t
    return a
```

```java
// 1979. Find Greatest Common Divisor of Array
// Time: O(n + logMax); Space: O(1)

class Solution {
    public int findGCD(int[] nums) {
        int max = 0;
        int min = 1001;
        
        for (int num : nums) {
            max = Math.max(num, max);
            min = Math.min(num, min);
        }
        return gcd(max, min);
    }
    
	// 辗转相除法
    private int gcd(int a, int b) {
        while (b != 0) {
            int temp = a % b;
            a = b;
            b = temp;
        }
        return a;
    }
}
```

------



###### 质数/素数 (prime number)

在大于1的自然数中，除了1和该数自身外，无法被其他自然数整除的数是**质数**。如果大于1的自然数不是子树，那么就是**合数**。

```java
boolean isPrime(a) {
    if (a < 2) return false;
    for (int i = 2; i * i <= a; i++) {
        if (a % i == 0) return false;
    }
    return true;
}
```

```java
// LCP 02. 分式化简
// https://leetcode-cn.com/problems/deep-dark-fraction/

class Solution {
    public int[] fraction(int[] cont) {
        int[] res = new int[2];
        res[0] = 1;
        res[1] = 0;

        for (int i = cont.length - 1; i >= 0; i--) {
            int temp = res[1];
            res[1] = res[0];
            res[0] = cont[i] * res[1] + temp;
        }
        return res;
    }
}
```

------

###### 质数筛法

*埃氏筛*：如果x是合数，那么x的倍数也是合数。如果我们从小到大考虑每个数，然后同时把当前这个数的所有（比自己大的）倍数记为合数，那么运行结束的时候没有被标记的数就是质数.

```java
// 204. Count Primes
// Time: O(nloglogn); Space:O(n)
// 埃式筛 首先找第一个质数，然后把他的倍数都标记，
// 然后第二个... 直到最新prime^2 >= n 说明所有质数找到

class Solution {
    public int countPrimes(int n) {
        int[] isPrime = new int[n];
        int ans = 0;
        Arrays.fill(isPrime, 1);
        
        for (int i = 2; i < n; i++) {
            if (isPrime[i] == 1) {
                ans++;
            }
            if ((long)i * i < n) {
				// 因为从2到i - 1的倍数已经算了，这里直接从i开始
                for (int j = i * i; j < n; j += i) {
                    isPrime[j] = 0;
                }
            }
        }
        return ans;
    }
}
```

