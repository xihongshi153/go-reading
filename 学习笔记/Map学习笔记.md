#### Go map 扩容方式

> **翻倍扩容**与**等量扩容**

***

|          | 翻倍扩容                         | 等量扩容                                                     |
| -------- | -------------------------------- | ------------------------------------------------------------ |
| 触发条件 | count/(2^B)>6.5                  | LoadFactor没超标,1.B<15且noverflow>=2^B 2.B>15且noverflow>=2^15 |
| 扩容过程 | 1.B++,buckets指向新的桶数组      |                                                              |
|          | 2.oldbuckets指向旧的桶数组       |                                                              |
|          | 3.nevacuate代表正要迁移的桶      |                                                              |
|          | 4.hash>B&1==0,1 决定迁移到哪个桶 |                                                              |

> 如何访问的 mapaccess1()与mapaccess2() 方法

```go
v     := hash[key] // => v     := *mapaccess1(maptype, hash, &key)
v, ok := hash[key] // => v, ok := mapaccess2(maptype, hash, &key)
```

