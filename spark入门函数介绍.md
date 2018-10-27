## 1.reduceByKey(func)
reduceByKey(func)的功能是，使用func函数合并具有相同键的值

## 2.groupByKey()
groupByKey()的功能是，对具有相同键的值进行分组。比如，对四个键值对(“spark”,1)、(“spark”,2)、(“hadoop”,3)和(“hadoop”,5)，采用groupByKey()后得到的结果是：(“spark”,(1,2))和(“hadoop”,(3,5))

## 3.keys()
keys()只会把键值对RDD中的key返回形成一个新的RDD

## 4.valuse()
values()只会把键值对RDD中的value返回形成一个新的RDD

## 5.sortByKey()
sortByKey()的功能是返回一个根据键排序的RDD

## 6.mapValues(func)
对键值对RDD中的每个value都应用一个函数，但是，key不会发生变化

## 7.join
pairRDD1是一个键值对集合{(“spark”,1)、(“spark”,2)、(“hadoop”,3)和(“hadoop”,5)}，pairRDD2是一个键值对集合{(“spark”,”fast”)}，那么，pairRDD1.join(pairRDD2)的结果就是一个新的RDD，这个新的RDD是键值对集合{(“spark”,1,”fast”),(“spark”,2,”fast”)}

## 8.[textFile](https://blog.csdn.net/legotime/article/details/51871724)

## [spark之DataFrame](http://dblab.xmu.edu.cn/blog/1719-2/) 类似于将数据变为数据库形式，可以跟SQL一样操作
