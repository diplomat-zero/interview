```
// Go map的一个header结构
type hmap struct {
    count     int // map的大小.  len()函数就取的这个值
    flags     uint8 //map状态标识
    B         uint8  // 可以最多容纳 6.5 * 2 ^ B 个元素，6.5为装载因子即:map长度=6.5*2^B
                    //B可以理解为buckets已扩容的次数
    noverflow uint16 // 溢出buckets的数量
    hash0     uint32 // hash 种子
 
    buckets    unsafe.Pointer //指向最大2^B个Buckets数组的指针. count==0时为nil.
    oldbuckets unsafe.Pointer //指向扩容之前的buckets数组，并且容量是现在一半.不增长就为nil
    nevacuate  uintptr  // 搬迁进度，小于nevacuate的已经搬迁
    extra *mapextra // 可选字段，额外信息
}
 
//额外信息
 type mapextra struct {
     overflow    *[]*bmap
     oldoverflow *[]*bmap
 ​
     nextOverflow *bmap
 }
 
 //在编译期间会产生新的结构体，bucket
 type bmap struct {
     tophash [8]uint8 //存储哈希值的高8位
     data    byte[1]  //key value数据:key/key/key/.../value/value/value...
     overflow *bmap   //溢出bucket的地址
 }
```