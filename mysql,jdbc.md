# ubuntu18和直接下载的mysql5.7不适配
- 已经下好的先卸载
- 在[mysql官网](https://dev.mysql.com/downloads/repo/apt/)下载一个(mysql-apt-config_0.8.10-1_all.deb)类似这样的文件
- [具体步骤参考](https://blog.csdn.net/weixin_37946237/article/details/81634505)

# 创建一个mysql新用户
- 1.use mysql; （非常重要一定要先切换到mysql数据库）
- 2.CREATE USER 'sky'@'localhost' IDENTIFIED BY 'password';
- 3.GRANT ALL PRIVILEGES ON *.* TO 'sky'@'localhost' WITH GRANT OPTION;
- 4.需要mysql -u xxx -p登陆

# 连接MySQL时都需要用JDBC[下载](https://dev.mysql.com/downloads/connector/j/8.0.html)
- 1.先现在deb文件，sudo dpkg -i mysql-connector-..deb
- 2.pip install mysql-connector-pytho
- 3.先知道pip文件的目录pip show xxxxx
- 4.重启pycharm
- 5.具体差异官方文档

# 现在官网没有tar文件可以解压，但是用deb文件解压之后，用
`
 sudo dpkg -c /home/nolansheng/mysql-connector-java_8.0.13-1ubuntu18.04_all.deb
`
可以找到我们需要的jar文件在哪里，然后复制到需要的地方去
## 比如/usr/local/spark/jars目录下j'd

# spark连接mysql数据库的例子
`
cd /usr/local/spark
./bin/pyspark \
--jars /usr/local/spark/jars/mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar \
--driver-class-path /usr/local/spark/jars/mysql-connector-java-5.1.40/mysql-connector-java-5.1.40-bin.jar
`
`
>>> jdbcDF = spark.read.format("jdbc").option("url", "jdbc:mysql://localhost:3306/spark").option("driver","com.mysql.jdbc.Driver").option("dbtable", "student").option("user", "root").option("password", "hadoop").load()
>>> jdbcDF.show()
`
- 但是 com.mysql.jdbc.Driver已经被弃用，改为com.mysql.cj.jdbc.Driver

## [关于deb包安装的一些方法](https://blog.csdn.net/zhaoyang22/article/details/4235596)

## python spark连接mysql
```
from pyspark import SparkContext
from pyspark.sql import SparkSession
sc=SparkContext('local','test')
spark=SparkSession(sc)
import mysql
jdbcDF = spark.read.format("jdbc").option("url", "jdbc:mysql://localhost:3306/spark").option("driver","com.mysql.cj.jdbc.Driver").option("dbtable", "student").option("user", "root").option("password", "7899").load()
jdbcDF.show()
```

