---
title: ProblemJBlackAndWhite
date: 2020-08-28 10:38:11
tags:
categories: 2019NCNARegionalContest
---

[点这里](https://ncna19.kattis.com/problems/thisaintyourgrandpascheckerboard)
```cpp
#include <iostream>
#include <cstdio>
using namespace std;
char grid[26][26];
int main()
{
    int n;
    int ans = 1;
    int wnumr = 0;
    int wnumc = 0;
    scanf("%d",&n);
    for(int i = 0;i < n;i ++)
    {
        scanf("%s",grid[i]);
    }
    for(int i = 0;i < n;i ++)
    {
        wnumr = wnumc = 0;
        for(int j = 0;j < n;j ++) //既当行也当列
        {
            if(grid[i][j] == 'W')
            {
                wnumr++;
            }
            if(grid[j][i] == 'W')
            {
                wnumc++;
            }
        }
        for(int j = 0;j+2 < n;j ++) //既当行也当列
        {
            if(grid[i][j]==grid[i][j+1]&&grid[i][j+1]==grid[i][j+2])
            {
                ans = 0;
            }
            if(grid[j][i]==grid[j+1][i]&&grid[j+1][i]==grid[j+2][i])
            {
                ans = 0;
            }
        }
        if(wnumr+wnumr!=n||wnumc+wnumc!=n) //判断数量是否相等
        {
            ans = 0;
        }
    }
    printf("%d",ans);
    return 0;
}
```

> 就遍历就可以了