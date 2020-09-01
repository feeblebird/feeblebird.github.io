---
title: ProblemIFullDepthMorningShow
date: 2020-08-31 17:02:02
tags: 
categories: 2019NCNARegionalContest
---

* #### 尝试用了Dijkstra，TLE了
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <queue>
using namespace std;
#define MAX 100005*2  //因为这里是无向图，添加边的时候会添加两次，注意这里，不然会RE
typedef long long ll;
struct Edge
{
    int to;
    int len;
    int next;
}E[MAX];
int head[MAX];
ll dist[MAX];
bool exi[MAX];
int siz = 0;
priority_queue<pair<int,int>,vector<pair<int,int> >,greater<pair<int,int> > >p;
void addEdge(int from,int to,int val);
void Dijkstra(int sta);
ll t[MAX/2];
int main()
{
    int n,sta;
    scanf("%d",&n);
    int from,to,val;
    for(int i = 1;i <= n;i ++)
    {
        scanf("%lld",&t[i]);
    }
    for(int i = 1;i <= n-1;i ++)
    {
        scanf("%d%d%d",&from,&to,&val);
        addEdge(from,to,val);
        addEdge(to,from,val);
    }
    ll sum = 0;
    for(sta = 1;sta <= n;sta ++)
    {
        Dijkstra(sta);
        sum = 0;
        for(int i = 1;i <= n;i ++)
        {
            if(i==sta)
            {
                continue;
            }
            sum = sum + dist[i]*(t[sta]+t[i]);
        }
        if(sta<n)
        {
            printf("%lld\n",sum);
        }
    }
    printf("%lld",sum);
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
    memset(dist,0x3f,sizeof(dist));
    for(int i = 1;i < MAX;i ++)
    {
        exi[i] = false;
    }
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
* #### 上网查后用的是二次扫描加换根法

```cpp
#include <iostream>
#include <cstdio>
using namespace std;
const int maxn=1e5+10;

struct node
{
	int next;
    int to;
    int len;
}e[maxn<<1];
int head[maxn];
int siz = 0;
int n,size[maxn],sum[maxn],dp[maxn];
int t[maxn];
inline void add_edge(int from,int to,int val){
    siz++;
    e[siz].to = to;
    e[siz].val = val;
    e[siz].next = head[from];
    head[from] = siz;
}

void dfs1(int u,int fa){
	size[u]=1;
	for(int i=head[u];i;i=e[i].nxt){
		int v=e[i].to;if(v==fa)continue;
		sum[v]=sum[u]+1;
		dfs1(v,u);
		size[u]+=size[v];
	}
	dp[1]+=sum[u];
}

void dfs2(int u,int fa){
	for(int i=head[u];i;i=e[i].nxt){
		int v=e[i].to;if(v==fa)continue;
		dp[v]=dp[u]+n-(size[v]<<1);
		dfs2(v,u);
	}
}

void solve(){
	dfs1(1,0),dfs2(1,0);
	for(int i=1;i<=n;i++)printf("%d\n",dp[i]);
}

int main(){
    scanf("%d",&n);
    for(int i = 1;i <= n;i ++)
    {
        scanf("%d",&t[i]);
    }
    for(int i = 1;i <= n-1;i ++)
    {
        scanf("%d%d",&from,&to);
        addedge(from,to,1);
        addedge(to,from,1);
    }
	solve();
	return 0;
}
```

