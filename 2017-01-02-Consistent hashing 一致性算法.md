---
layout : post
title: Consistent hashing 一致性算法
date: 2017-01-02 12:03:17
tags: redis
categories: Consistent hashing ,一致性算法,Redis
---

## Consistent hashing


### what is libconhash
libconhash is a consistent hashing library :
with high performance and easy to use,libconhash uses a red-black tree to manage all nodes to achieve high performance.
Easy to scale according to the node's processing capacity.
import imprt imort :Easy to scale according to the node's processing capacity.
#### why we need consistent hashing 
e.g. we have n machines and object O need to cache. 
will be :
```
hash(o)  mod n
```

now we must need to add a machine or remove a machine, 
```
hash(o)  mod (n+1)
```
```
hash(o)  mod (n-1)
```
if by this way , almost all object will hash into a new location.
So this is why you need consistent hashing  . Consistent can guarantee that when a machine added or removed,only a few object will be rehashed or only the object cached in it will be rehashed.
### Hash space

通常Hash算法都是将value映射在一个32位的key值当中。
假设有一个环形hash空间，空间的大小是0～2^32-1。
