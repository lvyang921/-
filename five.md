# 哈希
---
## 哈希函数
哈希函数的性质
1. 输入域无穷str
2. 输出域有穷
3. 哈希函数固定输入 输出一定 不随机
4. 哈希函数输入不同 输出可能相同
5. 对于输入域 可通过哈希函数均匀分布在输出域上

## 哈希表
对于（key,value）先计算hash(key)令其为a，然后把该（key,value）挂在a上；查找key 则先计算hash(key)，然后找该位置的value

## 布隆过滤器
- 具有失误率（宁可错杀不放过）
- bit类型数据集合 可通过定义int占4个字节共计32bit位
- 添加布隆过滤器
    1. 首先对于str求hash然后对布隆过滤器长度取模 得到对应位置‘描黑’
    2. 准备k个hash函数 重复步骤1 对应位置描黑
- 查找布隆过滤器 
   1.对str计算k个hash函数 找到对应位置是否描黑 都是则在布隆过滤器中
   2.如有一个不为黑 则str不在其中
 - 布隆过滤器的大小与多少个hash有关，与输入str长度无关，和输入样本量有关，与失误率有关
 - 布隆过滤器的长度 m=-（n*ln(p)）/(ln2)^2,其中n为样本量，p为预期失误率
 - hash函数的个数k=ln2*m/n
- 真实失误率为（1-e^(-m*k/m)）^k

## 一致性哈希
通过虚拟节点技术优化

# 并查集
---
用代表节点实现
1. 是否两个元素在一个集合 
2. 合并两个元素所在的所有集合
3. 样本为N 当查询与合并逼近O(N) 则单次查询时间负责度为O(1)


## 岛问题 
一个矩阵中只有0和1 两种值，每个位置都可以和自己的上下左右四个位置相连，如果有一片1连在一起，这个部分叫做一个岛，求一个矩阵中有多少个岛 
如：
         [[0 0 1 0 1 0]
         [1 1 1 0  1 0]
		 [1 0 0 1 0 0]
		 [0 0 0 0 0 0]]
这个矩阵有3个岛

- 单核遍历：用感染函数实现
- 多核处理：切割 设定感染核心 查看边界 用并查集合并 