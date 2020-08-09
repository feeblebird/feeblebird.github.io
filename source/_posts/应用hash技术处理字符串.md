---
title: 应用hash技术处理字符串
date: 2020-08-08 10:06:13
tags:
	- hash技术处理字符串
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

  Ellie Arroway博士与一个外星文明建立了联系。然而，所有破解外星人讯息的努力都失败了，因为他们遇上了一群口吃的外星人。Ellie的团队发现，在每一条足够长的讯息中，最重要的单词都会以连续字符的顺序出现一定次数的重复，甚至出现在其他单词的中间；而且，有时讯息会以一种模糊的方式缩写；例如，如果外星人要说bab两次，他们可能会发送讯息babab，该讯息已被缩写，在第一个单词中第二个b被重用为第二个单词中的第一个b