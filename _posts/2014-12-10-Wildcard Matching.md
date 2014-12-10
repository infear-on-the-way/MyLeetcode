---
title: Wildcard Matching
layout: default
permalink: Wildcard Matching.html
category: blog
tags: Alogrithm
description: Implement wildcard pattern matching with support for '?' and '*'.
---

'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false

<p>Problem link: <a href="https://oj.leetcode.com/problems/wildcard-matching/">https://oj.leetcode.com/problems/wildcard-matching/</a></p>

<p>分析:</p>
典型的动态规划题。虽然递归可以解决，但是在数据过大时会超时。

用A(i,j)表示s[i:]和p[j:]的匹配情况：  
当s[i]==p[j] or p[j]=='?'时，A(i,j) = A(i+1,j+1)。否则当p[j]=='*'时，A(i,j)=A(i,j+1) or A(i+1,j).注意只要A(i+1,j)就够了，  
因为当A(i+1,j)为True时，*只要再多包含一个字符，就可以使得A(i,j)为True，否则A(i,j)和A(i+1,j)一样为False。 

一开始几个case没过，所以针对特殊情况作了特别处理，比如p中非*字符的个数如果大于s的长度，就直接返回False。  

<p>代码如下：</p>

{% highlight python %}
class Solution:
    # @param s, an input string
    # @param p, a pattern string
    # @return a boolean
    def isMatch(self, s, p):
        if s is None:
            return True
        if p is None:
            return False
        l1, l2 = len(s), len(p)
        tmp = 0
        c = 0
        while tmp != l2:
            if p[tmp] != '*':
                c = c + 1
            tmp += 1
        if c > l1:
            return False 
        
        if l1 != 0 and l2 != 0:
            if p[0] != '*' and p[0] != '?' and p[0] != s[0]:
                return False
        
        A = {}
        i = 0
        while i != l1:
            A[i] = False
            i = i + 1
        A[i] = True
 
        j = l2 - 1
        i = l1
        tmp = False
        while j != -1:
            B = {}
            #print(A)
            while i != -1:            
                if i == l1:
                    B[i] = (A[i] and (p[j] == '*'))
                elif s[i] == p[j] or p[j] == '?':
                    B[i] = A[i + 1]
                elif p[j] == '*':
                    B[i] = (A[i] or B[i + 1])
                else:
                    B[i] = False
                i = i - 1
            A = B
            #print(j, A)
            i = l1
            j = j - 1
        return A[0]
{% endhighlight %}


	
