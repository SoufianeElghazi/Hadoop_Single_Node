# Install Hadoop single node on Ubuntu operating system

This guide will walk you through the steps to install Hadoop on an Ubuntu operating system.

## Install Java JDK 8

```bash
sudo apt update
sudo apt install openjdk-8-jdk
```
Make sure to verify the installation after completing this step.
To check it’s there
```bash
cd /usr/lib/jvm
``` 
open .bashrc file with:
```bash
sudo nano .bashrc 
``` 
 and paste these commands:

```bash
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 
export PATH=$PATH:/usr/lib/jvm/java-8-openjdk-amd64/bin 
export HADOOP_HOME=~/hadoop-3.3.6/ 
export PATH=$PATH:$HADOOP_HOME/bin 
export PATH=$PATH:$HADOOP_HOME/sbin 
export HADOOP_MAPRED_HOME=$HADOOP_HOME 
export YARN_HOME=$HADOOP_HOME 
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop 
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native 
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native" 
export HADOOP_STREAMING=$HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.3.6.jar
export HADOOP_LOG_DIR=$HADOOP_HOME/logs 
export PDSH_RCMD_TYPE=ssh
```
( ssh — secure shell — protocol used to securely connect to remote server/system — transfers data in encrypted form)

```bash
sudo apt-get install ssh
``` 
now go to hadoop.apache.org  website download the tar file
(hadoop.apache.org — download tar file of hadoop.)
```bash
tar -zxvf ~/Downloads/hadoop-3.3.6.tar.gz 
``` 
(Extract the tar file)
```bash
cd hadoop-3.3.6/etc/hadoop
``` 
now open hadoop-env.sh
```bash
sudo nano hadoop-env.sh
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 (set the path for JAVA_HOME) 
``` 
core-site.xml
```bash
<configuration> 
 <property> 
 <name>fs.defaultFS</name> 
 <value>hdfs://localhost:9000</value>  </property> 
 <property> 
<name>hadoop.proxyuser.dataflair.groups</name> <value>*</value> 
 </property> 
 <property> 
<name>hadoop.proxyuser.dataflair.hosts</name> <value>*</value> 
 </property> 
 <property> 
<name>hadoop.proxyuser.server.hosts</name> <value>*</value> 
 </property> 
 <property> 
<name>hadoop.proxyuser.server.groups</name> <value>*</value> 
 </property> 
</configuration>
``` 
hdfs-site.xml
```bash
<configuration> 
 <property> 
 <name>dfs.replication</name> 
 <value>1</value> 
 </property> 
</configuration>
``` 
mapred-site.xml

```bash
<configuration> 
 <property> 
 <name>mapreduce.framework.name</name>  <value>yarn</value> 
 </property> 
 <property>
 <name>mapreduce.application.classpath</name> 
  
<value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value> 
 </property> 
</configuration>
``` 
yarn-site.xml

```bash
<configuration> 
 <property> 
 <name>yarn.nodemanager.aux-services</name> 
 <value>mapreduce_shuffle</value> 
 </property> 
 <property> 
 <name>yarn.nodemanager.env-whitelist</name> 
  
<value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREP END_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value> 
 </property> 
</configuration>
``` 
ssh

```bash
ssh localhost 
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa 
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys 
chmod 0600 ~/.ssh/authorized_keys 
hadoop-3.3.6/bin/hdfs namenode -format
``` 
format the file system
```bash
export PDSH_RCMD_TYPE=ssh
```
To start
```bash
start-all.sh
(Start NameNode daemon and DataNode daemon) 
localhost:9870
oem@Zoro:~$ hadoop fs -mkdir /user
oem@Zoro:~$ hadoop fs -mkdir /user/test
oem@Zoro:~$ touch demo.csv
oem@Zoro:~$ hadoop fs -put demo.csv /user/test

stop-all.sh

exit
```

In this markdown file, I've provided a basic guide for installing Hadoop on Ubuntu, including the installation of Java JDK 8 and a placeholder for the steps to download and configure Hadoop. You can also add more details or customize it further based on your specific requirements.
