---
title: Python的深拷贝和浅拷贝
date: 2018-04-20 17:16:52
tags: [python]
---

今天实现Python的排序问题，比如如下的代码：

```py
def merge(self, l, r):
    if l == r - 1 or l == r:
        return

    mid = (l + r) // 2
    self.merge(l, mid)
    self.merge(mid, r)

    length = r - l
    left = [i for i in self.data[l:mid]]
    right = [i for i in self.data[mid:r]]

    i = j = 0
    k = l
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            self.data[k] = left[i]
            i += 1
        else:
            self.data[k] = right[j]
            j += 1
        k += 1
    if i == len(left):
        while k - l < length:
            self.data[k] = right[j]
            k += 1
            j += 1
    else:
        while k - l < length:
            self.data[k] = left[i]
            i += 1
            k += 1

def MergeSort(self):
    len = self.n
    self.merge(0, len)
    return self.data
```

以上是正确的写法，但是一开始的写法是直接使用了：

```py
left = self.data[l:mid]
right = self.data[mid+1:r]
```
这样子实际上 ` left ` 和 ` right ` 就是一个实际的应用，也就是说修改这个的时候会同时原来的 ` self.data `
的数据，为了避免这个问题，我们的拷贝必须使用 一些特殊的技巧：

    
```py 
newList = list(arr[l:r])
newList = [i for i in arr[l:r]]

import copy as cp # emmmm，这个缩写，233333
newList = cp.copy(arr[l:r])
```
一般不用引入一个包来解决问题，前两个已经很不错了

