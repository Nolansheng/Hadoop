## pycharm 运行spark程序是，每次新建的文件需要重新添加Environment variables
或者在程序之前加上
```
import os
os.environ["SPARK_HOME"]="/usr/local/spark"
os.environ["PYSPARK_PYTHON"]="/usr/bin/python3"
```

## [Spark常用函数介绍](https://www.cnblogs.com/yxpblog/p/5269314.html)

## 配置pycharm时提示错误 ModuleNotFoundError: No module named 'distutils.core'
sudo apt-get install python-pip

## 启动spark时，提示JAVA_HOME NOT SET,在sbin中的文件spark-config.sh中加入export JAVA_HOME
