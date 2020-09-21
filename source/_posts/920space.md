---
title: 920space
date: 2020-09-20 15:02:26
tags: ccpc
categories: ccpc
---

# P1007

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
char str[100005];
int cou[27];
int main()
{
    int t;
    scanf("%d",&t);
    int ma = 0;
    for(int i = 1;i <= t;i ++)
    {
        ma = 0;
        memset(cou,0,sizeof(cou));
        scanf("%s",str);
        int lenstr = strlen(str);
        for(int j = 0;j < lenstr;j ++)
        {
            cou[str[j]-96]++;
            ma = max(ma,cou[str[j]-96]);
        }
        printf("Case #%d: %d\n",i,ma);
    }

    return 0;
}
```

# P1003

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cmath>
using namespace std;
#define M 1000006
typedef long long ll;
int mail[M];

int main()
{
    int t;
    scanf("%d",&t);
    int n,m,k;
    for(int i = 1;i <= t;i ++)
    {
        scanf("%d%d%d",&n,&m,&k);
        for(int j = 1;j <= m;j ++)
        {
            scanf("%d",&mail[j]);
        }
        sort(mail+1,mail+1+m);
        ll ans = 0;
        ans += abs(k-1);
        for(int j = m;j >= 1;j --)
        {
            ans += abs(mail[j]-k);
            if(j==1 && mail[j]<k)
            {
                ans += (mail[j]-1);
            }else
            {
                ans += abs(mail[j] - k);
                if(j==1)
                {
                    ans += k -1;
                }
            }
        }
        printf("%lld\n",ans);
    }
    return 0;
}
```

