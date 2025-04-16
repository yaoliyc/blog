---
title: Mysql实现按距离排序、范围查找
date: 2025-04-16 10:11:34
tags: [mysql,spatial4j]
categories: [mysql,spatial4j]
---

# Mysql实现按距离排序、范围查找


现在几乎所有的O2O应用中都会存在“按范围搜素、离我最近、显示距离”等等基于位置的交互，那这样的功能是怎么实现的呢？本文提供的实现方式，适用于所有数据库。

## 实现

实现过程主要分为四步：   
1. 搜索   
在数据库中搜索出接近指定范围内的商户，如：搜索出1公里范围内的。   
2. 过滤   
搜索出来的结果可能会存在超过1公里的，需要再次过滤。如果对精度没有严格要求，可以跳过。   
3. 排序   
距离由近到远排序。如果不需要，可以跳过。   
4. 分页   
如果需要2、3步，才需要对分页特殊处理。如果不需要，可以在第1步直接SQL分页。

第1步数据库完成，后3步应用程序完成。

为了方便下面说明，先给出一个初始表结构，我使用的是MySQL：

![](1218828-20171022180821084-1141286440.png)

## step1 搜索

搜索可以用下面两种方式来实现。

### 区间查找

customer表中使用两个字段存储了经度和纬度，如果提前计算出经纬度的范围，然后在这两个字段上加上索引，那搜索性能会很不错。   
那怎么计算出经纬度的范围呢？已知条件是移动设备所在的经纬度，还有满足业务要求的半径，这很像初中的一道平面几何题：给定圆心坐标和半径，求该圆外切正方形四个顶点的坐标。而我们面对的是一个球体，可以使用[spatial4j](https://github.com/locationtech/spatial4j)来计算。

![](1218828-20171022180905021-1403485682.png)

![](1218828-20171022180929615-603715276.png)

geohash的原理不讲了，详细可以看[这篇文章](http://www.cnblogs.com/LBSer/p/3310455.html)，讲的很详细。geohash算法能把二维的经纬度编码成一维的字符串，它的特点是越相近的经纬度编码后越相似，所以可以通过前缀like的方式去匹配周围的商户。   
customer表要增加一个字段，来存储每个商户的geohash编码，并且建立索引。

![](1218828-20171022180956037-674314141.png)

![](1218828-20171022181016802-1620997722.png)

 ![](1218828-20171022181042615-564048244.png)

![](1218828-20171022181202224-1107522791.png)

![](1218828-20171022181224537-190479827.png)

## step3 排序

同样，排序也需要在应用程序中处理。排序基于上面的过滤结果做就可以了`Collections.sort(list, comparator)`。

## step4 分页

如果需要2、3步，只能在内存中分页，做法也很简单，可以参考[这篇文章](http://blog.csdn.net/ghsau/article/details/7243540)。

## 总结

全文的重点都在于搜索如何实现，更好的利用数据库的索引，两种搜索方式以百万数据量为分割线，第一种适用于百万以下，第二种适用于百万以上，`未经过严格验证`。可能有人会有疑问，过滤和排序都在应用层做，内存占用会不会很严重？这是个潜在问题，但大多数情况下不会。看我们大部分的应用场景，都是单一种类POI(Point Of Interest)的搜索，如酒店、美食、KTV、电影院等等，这种数据密度是很小，1公里内的酒店，能有多少家，50家都算多的，所以最终要看具体业务数据密度。本文没有分析原理，只讲了具体实现，有关分析的文章可以看参考链接。

___

## 参考

[http://www.infoq.com/cn/articles/depth-study-of-Symfony2](http://www.infoq.com/cn/articles/depth-study-of-Symfony2)   
[http://tech.meituan.com/lucene-distance.html](http://tech.meituan.com/lucene-distance.html)   
[http://blog.csdn.net/liminlu0314/article/details/8553926](http://blog.csdn.net/liminlu0314/article/details/8553926)   
[http://janmatuschek.de/LatitudeLongitudeBoundingCoordinates](http://janmatuschek.de/LatitudeLongitudeBoundingCoordinates)   
[http://www.cnblogs.com/LBSer/p/3310455.html](http://www.cnblogs.com/LBSer/p/3310455.html)   
[http://cevin.net/geohash/](http://cevin.net/geohash/)
