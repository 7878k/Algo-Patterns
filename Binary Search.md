# Binary Search

二分模板一共有两个，分别适用于不同情况。
算法思路：假设目标值在闭区间```[l, r]```中， 每次将区间长度缩小一半，当```l = r```时，我们就找到了目标值。

**版本1**

当我们将区间```[l, r]```划分成```[l, mid]```和```[mid + 1, r]```时，其更新操作是```r = mid```或者```l = mid + 1```; 计算mid时不需要加1。

```java
int binarySearch(int left, int right) {
    while (left < right) {
        int mid = left + right >> 1;
        if (check(mid)) right = mid;
        else left = mid + 1;
    }
    return left;
}
```



**版本2**

当我们将区间```[l, r]```划分成```[l, mid - 1]```和```[mid, r]```时，其更新操作是```r = mid - 1```或者```l = mid```，此时为了防止死循环，计算mid时需要加1。

```java
int binarySearch(int left, int right) {
    while (left < right) {
        int mid = left + right + 1 >> 1;
        if (check(mid)) left = mid;
        else right = mid - 1;
    }
}
```



example:

```java
// 34. Find First and Last Position of Element in Sorted Array
// Time: O(logn); Space: O(1)

public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int len = nums.length;
        if (len == 0) {
            return new int[]{-1, -1};
        }

        int firstPosition = findFirstPosition(nums, target);
        if (firstPosition == -1) {
            return new int[]{-1, -1};
        }

        int lastPosition = findLastPosition(nums, target);
        return new int[]{firstPosition, lastPosition};
    }

    private int findFirstPosition(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left) / 2;
            // 小于一定不是解
            if (nums[mid] < target) {
                // 下一轮搜索区间是 [mid + 1..right]
                left = mid + 1;
            } else {
                // nums[mid] > target，下一轮搜索区间是 [left..mid]
                right = mid;
            }
        }

        if (nums[left] == target) {
            return left;
        }
        return -1;
    }

    private int findLastPosition(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = left + (right - left + 1) / 2;
            if (nums[mid] > target) {
                // 下一轮搜索区间是 [left..mid - 1]
                right = mid - 1;
            } else 
                // 下一轮搜索区间是 [mid..right]
                left = mid;
            } 
        }
        return left;
    }
}
```

