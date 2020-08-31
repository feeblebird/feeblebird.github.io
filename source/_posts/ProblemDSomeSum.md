---
title: ProblemDSomeSum
date: 2020-08-27 20:42:36
tags:
categories: 2019NCNARegionalContest
---

[点这里](https://ncna19.kattis.com/problems/somesum)

```cpp
#include <iostream>
#include <cstdio>
using namespace std;

int main()
{
    int n;
    scanf("%d",&n);
    if(n%2==0)
    {
        int tem = n / 2;
        if(tem%2==0)
        {
            printf("Even");
        }else
        {
            printf("Odd");
        }
    }else
    {
        printf("Either");
    }
    return 0;
}
```

> 当n==2时，和一定是奇数。所以如果n是偶数，则判断是2的几倍，然后对应的就是奇数和偶数。如果n是奇数，那么和的奇偶性是步确定的。