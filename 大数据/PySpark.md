
# 简介

Spark 是用于 <span style="color:red">大规模数据</span> 处理的 <span style="color:red">统一分析引擎</span>.  
其通过 **RDD**(弹性分布式数据集), 能够在大规模的集群中做内存运算.  

发展:  
2009: 起源于加州伯克利分校.  
2010: Spark开源.  
2013: Spark被捐赠给Apache基金会.  
2014: Spark成为Apache顶级项目.  
2016: Spark2.0分布, 其后逐步登上分布式计算的王座.  
2019: Spark3.0分布, 性能相比2.0有50%的提升.  

Spark 支持众多语言进行开发, java, python, scala...  
Python成为 Spark 上使用最广泛的语言.  
Spark3.2.0 支持 pandas的API.  

## Spark与Hadoop

|          |                Hadoop                 |                           Spark                            |
| -------- |:-------------------------------------:|:----------------------------------------------------------:|
| 类型     |    基础平台, 包含储存, 计算, 调度     |                         纯计算工具                         |
| 场景     |     海量数据批处理(磁盘迭代计算)      | 海量数据的批处理(内存迭代计算, 交互式计算), 海量数据流计算 |
| 价格     |          对机器要求低, 便宜           |                   对内存有要求, 相对较贵                   |
| 编程范式 | Map+Reduce, API较为底层, 算法适应性差 |        RDD组成DAG有向无环图, API较为顶层, 方便使用         |
| 数据储存结构         |                                       |                                                            |
> Spark仅做计算, 而Hadoop不仅有计算(MR), 也有储存(HDFS)和资源管理调度(YARN).  
> HDFS和YARN仍是大数据体系的核心架构.  


## Spark框架模块


- Spark Core:  
	Spark的核心, Spark核心功能均由Spark Core模块提供.  
	Spark Core以RDD为数据抽象, 提供python, java, scala, R语言的API.  

- Spark SQL:  
	基于SparkCore之上, 提供结构化数据的处理模块.  
	支持以SQL语言对数据进行处理.  

- SparkStreaming:  
	以SparkCore为基础, 提供数据的流式计算功能. 但一般以StructuredStreaming模块代替.  

- MLlib:  
	以SparkCore为基础, 进行机器学习计算, 内置了大量的机器学习库和API算法等.  

- GraphX:  
	以SparkCore为基础, 进行图计算, 提供了大量的图计算API, 方便用以分布式计算模式进行图计算.  


## Spark的运行模式


- 本地模式(单机):  
	Local模式, 以一个独立的进程, 通过其内部的多个线程来模拟整个Spark运行时的环境.  
	一般用于开发和测试.  

- Standalone模式(集群):  
	Spark中的各个角色以独立进程的形式存在, 并组成Spark集群环境.  

- Hadoop YARN模式(集群):  
	Spark中的各个角色运行在YARN的容器内部, 并组成Spark集群环境.  

- Kubernetes模式(容器集群):  
	Spark中的各个角色......  

- 云服务模式:  
	Spark中的各个角色......  


## Spark的架构角色


- Master:  
	集群的资源管理者.  

- Worker:  
	单机资源的管理者.  

- Driver:  
	单个任务的管理者. 单机模式下, 也是任务的执行者.  

- Executor:  
	单个任务的执行者.  


# 单机模式


%% - 三台Linux虚拟机:  
	1. node1: Master(DHFS/YARN/Spark) 和 Worker(HDFS/YARN/Spark).  
	2. node2: Worker(HDFS/YARN/Spark).  
	3. node3: Worker(HDFS/YARN/Spark) 和 Hive.   %%


- Local模式:  
	启动JVM Process进程, 执行任务Task.  
	local\[N]: N代表线程的数量, 不指定则为1, 指定为"\*"表示CPU最大核心数.  


Local下的角色分布:  
- 资源管理:  
	- Master: Local进程本身.  
	- Worker: Local进程本身.  
- 任务执行:  
	- Driver: Local进程本身.  
	- Executor: 不存在, 计算由Driver的线程完成.  














