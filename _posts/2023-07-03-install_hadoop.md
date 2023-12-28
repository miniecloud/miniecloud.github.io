---
title: 하둡 설치하기(CentOS7)
author: mini
date: 2023-07-03 11:50:00 +0800
categories: [Etc, Data Engineering]
tags: [data engineering]
toc : true
---


설치 환경 : CentOS7

### 1. 준비
#### 1. java 설치
```
sduo yum install -y java-1.8.0-openjdk
```
#### 2. hadoop 설치
```
wget http://www-us.apache.org/dist/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz
tar -zxvf hadoop-2.7.3.tar.gz
```
#### 3. ssh 설치
```
ssh-keygen -t rsa -b 4096
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```


<br/><br/>
### 2. 환경설정
#### 1. /etc/hosts
```
ip  hostname
ip  hostname
```
#### 2. ~/.bashrc
```
export HADOOP_HOME=/home/user/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_NOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
```

#### 3. 기타 설정
/hadoop/etc/hadoop/hadoop-env.sh<br/>

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk

export HDFS_NAMENODE_USER=root
export HDFS_DATENODE_USER=root
exprot HDFS_SECONDARYNAMENODE=root
export YARN_RESOURCEMANAGER_USER=root
export YARN_NODEMANAGER=root
export YARN_NODEMANAGER_USER=root
```


/hadoop/etc/hadoop/core-site.xml
```
<property>
  <name>fs.default.name</name>
  <value>hdfs://localhost:9000</value>     # 마스터 서버의 이름
</property>

```

/hadoop/etc/hadoop/hdfs-site.xml
```
<property>
  <name>dfs.replication</name>
  <value>1</value>  #데이터를 1개만 복사:가상분산모드, 3일경우:완전분산모드
</property>
<property>
  <name>dfs.name.dir</name>
  <value>file:///home/user/hadoopdata/hdfs/namenode</value>
</property>
<property>
  <name>dfs.data.dir</name>
  <value>file:///home/user/hadoopdata/hdfs/datanode</value>
</property>
```

/hadoop/etc/hadoop/mapred-site.xml
```
<property>
  <name>mapreduce.framework.name</name>
  <value>yarn</value>
</property>
```

/hadoop/etc/hadoop/yarn-site.xml
```
 <property>
  <name>yarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
</property>
<property>
  <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
  <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
```

➕ `source [파일명]`


<br/>
#### 실행했을때 에러
🛑 WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable 해결방법

~/.bashrc
```
export HADOOP_OPTS=$HADOOP_OPTS -D.java.library.path=$HADOOP_NAME/lib/native
```


<br/>
※ Graphical.target 적용안될 때
```
yum groupinstall -y "GNOME Desktop" "Graphical Administration Tools"
```

