# 排序

**Merge Sort**

1. 确定分界点: 

   ```java
   mid = l + r >> 1
   ```

2. 递归排序 left, right

3. 归并， 合二为一

```c++
void merge_sort(int q[], int l, int r)
{
    if (l >= r) return;

    int mid = l + r >> 1;
    merge_sort(q, l, mid);
    merge_sort(q, mid + 1, r);

    int k = 0, i = l, j = mid + 1;
    while (i <= mid && j <= r)
        // 需要一个temp数组
        if (q[i] <= q[j]) tmp[k++] = q[i++];
        else tmp[k++] = q[j++];

    while (i <= mid) tmp[k ++ ] = q[i++];
    while (j <= r) tmp[k ++ ] = q[j++];
	
    // 每次递归都会有新的left, temp
    for (i = l, j = 0; i <= r; i++, j ++) q[i] = tmp[j];
}

```

------



**Quick Sort**

1. 确定分界点	q[l + r >> 1]
2. 调整区间
3. 递归处理左右两段

```c++
void quick_sort(int q[], int l, int r)
{
    if (l >= r) return;

    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while (i < j)
    {
        do i ++ ; while (q[i] < x);
        do j -- ; while (q[j] > x);
        if (i < j) swap(q[i], q[j]);
    }
    quick_sort(q, l, j), quick_sort(q, j + 1, r);
```

