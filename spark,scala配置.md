# [Spark的配置](http://dblab.xmu.edu.cn/blog/1689-2/)
# [scala的安装配置](http://www.runoob.com/scala/scala-install.html)
## 入坑提示！！！
## Spark好像还不适配更高的JDK版本，所以我把JDK降到了8
## ~/.bashrc的配置
```
export  JAVA_HOME=/usr/lib/jvm/jdk-10.0.2
export  JRE_HOME=${JAVA_HOME}/jre
export  CLASSPATH=.:{JAVA_HOME}/lib:${JRE_HOME}/lib
export  PATH=${JAVA_HOME}/bin:$PATH

export  HADOOP_HOME=/usr/local/hadoop
export  PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

export SPARK_HOME=/usr/local/spark
export PATH=$SPARK_HOME/bin:$PATH

export SCALA_HOME=/usr/lib/scala/scala-2.12.7
export PATH=$SCALA_HOME/bin:$PATH

export PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.7-src.zip:$PYTHONPATH
export PYSPARK_PYTHON=python3
export PYSPARK_DRIVER_PYTHON=python3
export PATH=$HADOOP_HOME/bin:$SPARK_HOME/bin:$PATH
```
![运行例子](http://stxzyq.cn/img/sparkwdc.png)


- 测试1 直接输入命令pyspark,和 spark-shell，看看能否进入spark
- 测试2 查看localhost:8080 Alive Workers的数量
- 测试3 [spark下使用python写wordcount](https://blog.csdn.net/levy_cui/article/details/53216424)


## 遇到的错误1 在运行python程序是提示有python2.7 和3.6 不能用是运行，
解决方法 在pycharm中找到 'Edit Configurations...' 
在'Enviroment variables:'中添加PYTHONPATH,PYSPARK_PYTHON,PYSPARK_DRIVER_PYTHON,value与配置文件相同

## 遇到错误2 不能连接到HDFS文件
解决方法，使用端口9000

## [关于在Ubuntu18上安装mysql](https://blog.csdn.net/Iversonx/article/details/80341596)
直接用命令行下载的mysql5.5不适配ubuntu18,网上的教程都是说安装过程会要求输入密码，但是用ubuntu18没有
另外在mysql中经常遇到一些问题以后再专门写

