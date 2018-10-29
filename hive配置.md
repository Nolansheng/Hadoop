# 1.配置文件hive-site.xml
```
<configuration>
<property>

      <name>javax.jdo.option.ConnectionUserName</name>

      <value>root</value>

  </property>

  <property>

      <name>javax.jdo.option.ConnectionPassword</name>

      <value>7899</value>

  </property>

  <property>

      <name>javax.jdo.option.ConnectionURL</name>

      <value>jdbc:mysql://localhost:3306/hive</value>

  </property>

  <property>

      <name>javax.jdo.option.ConnectionDriverName</name>

      <value>com.mysql.cj.jdbc.Driver</value>

  </property>

  <property>

      <name>hive.metastore.schema.verification</name>

      <value>false</value>

  </property>

  <property>

    <name>datanucleus.schema.autoCreateAll</name>

    <value>true</value>

 </property>
 <property>
    <name>hive.metastore.warehouse.dir</name>
    <value>/user/hive/warehouse</value>
 </property>
<property>  
    <name>hive.exec.scratchdir</name>  
    <value>/user/hive/tmp</value>  
</property>  
<property>
    <name>hive.querylog.location</name>
    <value>/user/hive/log/hadoop</value>
</property>
</configuration>
```

# 2.hive-env.sh
```
HADOOP_HOME=/usr/local/hadoop
export HIVE_CONF_DIR=/usr/local/hive/conf
export HIVE_AUX_JARS_PATH=/usr/local/hive/lib
```
# 3.要把mysql的驱动类（jdbc jar文件）放到hive的lib里面！！

# 4.启动初始化
```
cd /home/hadoop/hive-2.3.0/bin
./schematool -initSchema -dbType mysql
```
# 5.[参考资料](https://segmentfault.com/a/1190000011303459)
