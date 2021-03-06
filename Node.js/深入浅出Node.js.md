# 深入浅出Node.js看书笔记
《深入浅出Node.js》一书作者朴灵，阿里巴巴数据平台，长期进行nodejs研究，算是国内NodeJS权威人士


## 第五章 内存控制

### V8的垃圾回收机制
因为Node的诞生跟V8有着很大关系，所以，Node的垃圾回收机制采用的是V8 引擎的回收方式。  
* V8对内存大小有着限制，64位系统下1.4G，32位系统下0.7G。加上新生代内存，严格意义上来说，64位系统堆内存位1464MB，32位系统上为732MB
* V8内存分类为新生代内存和老生代内存。
* **Scavenge**算法回收。 分成两块内存From和To，将From中存活对象移到To中，非存活对象释放，From和To会校色互换。特点是：**牺牲空间换时间**
* 对象从新生代到老生代的过程叫做晋升。条件有两个：一个是对象是否经历过Scavenge回收，二是To空间的内存占比是否超过限制（25%）。
* **Mark-Sweep**回收 ：标记过程-遍历所有对象，标记活着的；随后清除标记过程，只清除没有标记的对象（即死亡对象）。问题是没有移动，内存会出现不连续，成为碎片。
* **Mark-Compact**回收：在Mark-Sweep标记死亡后，清除整理过程将对象移动到一端，移动完成，直接清理掉边界外的内存。
* 三种清除方式都是**全停顿**。为了监听全停顿带来的影响。使用**增量标记**的方式优化
![](../assets/mark-Sweep.png)

### 高效使用内存 & 内存指标
* JS 作用域域闭包使用的问题。
* 查看进程内存占用各种方法，例如： `process.memoryUsage()`

### 内存泄露
* 原因一般为：缓存、队列消费不及时、作用域位未释放
* Node中关于解决缓存造成的内存泄漏。1、
  1. 将缓存转移到外部，减少常驻内存的对象数量，让垃圾回收更高效
  2. 进程之间科共享缓存
* 内存泄漏排查工具。 `v8-profiler` `node-heapdump` , `node-mtrace`, `dtrace`, `node-memwatch`



