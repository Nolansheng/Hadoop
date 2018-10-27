
# [zookeeper配置](https://blog.csdn.net/molaifeng/article/details/52945095)


## [zookeeper出错](https://stackoverflow.com/questions/30940981/zookeeper-error-cannot-open-channel-to-x-at-election-address)

### 报错1：2018-10-15 18:38:38,364 [myid:1] - ERROR [main:QuorumPeerMain@89] - Unexpected exception, exiting abnormallyjava.net.BindException: 地址已在使用
### netstat -nltp | grep 2181找到这个端口的的进程，然后Kill -9 x

### 报错2：2018-10-15 18:51:05,786 [myid:1] - WARN  [WorkerSender[myid=1]:QuorumCnxManager@588] - Cannot open channel to 6 at election address servere/10.66.101.212:3888  java.net.ConnectException: 拒绝连接 (Connection refused)
### 把每个配置文件中自己的端口改为0.0.0.0

# [Hbase的配置](https://www.polarxiong.com/archives/%E5%AE%89%E8%A3%85HBase-1-1-5%E4%BC%AA%E5%88%86%E5%B8%83%E6%A8%A1%E5%BC%8F%E5%88%B0Ubuntu-16-04%E6%95%99%E7%A8%8B.html)

## 可能遇到的问题
### 1.HMaster不能产生
将Lib文件夹中的Hadoop-*.jar删除，将hadoop中的导入，可能是因为版本不符合

### 2.[Hbase shell 命令](https://www.cnblogs.com/cxzdy/p/5583239.html)
- 切换到Hbase目录./bin/hbase shell 进入shell
- list显示有哪些表（与MySQL不同的是，Hbase不需要先建数据库）
