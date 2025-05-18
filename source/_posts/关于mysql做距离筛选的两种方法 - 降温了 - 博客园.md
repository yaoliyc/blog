---
title: 关于mysql做距离筛选的两种方法
date: 2025-04-15 16:16:15
tags: [java,redis,实用操作]
categories: [java,redis,实用操作]
---

# 关于mysql做距离筛选的两种方法 - 降温了 - 博客园

## 使用mysql自带的函数计算距离作为筛选条件

- 这种方式是网上比较常见的，缺点很明显，不能使用索引，查询非常的慢，几万条数据量查询都慢的要死

```sql
/**
*  @param :lat 纬度
*  @param :lon 经度
*  @param :dis 距离范围
**/
SELECT a.*,ROUND(6378.138 * 2 * ASIN(SQRT(POW(SIN((:lat * PI() / 180 - a.latitude * PI() / 180) / 2), 2) + COS(:lat * PI() / 180) * COS(a.latitude * PI() / 180) * POW(SIN((:lon * PI() / 180 - a.longitude * PI() / 180) / 2), 2))) * 1000) AS distance FROM maoyan_cinema a WHERE a.del_flag = 0 HAVING distance < :dis ORDER BY distance ASC


```

## 使用redis计算距离

- 先将数据库里的数据全部导入到redis（经纬度和主键）即可

```java
//导入到redis部分代码
public void syncGeo() {
        //查询经度纬度主键id保存在list
        List<Object[]> list = xxx.getStationPoint();
        if (CollectionUtils.isEmpty(list) || list.size() < 1) {
            return;
        }
        Map<Long, Point> map = new HashMap<>(hashMapInitialCapacity);
        for (Object[] o : list) {
            map.put(Long.parseLong(o[0].toString()), new Point(Double.parseDouble(o[2].toString()), Double.parseDouble(o[1].toString())));
        }
        GeoOperations geoOperations = redisTemplate.opsForGeo();
        Long stations = geoOperations.geoAdd("redisKeyGeo", map);
        redisTemplate.expire("redisKeyGeo", 2, TimeUnit.DAYS);
    }

```

- 保存完后在redis可视化工具可以看到  
    ![](2169095-20220325154323367-42656464.png)

- 也可以使用命令行查看其中的某条记录  
    ![](2169095-20220325151107218-966233511.png)

- geo计算满足距离范围内主键id列表

```java
           Circle circle = new Circle(new Point("入参经度", "入参纬度"), new Distance("距离范围", Metrics.KILOMETERS));
            //这里限制1w条，可根据实际业务确定需要多少条数据
            RedisGeoCommands.GeoRadiusCommandArgs args = RedisGeoCommands.GeoRadiusCommandArgs.newGeoRadiusArgs().includeDistance().sortAscending().limit(10000);
            GeoResults<RedisGeoCommands.GeoLocation<Integer>> results = geoOperations.geoRadius("redisKeyGeo", circle, args);
            Map<Long, Double> stationIdsAndDistance = new LinkedHashMap<>();
            List<GeoResult<RedisGeoCommands.GeoLocation<Integer>>> content = results.getContent();

```

- 得到范围内的所有主键id,再使用mysql进行各种条件筛选。这种方式可以用到索引，测试geo计算距离也很快，只需要几毫秒
