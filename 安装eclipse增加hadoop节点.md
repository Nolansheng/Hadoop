# 在ubuntu安装eclipses
1. jdk已经安装完成

2. 在Eclipse官网下载最新的[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/oxygen/3a/eclipse-jee-oxygen-3a-win32-x86_64.zip)(ps:这是最新的64位oxygen)

3. 解压到合适的文件夹
sudo tar -zxvf /eclipse压缩包位置 /usr


4.创建eclipse桌面快捷图标
cd /usr/share/applications

sudo vi eclipse.desktop
```
[Desktop Entry]
Encoding=UTF-8
Name=Eclipse
Comment=Eclipse
Exec=/usr/local/eclipse/eclipse(安装的位置）
Icon=/usr/local/eclipse/icon.xpm（安装的图标位置）
Terminal=false
StartupNotify=true
Type=Application
Categories=Application;Development;
```

5. 最重要的一点。。现在还会报错打不开，因为还没有指定JRE的位置
cd 到eclipse目录

mkdir jre

cd jre

sudo ln -s /你的jdk目录/bin

或者在eclipse.ini文件的第一行加上 -vm /usr/jav/jdk/bni


6. 点下左下角显示应用，把Eclipse加到收藏夹

## 将Hadoop和eclipse联系的插件hadoop2x-eclpise-plugin配置

1. 下载 [hadoop2x-eclipse-plugin-master.zip](https://github.com/winghc/hadoop2x-eclipse-plugin)
 这是在GitHub的源码在Ubuntu上给可以用命令 git clone https://github.com/winghc/hadoop2x-eclipse-plugin

2. 打开文件夹中的release将hadoop-eclipse-plugin-2.x.x.jar文件复制到eclipse目录下的plugins中

3. 重新打开eclipse,点击Windouw选择Preferences 会看到Hadoop Map/Reduce,在Hadoop installation directory中填入hadoop的文件地址，如/usr/local/hadoop 点击Apply and Close

4. 切换 Map/Reduce 开发视图,点击Windows-->Perspective-->Open Perspective-->Other-->Map/Reduce

5. 建立与 Hadoop 集群的连接,先点击右上角的蓝色小象，然后在新出来的窗体中点击右下角的蓝色小象-->New Hadoop Location...
 在跳出来的面板中更改Location Name:MapReduce Locatoin,  DFS MASTER下的port改为9000-->Finsh

6. 可以直接看到HDFS文件结构

# 增加节点的操作
## [参考](https://blog.csdn.net/forever19870418/article/details/62887072)
1.更新所有节点的/etc/hosts

2.无密码登入，即节点间信任关系，相互直接可以SSH

3.更改/usr/local目录的权限 [hadoop@newslaves]# chmod 775 /usr/local

4.创建链接 on new slave:[hadoop@hadoop04 ]$ ln -s /usr/local/hadoop hadoop

5.查看配置文件，slaves文件，路径是否添加,hosts文件是否一致

6.new slave启动datanode和nodemanager服务

hadoop-daemon.sh start datanode

yarn-daemon.sh start nodemanager

7.查看集群状态 hdfs dfsadmin -report有新的节点说明添加成功
