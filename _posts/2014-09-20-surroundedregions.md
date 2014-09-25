---
title: Surrounded Regions 
layout: default
permalink: SurroundedRegions.html
category: blog
tags: Alogrithm
description: Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'
---

<p>Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'.</p>

<p>A region is captured by flipping all 'O's into 'X's in that surrounded region.</p>

For example,
X X X X  
X O O X  
X X O X  
X O X X

<p>After running your function, the board should be:</br>
X X X X
X X X X
X X X X
X O X X</p>

<p>Problem link: <a href="https://oj.leetcode.com/problems/surrounded-regions/">https://oj.leetcode.com/problems/surrounded-regions/</a></p>

<p>分析：本题的目的就是找出所有被'X'完全包围的'O',容易想到如果一个'O'可以和一个边界上的'O'连通，那这个'O'就没有被完全包围。
所以，思路就变成，遍历所有边界上的'O',并且从它出发，找到所有连通的'O'并且作上标记。
然后，再遍历一遍所有位置，如果这个位置上的字符为'O'，且没有被标记，说明这个'O'被完全包围，于是就把它改成'X'。</p>

<p>备注：不要用递归实现第一次遍历的过程，因为我前几次的实现都是用的递归，在输入规模到达400×400时，会出现StackOverFlow的问题。</p>
<p>代码如下：</p>

{% highlight python %}
class Solution:
    # @param board, a 2D array
    # Capture all regions by modifying the input board in-place.
    # Do not return any value.
    def solve(self, board):
        if board is None or len(board) == 0:
            return
        h, l = len(board), len(board[0])
        i = 0
        while i != h:
            board[i] = list(board[i])
            i += 1
        visited = {}
        i = 0
        while i != h:
            j = 0
            yy = {}
            while j != l:
                yy[j] = 0
                j += 1
            visited[i] = yy
            i += 1

        i = j = 0
        while j != l:
            if board[i][j] == 'O' and visited[i][j] == 0:
                self.visit(i, j, visited, board)
            j += 1

        i = j = 0
        while i != h:
            if board[i][j] == 'O' and visited[i][j] == 0:
                self.visit(i, j, visited, board)
            i += 1

        i = h - 1
        j = 0
        while j != l:
            if board[i][j] == 'O' and visited[i][j] == 0:
                self.visit(i, j, visited, board)
            j += 1

        i = 0
        j = l - 1
        while i != h:
            if board[i][j] == 'O' and visited[i][j] == 0:
                self.visit(i, j, visited, board)
            i += 1

        i = 0
        while i != h:
            j = 0
            while j != l:
                if board[i][j] == 'O' and visited[i][j] == 0:
                    board[i][j] = 'X'
                j += 1
            i += 1

    def visit(self, i, j, visited, board):
        s = []
        s.append(i)
        s.append(j)
        while len(s) != 0:
            j = s.pop()
            i = s.pop()
            visited[i][j] = True

            if (0 <= i - 1 < len(board) and 0 <= j < len(board[0])) and board[i - 1][j] == 'O' and visited[i - 1][
                j] == 0:
                s.append(i - 1)
                s.append(j)

            if (0 <= i + 1 < len(board) and 0 <= j < len(board[0])) and board[i + 1][j] == 'O' and visited[i + 1][
                j] == 0:
                s.append(i + 1)
                s.append(j)

            if (0 <= i < len(board) and 0 <= j + 1 < len(board[0])) and board[i][j + 1] == 'O' and visited[i][
                        j + 1] == 0:
                s.append(i)
                s.append(j + 1)

            if (0 <= i < len(board) and 0 <= j - 1 < len(board[0])) and board[i][j - 1] == 'O' and visited[i][
                        j - 1] == 0:
                s.append(i)
                s.append(j - 1)
     
{% endhighlight %}
