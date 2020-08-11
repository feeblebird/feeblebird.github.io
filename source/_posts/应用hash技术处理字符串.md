---
title: 应用hash技术处理字符串
date: 2020-08-08 10:06:13
tags:
	- hash技术处理字符串
	- STLmap
categories: 字符串处理
---
# 字符串的hash技术

* #### 定义：

  字符串的hash是通过某种字符串hash函数将不同的字符串映射到不同的数字，配合其他数据结构或STL，进行判重，统计，查询等操作。

* #### 一个常用的字符串hash函数

  * hash[i] = (hash[i-1]\*p + idx(s[i]))%mod

    hash[0] = idx(s[0])%mod

  * 即hash[i]是字符串的前i个字符组成的前缀的hash值，而idx(s)为字符s的一个自定义索引，例如，idx('a') = 1, idx('b') = 2,......, idx('z') = 26。

  * 例如：p = 7, mod = 91,把字符串"abc"映射为一个整数：hash[0] = idx('a')%91 = 1,字符串"a"被映射为1；hash[1] = (hash[0]\*p + idx('b'))%mod = 9,表示字符串"ab"被映射为9；hash[2] = (hash[1]\*p + idx('c'))%mod = 66,所以，字符串"abc"被映射为66。

* #### 基于字符串hash函数，可以求字符串的任何一个子串的hash值

  * hash[l..r] = ((hash[r]-hash[l-1]*p<sup>r-l+1</sup>)%mod+mod)%mod (不出现负数)

  * 如上例，对于字符串"abab"，hash[2]=(hash[1]\*p+idx(‘a’))%mod=64，表示字符串"aba"被映射为64；hash[3]=(hash[2]\*p+idx(‘b’))%mod=86，即字符串"abab"被映射为86。则hash[2..3]=( (hash[3]\-hash[1]\*p<sup>2</sup>)%mod+mod)%mod =9=hash[1]，即字符串 "abab"    的第一个"ab"子串和第二个"ab"子串所对应的hash值相同，都是9
    

* #### p 和 mod取值要合适

  * 否则可能会出现不同字符串有相同的hash值。
  * 一般p 和 mod要取`素数` ，p取一个**6位到8位**的较大的**素数**，mod取一个**大素数**，比如10<sup>9</sup>+7,或者10<sup>9</sup>+9。

# Power Strings(POJ 2406)

* #### 题目

  给出两个字符串a和b，定义a\*b是它们的串联。例如，如果a="abc"，b="def"，则a\*b="abcdef

  "。如果把串联视为相乘，非负整数指数则定义为：a^0=""（空串），而a^(n+1)=a\*(a^n)。

* #### 输入

  每个测试用例是在一行中给出一个可打印字符的字符串*s*。*s*的长度将至少为1，并且不会超过1000000（一百万）个字符。在最后 一个测试用例后面，给出包含句点的一行。

* #### 输出

  对于每个s，请输出最大的n，使得对某个字符串a，s = a ^ n。

* #### 提示

  本题海量输入，为避免超时，请使用scanf代替cin。

* #### 分析

  ![分析](https://i.loli.net/2020/08/09/Empeq6iORC9FXND.png)

* #### 代码

我的下标是从零开始的。

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;
#define N 1000005
typedef long long ll;
ll has[N];
char str[N];
int idx[N];
int p = 1000007;
int mod = 1000000007;
int lenstr;
void hashstr(char* str);
int judge();
ll pow(int p,int r)
{
    ll ans = p;
    for(int i = 1;i < r;i ++)
    {
        ans *= p;
        ans = ans % mod;    //注意取模防止爆掉
    }
    return ans;
}
int main()
{
    for(int i = 0;i < 26;i ++)
    {
        idx[i] = i+1;
    }
    while(true)
    {
        scanf("%s",str);
        if(!strcmp(str,"."))
        {
            break;
        }
        lenstr = strlen(str);
        hashstr(str);
        int ans = judge();
        printf("%d\n",ans);
    }
    return 0;
}
void hashstr(char* str)
{
    has[0] = idx[str[0]-97];
    for(int i = 1;i < lenstr;i ++)
    {
        has[i] = (has[i-1]*p+idx[str[i]-97])%mod;
    }
}
int judge()
{
    ll has1;
    for(int i = 1;i <= lenstr;i ++)
    {
        bool flag = true;
        if(lenstr%i==0)
        {
            int k = lenstr/i;
            has1 = has[i-1];
            for(int j = 2;j <= k;j ++)
            {
                ll temp = ((has[j*i-1]-has[(j-1)*i-1]*pow(p,i))%mod+mod)%mod; //注意这里n次方要自己写个函数，不要^，这个是异或。。。。
                if(temp != has1)
                {
                    flag = false;
                    break;
                }
            }
            if(flag)
            {
                return lenstr/i;
            }
        }
    }
}

```

# Stammering Aliens(HDOJ 4080)

* #### 题目

  * Ellie Arroway博士与一个外星文明建立了联系。然而，所有破解外星人讯息的努力都失败了，因为他们遇上了一群口吃的外星人。Ellie的团队发现，在每一条足够长的讯息中，最重要的单词都会以连续字符的顺序出现一定次数的重复，甚至出现在其他单词的中间；而且，有时讯息会以一种模糊的方式缩写；例如，如果外星人要说bab两次，他们可能会发送讯息babab，该讯息已被缩写，在第一个单词中第二个b被重用为第二个单词中的第一个b

  * 因此，一条讯息可能包含重复的相同单词一遍又一遍。现在，Ellie向您，S.R.Hadden，寻求帮助，以确定一条讯息的要点。
  * 给出一个整数*m*和一个表示讯息的字符串*s*，请您查找至少出现*m*次的*s*的最长子字符串。例如，在讯息baaaababababbababbab中，长度为5个单词的babab包含3次，即在位置5、7和12处（其中下标索引从零开始），出现3次或更多次的子字符串不会比5更长（请参见样例输入中的第1个样例）；而且，在这条讯息中，没有子串出现11次或更多次（请参见第2个样例）。如果存在多个解决方案，则首选出现最右的子字符串（请参见第3个样例）。
  
* #### 输入

  输入包含若干测试用例。每个测试用例在第一行给出一个整数*m*（*m*$\geq$1），表示最小重复次数；接下来的一行给出一个长度介于*m*和40000之间（包括*m*和40000）的字符串*s*。在*s*中，所有字符都是从“a”到“z”的小写字符。最后一个测试用例由*m*=0标识，程序不用处理。

* #### 输出

  对每个测试用例输出一行。如果无解，则输出none；否则，在一行中输出两个用空格分隔的整数，第一个整数表示至少出现*m*次的子串的最大长度；第二个整数表示此子字符串的最右起始位置。

* #### 分析

  

* #### 代码

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <map>
using namespace std;
#define N 40005
typedef unsigned long long ll;
ll has[N];   //下标从1开始
char str[N];
ll mi[N];
ll p = 131;               //这道题没有用mod，p取的值也很小。
map<ll,int> mapint;
int lenstr;
int m;
bool check(int mid);
int confir(int mid);
int main()
{
    mi[0] = 1;
    for(int i = 1;i <= 40000;i ++)
    {
        mi[i] = mi[i-1]*p;
    }
    while(true)
    {
        scanf("%d",&m);
        if(m==0)
        {
            break;
        }
        scanf("%s",str);
        lenstr = strlen(str);
        for(int i = 1;i <= lenstr;i ++)
        {
            has[i] = has[i-1]*p+str[i-1]-97+1;
        }
        int lef = 1,rig = lenstr;
        int mid;
        int fir;
        while(lef <= rig)
        {
            mapint.clear();
            mid = (lef + rig)>>1;
            if(check(mid))
            {
                lef = mid + 1;
            }else
            {
                rig = mid - 1;
            }
        }
        if(rig==0)
        {
            printf("none\n");
        }else
        {
            fir = confir(rig);
            if(fir==-1)
            {
                printf("none\n");
            }else
            {
                printf("%d %d\n",rig,fir);
            }
        }
    }
    return 0;
}
bool check(int mid)
{
    mapint.clear();
    for(int i = 0;i <= lenstr - mid;i ++)
    {
        int tem = has[i+mid] - has[i]*mi[mid];
        if(++mapint[tem]>=m)
        {
            return true;
        }
    }
    return false;
}
int confir(int mid)
{
    mapint.clear();
    int ans = -1;
    for(int i = 0;i <= lenstr - mid;i ++)
    {
        int tem = has[i+mid] - has[i]*mi[mid];
        if(++mapint[tem]>=m)
        {
            ans = i;
        }
    }
    return ans;
}
```

# 从上题TLE中学到的东西

* ```cpp
  for(int i = 0;i <= lenstr - mid;i ++)
  {
      tem = has[i+mid] - has[i]*mi[mid];
      mapint[tem]++;
      if(mapint[tem]>=m)
      {
          ans = i;
      }
  }
  ```
  > 这里注意那个mapint[tem]++; 应该合并到if语句中，改后代码如下。
  
  ```cpp
  for(int i = 0;i <= lenstr - mid;i ++)
  {
      tem = has[i+mid] - has[i]*mi[mid];
      if(++mapint[tem]>=m)
      {
          ans = i;
      }
  }
  ```
  
* 我之前学习的字符串的hash技术中，用到了p和mod，p和mod都推荐使用较大的素数，p推荐使用6位到8位的素数，mod推荐10<sup>9</sup>+7等等。

  但是这道题中如果用了这个以及那个取模的公式，就会超时。

* 除以二等等的运算可以用位运算，能快一点。

# STLmap的简单用法

* #include \<map\>

* map是模板类，需要关键字和存储对象两个模板参数：std:map\<int ,string\> personnel;

  这样就定义了又给用int作为索引，并拥有相关联的指向string的指针。

* 数据的插入：

  * mapStudent.insert(pair<int,string>(1,"studeng_one"));

  * mapStudent.insert(map<int,string>::value_type(2,"student_two"));

  * mapStudent[3] = "student_three";

* 通过size()成员函数得到map的大小

* 通过find()成员函数查找元素，找到则返回元素的所在位置的**迭代器**，找不到则返回**迭代器**end()。

  ```cpp
  map<int,string>::iterator iter;
  iter = mapStudent.find(1);
  if(iter!=mapStudent.end())
  {
      cout<<"Find it, the value is "<<iter->second<<endl;
  }else
  {
      cout<<"Not find"<<endl;
  }
  ```

* 用迭代器遍历

  ```cpp
  map<int,string>::iterator iter;
  for(iter = mapStudent.first();iter < mapStudent.end();iter ++)
  {
      cout<<iter->first<<' '<<iter->second<<endl;
  }
  ```

* 删除元素

  * mapStudent.erase(iter);  //指向要删除元素的迭代器作为参数
  * mapStudent.erase(key); //用要删除元素的键值作为参数

* 删除区间元素

  * mapStudent.erase(mapStudent.begin(),mapStudent.end());//把整个区间删除

    注意删除区间是**前闭后开**

# String(HDOJ 4821)

* #### 题目描述

  * 给定一个字符串S和两个整数L和M，我们称S是一个子串是"可恢复的"，当且仅当

  * (i)子串的长度位M*L;

  * (ii)这一子串通过串联S的M个"多样化"子串来构造:其中每个子串的长度L；而且这些子串不能又两个完全一样的串。
  * 如果S的两个子串是从S的不同部分切下来的，则它们被认为是“不同的”。例如，字符串"aa"有3个不同的子串"aa","a"和"a"。
  * 请您计算S的不同的”可恢复”子字符串的数量。
  
* #### 输入

  * 输入包含多个测试用例，以EOF结束

  * 每个测试用例的第一行给出两个用空格分隔的整数M和L

  * 每个测试用例的第二行给出一个字符串S,它只包含小写字母

  * S的长度不大于10<sup>^</sup>5,而且1 $\leq$ M*L $\leq$ S的长度

* #### 输出

  对每个测试用例，在一行中输出答案。
  
* #### 分析

  通过字符串的hash，求出任意一个长度为*L*的子串的hash值。枚举字符串起始位置，从0枚举到*L*\-1。然后，在这个位置开始，每*L*个字符作为一块，首先将前*M*块插入到*map*中，同时记录不相同字符串的个数，如果不相同字符串的个数是*M*，则满足要求。然后，**将这个区间向右移**，删掉第1块，加入第*M*+1块，同样记录不相同字符串的个数。

* #### 注意的点

  unsigned long long会自动取模，所以可以不用mod这个变量了。

* #### 代码

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <map>
using namespace std;
#define N 100005
typedef unsigned long long ll;   //unsigned long long会自动取模
ll p = 31;
char str[N];
ll has[N]; //下标从1开始
ll mi[N];
int m,l;
int ans = 0;
int main()
{
    mi[0] = 1;
    for(int i = 1;i <= N;i ++)
    {
        mi[i] =  mi[i-1]* p;
    }
    while(scanf("%d%d",&m,&l)!=EOF)
    {
        scanf("%s",str);
        ans = 0;
        int lenstr = strlen(str);
        for(int i = 1;i <= lenstr;i ++)
        {
            has[i] = has[i-1]*p+str[i-1]-97+1;
        }
        for(int i = 0;i <= l-1;i ++)
        {
            map<ll,int> mapint;
            int lenstr2 = strlen(str+i);
            int tem = lenstr2 / l;
            ll k;
            for(int j = 1;j <= m;j ++)
            {
                k = has[i+j*l]-has[i+(j-1)*l]*mi[l];
                mapint[k]++;
            }
            int siz = mapint.size();
            if(siz==m)
            {
                ans++;
            }
            for(int j = 1;j <= tem - m;j++)
            {
                k = has[i+j*l]-has[i+(j-1)*l]*mi[l];
                mapint[k]--;
                if(mapint[k]==0){mapint.erase(k);}
                k = has[i+(m+j)*l]-has[i+(m+j-1)*l]*mi[l];
                mapint[k]++;
                int siz = mapint.size();
                if(siz==m)
                {
                    ans++;
                }
            }
        }
        printf("%d\n",ans);
    }
    return 0;
}
```
# 通过上面这道题学到的东西

* #### unsigned long long 会自动取模

* #### 这也就是为什么上上题不用mod也能保证做对