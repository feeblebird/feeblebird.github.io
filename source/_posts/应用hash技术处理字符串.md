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

  * 即hash[i]是字符串的前i个字符组成的前缀的hash值，而idx(s)为字符s的一个自定义索引，例如，idx('a') = 1, idx('b') = 2,......, idx('z') = 26。
  * 例如：p = 7, mod = 91,把字符串"abc"映射为一个整数：hash[0] = idx('a')%91 = 1,字符串"a"被映射为1；hash[1] = (hash[0]\*p + idx('b'))%mod = 9,表示字符串"ab"被映射为9；hash[2] = (hash[1]\*p + idx('c'))%mod = 66,所以，字符串"abc"被映射为66。

* #### 基于字符串hash函数，可以求字符串的任何一个子串的hash值

  * hash[l..r] = ((hash[r]-hash[l-1]*p<sup>r-l+1</sup>)%mod+mod)%mod (不出现负数)

  * 如上例，对于字符串"abab"，hash[2]=(hash[1]\*p+idx(‘a’))%mod=64，表示字符串"aba"被映射为64；hash[3]=(hash[2]\*p+idx(‘b’))%mod=86，即字符串"abab"被映射为86。则hash[2..3]=( (hash[3]\-hash[1]\*p<sup>2</sup>)%mod+mod)%mod =9=hash[1]，即字符串 "abab"    的第一个"ab"子串和第二个"ab"子串所对应的hash值相同，都是9
    

* #### p 和 mod取值要合适

  * 否则可能会出现不同字符串有相同的hash值。
  * 一般p 和 mod要取`素数` ，p取一个6位到8位的较大的素数，mod取一个大素数，比如10<sup>9</sup>+7,或者10<sup>9</sup>+9。