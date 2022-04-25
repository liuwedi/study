## 2022.4.25

git token: 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

### 1）kafka面经

https://www.nowcoder.com/discuss/809261?type=post&order=recall&pos=&page=1&ncTraceId=&channel=-1&source_id=search_post_nctrack&gio_id=5481F0EDF386C227E070D0D1AE345320-1650849034119

![kafka](/home/mdPicture/kafka.png)

### 2）IO:

https://www.cnblogs.com/xiaolincoding/p/13719610.html

DMA、MMAP、零拷贝

### 3）分布式锁：redis和zookeeper

redis:

- setnx(节点挂掉，导致锁丢失;expireTime不好控制)

使用redis做分布式锁的缺点在于：如果采用单机部署模式，会存在单点问题，只要redis故障了。加锁就不行了。

采用master-slave模式，加锁的时候只对一个节点加锁，即便通过sentinel做了高可用，但是如果master节点故障了，发生主从切换，此时就会有可能出现锁丢失的问题。

- RedLock(前提：redis的部署模式是redis cluster，该模式也无法保证加锁的过程一定正确)
- Redission(内部包含watchDog)

缺点：需要不停轮询，且可能出现锁丢失的情况

zookeeper:

- 临时节点+监控

缺点：若不停申请锁、释放锁，对zk集群压力大。

个人推荐zk分布式锁。

### 4）zk相关面经

- zookeeper将数据保存在内存中，所以性能很棒
- 重点在于协调服务，不是存储数据，因此每个zNode最多存1M的数据
- ==选举leader的过程不够详细==

lwdlwd

