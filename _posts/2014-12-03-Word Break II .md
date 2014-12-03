---
title: Word Break II
layout: default
permalink: Word Break II.html
category: blog
tags: Alogrithm
description: Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word
---

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].

<p>Problem link: <a href="https://oj.leetcode.com/problems/word-break-ii/">https://oj.leetcode.com/problems/word-break-ii/</a></p>

<p>分析:</p>
<p>典型的动态规划题。虽然递归可以解决，但是在数据过大时会超时</p>

<p>代码如下：</p>

{% highlight python %}
class Solution:
    # @param s, a string
    # @param dict, a set of string
    # @return a list of strings
    def wordBreak(self, s, dict):
        if s is None or dict is None:
            return []
        if len(dict) == 0 or len(s) == 0:
            return []
        l = len(s)
        i,j = l - 1, 0
        result = []
        while j != l:
            result.append([])
            j += 1
        while i != -1:
            j = i
            while j != l + 1:
                if s[i:j] in dict:
                    if j == l:
                        result[i].append(s[i:j])
                    else:
                        for tmp in result[j]:
                            result[i].append(s[i:j] + " " + tmp)
                j = j + 1
            i = i - 1
        #print(s,result)
        return result[0]
{% endhighlight %}


	
