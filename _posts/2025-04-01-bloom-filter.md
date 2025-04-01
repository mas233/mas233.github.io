---
title: "Bloom Filter 布隆过滤器"
description: "Data Structure: Bloom Filter 数据结构——布隆过滤器"
date: 2025-04-01 16:41:00 +0800
author: mas
categories: [Data-Structure]
tags: [Bloom-Filter,Data-Structure]
math: true
---


# Bloom Filter
**Bloom Filter** is named after *Burton Howard Bloom* and invented in 1970s. It is not a basic data structure, but can be really useful in certain circumstances. When you need to check whether an element is present in your storage, but you don't have so much storage to maintain a **Hash Map**, Bloom Filter is highly competent for this job. However, high performance always comes with a cost, and Bloom Filter is no exception. Later we will talk about this **defect**. 

# 1 Definition & Implementation
A **Bloom Filter** consists of 2 parts:
- a **bit array** with size of M
- a set of $k$ **hash functions**

Each hash function will map the input $x$ to range $[0,M)$. In other words, each input is mapped to a k-dimention vector. \\
Bloom Filter only supports `put()` and `contains()`. The basic version doesn't support `remove()` operation.

## 1.1 put()
When an element needs to be put in Bloom Filter, firstly the k hash functions calculate k indices $i_1,i_2,...,i_k$. Each index is within $[0,M)$. Then in the array, the corresponding bits will be set to 1. \\
For example, we have an Bloom Filter with M=10 and k=3. We use $h_1(), h_2(), h_3()$ to denote these hash functions. In the beginning, the bit array should look like this(index: $0\rightarrow 9$):

$$
    0000000000
$$

Now an input *2* comes. Assuming $h_1(2)=3, h_2(2)=0,h_3(2)=6$, the array will then look like this: 

$$
    \color{red}{1}\color{black}{00}\color{red}{1}\color{black}{00}\color{red}{1}\color{black}{000}
$$

Now another input *6* comes. Assuming $h_1(6)=5, h_2(6)=3,h_3(6)=9$, the array will become:

$$
    \color{black}{100}\color{blue}{1}\color{black}{0}\color{red}{1}\color{black}{100}\color{red}{1}
$$

Note that data *2* and *6* both occupies the position $array[3]$ after hashed. 

## 1.2 contains()
Bloom Filter will assume the element $e$ is in the set if **all the bits at the hashed indices are 1**. \\
Let's continue with the example in **1.1**.

$$
    1001011001
$$

For example, if the input is *2*, its hashed indices are $[3,0,6]$. The bits at these indices are all **1**, so the method will return **true**.

$$
\color{red}{1}\color{black}{00}\color{red}{1}\color{black}{01}\color{red}{1}\color{black}{001}
$$
 
If another input *3* comes, and let's assume $h_1(3)=7, h_2(3)=4,h_3(3)=0$. We can see that $array[7]=0$, $array[4]=0$ and $array[3]=1$. Not all the bits are **1**, so the return value is **false**. 

$$
\color{red}{1}\color{black}{001}\color{red}{0}\color{black}{01}\color{red}{0}\color{black}{01}
$$

# 2 Complexity Analysis

## 2.1 Generation
Apparently, the array is generated at $O(M)$. Each hash function will take about $O(1)$, so the functions are generated at $O(k)$. The total generation complexity is $O(M+k)$.

## 2.2 put()
The calculation will base on these premises:
- Each bit operation will take constant amount of time $t_b$. 
- Hashing key $X$ will take $T(X)$ time. 
- The number of bits to store a key is not determined by the size of key nor the amount of elements already in the collection. 

Based on these, put() runs at $O(k\times T(\|X\|))$. And hashing is a process at $O(1)$, we can see the whole process is $O(k)$, a constant complexity. 

## 2.3 contains()
Similarly to **2.2**, this operation runs at $O(k)$ as well. 

# 3 The Defect
As shown in **1.1**, clashing indices for different input may result in **false positive**. This can be illustrated as such:
- If `contains()` returns **false**, the element is **absolutely NOT** in the collection.
- If `contains()` returns **true**, the emelemt is **highly probable** in the collection, but it is possible that it is **NOT** in the collection.

For a Bloom Filter with $M=10$ and $k=3$, we can see that after about 4 or 5 or more times of  `put()`, the whole array will be filled with **1**. Any element will be detected as *in the collection* then.

## 3.1 Precision Calculation[^1]
\# TODO
# References:
[^1]: 马塞洛·拉·罗卡（Marcello La Rocca）著; 肖鉴明译. 高级算法和数据结构. 北京: 人民邮电出版社, 2023:33.