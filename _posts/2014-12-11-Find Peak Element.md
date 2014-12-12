---
title: Find Peak Element 
layout: default
permalink: Find Peak Element.html
category: blog
tags: Alogrithm
description: A peak element is an element that is greater than its neighbors.
---

A peak element is an element that is greater than its neighbors.

Given an input array where num[i] ≠ num[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that num[-1] = num[n] = -∞.

For example, in array [1, 2, 3, 1], 3 is a peak element and your function should return the index number 2.

<p>Problem link: <a href="https://oj.leetcode.com/problems/find-peak-element/">https://oj.leetcode.com/problems/find-peak-element/</a></p>

<p>分析:</p>
看了提示，必须要在log(n)的时间内解决，所以很容易想到二分。  
需要注意到只要存在i使得num[i]>num[i-1]，那么num[i:]中一定会有极点，否则num[:i]中就一定会有极点。
 
<p>代码如下：</p>

{% highlight python %}
class Solution:
    # @param num, a list of integer
    # @return an integer
    def findPeakElement(self, num):
        if num is None or len(num) == 0:
            return -1
        if len(num) == 1:
            return 0
        mid = len(num)//2
        if num[mid] > num[mid - 1]:
            return mid + self.findPeakElement(num[mid:])
        else:
            return self.findPeakElement(num[0:mid])   
{% endhighlight %}


	
