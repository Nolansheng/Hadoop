# 10.10 使用hadoop2.8完成了集群配置
## 1.暂时只用三台机器master,serverb,serverc
配置步骤与之前相同

### 重点是  
### 1.一定要能相互无需密码SSH  

### 2. 将jdk,hadoop路径添加到系统变量

### 3.最困难的是hadoop的配置文件，目前网上基本都是hadoop2的教程内容，原计划使用最新的hadoop3.1.1遇到无数的坑，在开始使用wordcount的时候终于无解放弃，暂时先用Hadoop2.8  

### 4.配置文件参考
[林子雨大数据技术原理与应用](http://dblab.xmu.edu.cn/post/5663/)  

[Hadoop 集群安装配置教程](http://dblab.xmu.edu.cn/blog/install-hadoop-cluster/)

[Ubuntu18.04 配置 Hadoop 3.1.0 分布式集群](https://blog.mahonex.com/index.php/2018/06/22/ubuntu18-04-%E9%85%8D%E7%BD%AE-hadoop-3-1-0-%E5%88%86%E5%B8%83%E5%BC%8F%E9%9B%86%E7%BE%A4/)

[Hadoop3.1.1完全分布式集群部署流程](https://blog.csdn.net/qq_39151089/article/details/82708946)

### 5.目前已掌握的是熟练装系统，装Hadoop，JDK，还有Linux的一般命令



## 今日重点
### 1.hdfs dfs -mkdir -p /user/hadoop 该命令用于创建用户目录（hdfs就是一种文件系统，命令也与LINUX系统类似，但是生成的文件在系统中看不到，WEB端可以查看

### 2.hdfs dfs -mkdir input
### hdfs dfs -put /usr/local/hadoop/etc/hadoop/*.xml input 
### /usr/local/hadoop/etc/hadoop 中的配置文件作为输入文件复制到分布式文件系统中

### 3.hadoop jar /usr/local/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar grep /user/hadoop/input output 'dfs[a-z.]+' 使用Mapreduce作业（自带的例子Wordcount)

### 4.在/user/hadoop目录下会生成output文件夹，使用命令hdfs dfs -cat /user/nolansheng/output/part-r-00000可查看内容

### 5.已掌握HDFS常用命令的fs 熟悉了HDFS的web界面

### 6.新开启了一个 Jobhistoryserver
### 在mapred-site.xml 加入
```
        <property>
                <name>mapreduce.framework.name</name>
                <value>yarn</value>
        </property>
        <property>
                <name>mapreduce.jobhistory.address</name>
                <value>Master:10020</value>
        </property>
        <property>
                <name>mapreduce.jobhistory.webapp.address</name>
                <value>Master:19888</value>
        </property>
```
### 该命令mr-jobhistory-daemon.sh start historyserver开启

### 7.Wordcount应该是一个java程序，通过这个程序统计上传的文件中的单词个数

