---
title: ProblemHColor
date: 2020-08-28 19:53:52
tags: Dijkstra算法
categories: 2019NCNARegionalContest
---

[点这里](https://ncna19.kattis.com/problems/onaveragetheyrepurple)

* #### 这道是Dijkstra算法无向图的模板题，答案即为1到N的最短路径长度减1

* #### 使用堆优化的Dijkstra算法

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <queue>
using namespace std;
#define MAX 100005*2  //因为这里是无向图，添加边的时候会添加两次，注意这里，不然会RE
struct Edge
{
    int to;
    int len;
    int next;
}E[MAX];
int dist[MAX],head[MAX];
bool exi[MAX];
int siz = 0;
priority_queue<pair<int,int>,vector<pair<int,int> >,greater<pair<int,int> > >p;
void addEdge(int from,int to,int val);
void Dijkstra(int sta);
int main()
{
    memset(dist,0x3f,sizeof(dist));
    for(int i = 1;i < MAX;i ++)
    {
        exi[i] = false;
    }
    int n,m,sta;
    scanf("%d%d",&n,&m);
    sta = 1;
    int from,to,val;
    for(int i = 1;i <=m;i ++)
    {
        scanf("%d%d",&from,&to);
        val = 1;
        addEdge(from,to,val);
        addEdge(to,from,val);
    }
    Dijkstra(sta);
    printf("%d",dist[n]-1);
    return 0;
}
void addEdge(int from,int to,int val)
{
    siz++;//计数，记录是第几条边
    E[siz].to = to;
    E[siz].len = val;
    E[siz].next = head[from];
    head[from] = siz;    //以from为起点的边形成了一个链表，在Dijkstra函数里面遍历时就是根据这个链表进行遍历的。
}
void Dijkstra(int sta)
{
    int A = sta;
    dist[A] = 0; //注意别忘了这一句
    p.push(make_pair(0,A));
    while(!p.empty())
    {
        int V = p.top().second; //取出现在权值最小的边的点
        p.pop();
        if(exi[V]){continue;}
        exi[V] = true;
        for(int i = head[V];i > 0;i = E[i].next)
        {
            if(dist[V]+E[i].len<dist[E[i].to])
            {
                dist[E[i].to] = dist[V] + E[i].len;
                p.push(make_pair(dist[E[i].to],E[i].to));
            }
        }
    }
}
```

