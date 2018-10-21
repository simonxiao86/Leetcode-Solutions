### 题目

給出一个可能包含重复的整数数组 和一个大小为k的滑动窗口 从左至右在数组中滑动这个窗口 找到数组中

每个窗口内的最大值

给出数组 [1,2,7,7,8], 滑动窗口大小为 k = 3. 返回 [7,7,8].

最开始，窗口的状态如下：

[1, 2 ,7 ,7 , 8], 最大值为 7;

然后窗口向右移动一位：

[1, 2, 7, 7, 8], 最大值为 7;

最后窗口再向右移动一位：

[1, 2, 7, 7, 8], 最大值为 8.

### 思路

1.首先是最直观的 每次从起点i遍历一遍窗口长度j = i, i + k，找最大值，两层for循环，时间复杂度O(n * k)

2.因为是最大的元素 进进出出 考虑 大顶堆 每次移动，加入右边元素O(logk)，减去左边元素O(logk)，返回maxheap中的最大值O(1)，时间复杂度为O(n * logk)

3.使用deque 维护一个递减的双端队列


### 解法

#### Python

```
from collections import deque


class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        res = []
        d = deque()
        for i in range(len(nums)):
            while d and d[-1] < nums[i]:
                d.pop()
            d.append(nums[i])
            if i > k - 1 and d[0] == nums[i - k]:
                d.popleft()
            if i >= k - 1:
                res.append(d[0])
                
        return res

```