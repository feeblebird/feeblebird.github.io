---
title: Dijkstra算法
date: 2020-08-29 10:08:16
tags: 
	- Dijkstra算法
	- 单源最短路径
categories: 图论
---

* #### Dijkstra算法的使用条件

  该算法的条件是该图所有边的权值非负，而且式**无环**图。

* #### 基本做法(邻接表)

```cpp
#include <iostream>
#include <algorithm>
#include <cstring>
using namespace std;
#define MAX 100005
const int INF = 0x3f3f3f3f;
int GWeight[2000][2000];  //int二维数组不能开太大。
int path[MAX];   //记录最短路径一次经过的点
bool exi[MAX];   //记录各个点是否已经存在的状态
int dist[MAX];   //记录起点到各个点断最短距离
int n,m;
void Dijkstra(int start);
int main()
{
    memset(GWeight,0x3f,sizeof(GWeight));
    for(int i = 1;i <= MAX;i ++)
    {
        exi[i] = false;
        dist[i] = INF;
        path[i] = -1;
    }
    int start = 1;
    scanf("%d%d",&n,&m);
    int tem1,tem2;
    for(int i = 1;i <= m;i ++)
    {
        scanf("%d%d",&tem1,&tem2);
        GWeight[tem1][tem2] = 1;
        if(tem1 == start)
        {
            dist[tem2] = 1;
            path[tem2] = tem1;
        }
    }
    Dijkstra(1);
    printf("%d",dist[n]-1);
    return 0;
}
void Dijkstra(int start)
{
    dist[start] = 0;
    exi[start] = true;
    int mindis;
    int nextV;
    int oldV = start;
    while(true)
    {
        nextV = oldV;
        mindis = INF;
        for(int i = 1;i <= n;i ++)
        {
            if(!exi[i]&&dist[i]<mindis)
            {
                nextV = i;
                mindis = dist[i];
            }
        }
        if(nextV == oldV)
        {
            break;
        }
        exi[nextV] = true;
        oldV = nextV;
        for(int i = 1;i <= n;i ++)
        {
            if(!exi[i])
            {
                int tem = dist[nextV]+GWeight[nextV][i];
                if(tem<dist[i])
                {
                    dist[i] = tem;
                    path[i] = nextV;   //记录的是起点
                }
            }
        }
    }
}
```

* #### 在竞赛题中用邻接表做的话肯定会超时

* #### 堆优化(使用优先级队列，优先级队列是个堆)(有向图)
```cpp
#include <iostream>
#include <cstdio>
#include <queue>
#include <vector>
#include <algorithm>
#include <cstring>
using namespace std;
#define MAX 100005
struct Edge
{
    int to;
    int len;
    int next;
}E[MAX];
int head[MAX],dist[MAX];
bool exi[MAX];int siz = 0;
priority_queue<pair<int,int>,vector<pair<int,int> >,greater<pair<int,int> > >p; //greater<> 是小根堆
//元素基本类型是pair<int,int>对，装这些元素的容器时vector，优先级的排序方式为小根堆
//优先级队列的内部实现方式为堆
void addedge(int from,int to,int val);
void Dijkstra(int sta);
int main()
{
    memset(dist,0x3f,sizeof(dist));
    for(int i = 1;i < MAX;i ++)
    {
        exi[i] = false;
    }
    int n,m;
    int sta;
    scanf("%d%d%d",&n,&m,&sta);
    int from,to,val;
    for(int i = 1;i <= m;i ++)
    {
        scanf("%d%d%d",&from,&to,&val);
        if(from!=to)    //避免出现自环
        {
            addedge(from,to,val);
        }
    }
    Dijkstra(sta);
    printf("%d",dist[n]);
    return 0;
}
void addedge(int from,int to,int val)
{
    siz++;
    E[i].to = to;
    E[i].len = val;
    E[i].next = head[from];
    head[from] = siz;//对应着第几条边
}
//每个点作为起点时，head都是从零开始，然后记录是录入的第几条边
//如果后面还有以该点为起点的边，那么就将新的边的next记录为当前的
//边数，所以在选定一个点为起点的时候，就根据这个进行遍历，不断更新
//各个dist值。然后由优先级队列自动选出最小的值。
void Dijkstra(int sta)
{
    int A = sta;
    dist[A] = 0;
    p.push(make_pair(0,A));
    while(!p.empty())  //此时只有一个孤立的点，和别的点都不连通
    {
        int V = p.top().second;
        p.pop();
        if(exi[V]){continue;}
        exi[V] = true;
        for(int i = head[V];i>0;i = E[i].next)
        {
            if(dist[i]+E[i].len < dist[E[i].to])
            {
                dist[E[i].to] = dist[i] + E[i].len;
                p.push(make_pair(dist[E[i].to],E[i].to));
            }
        }
    }
}
```


* #### 堆优化的Dijkstra算法(这里使用优先级队列)(无向图)

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
        if(from != to) //避免出现自环
        {
            addEdge(from,to,val);
        	addEdge(to,from,val);
        }
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





