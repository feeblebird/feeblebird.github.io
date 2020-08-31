---
title: ProblemFWeight
date: 2020-08-28 10:51:52
tags:
categories: 2019NCNARegionalContest
---

(点这里)[https://ncna19.kattis.com/problems/pullingtheirweight]

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;
#define N 100005
typedef long long ll;
int wei[N];
ll sum[N];

int main()
{
    int n;
    scanf("%d",&n);
    for(int i = 1;i <= n;i ++)
    {
        scanf("%d",&wei[i]);
    }
    sort(wei+1,wei+n+1,less<int>()); //按照升序排列
    for(int i = 1;i <= n;i ++)
    {
        sum[i] = wei[i] + sum[i-1];
    }
    //int lef = wei[1];
    int lef = 1;
    //int rig = wei[n];
    int rig = 20000;
    int mid;
    int tem1,tem2;
    ll wei1,wei2;
    while(lef <= rig)
    {
        mid = (lef+rig)>>1;
        tem1 = lower_bound(wei+1,wei+n+1,mid)-wei; //第一个大于等于mid的数组元素的下标，确保减一后的一定是小于mid的。
        tem2 = upper_bound(wei+1,wei+n+1,mid)-wei; //第一个大于mid的数组元素
        wei1 = sum[tem1-1] - sum[0];
        wei2 = sum[n] - sum[tem2-1];
        if(wei1==wei2)
        {
            if(mid == wei[tem1])  //如果mid为数组中的一个数，那么输出这个
            {
                printf("%d",mid);
            }else       //如果mid不是，那么取满足条件的最小值即小于mid的数组中的那个数字加一。
            {
                printf("%d",wei[tem1-1]+1);
            }
            break;
        }else
        {
            if(wei1<wei2)
            {
                lef = mid+1;
            }else
            {
                rig = mid;
            }
        }
    }
    return 0;
}

```

