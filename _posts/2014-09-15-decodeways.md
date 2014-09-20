---
title: Decodeways
layout: default
permalink: Decodeways.html
category: blog
tags: Alogrithm
description: A message containing letters from A-Z is being encoded to numbers using the following mapping
---

<p>A message containing letters from A-Z is being encoded to numbers using the following mapping: </p>
<p>'A' -> 1 'B' -> 2 ... 'Z' -> 26</p> 
<p>Given an encoded message containing digits, determine the total number of ways to decode it. For example, Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12). The number of ways decoding "12" is 2.</p>
<p>Problem link: <a href="https://oj.leetcode.com/problems/decode-ways/">https://oj.leetcode.com/problems/decode-ways/</a></p>

<p>分析:</p>
<p>典型的动态规划题。对于输入的字符串s，用A[k]表示从s的第k个字符开始的子串的反解码个数，于是A[0]即为所求。</p>
<p>对于A[k],可以分为两种情况:</p>
<p>(1) s[k]可以独立反解码，即处于1到9之间，那么A[k] += A[k-1]<br>
(2) s[k:k+2)可以反解码，即处于10到26之间，那么A[k] += A[k-2]</p>
<p>最后对于base的情况, 有A[s.length] = 1, A[s.length-1] 根据最后一个字符的数值情况为1为0（或者定义A[s.length+1] = 0, 将A[s.length-1]泛化成一般情况）。</p> 



{% highlight python %}
class Solution:
    # @param s, a string
    # @return an integer
    def numDecodings(self, s):
        if s is None or len(s) == 0:
            return 0
        if len(s) == 1:
            return 1 if 1 <= int(s) <= 9 else 0
        k = len(s) - 2
        x = 1
        y = 1 if 1 <= int(s[k + 1]) <= 9 else 0
        while k != -1:
            tmp = 0
            if 1 <= int(s[k]) <= 9:
                tmp += y
            if 10 <= int(s[k:k + 2]) <= 26:
                tmp += x
            x = y
            y = tmp
            k -= 1
        return y  
{% endhighlight %}


	
