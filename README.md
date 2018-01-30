# Install Hive on Centos 7

## 1) Download appropriate version of Pig

Chage user to "hadoop" and downlaod Hive archive (from https://pig.apache.org/releases.html) to home directory of "hadoop" user. Choose the Hive version that is copatible with currently installed Hadoop version.
```
su - hadoop
wget -b http://www-eu.apache.org/dist/hive/hive-1.2.2/apache-hive-1.2.2-bin.tar.gz
```

## 2) Extract archive 
```
tar -xvf apache-hive-1.2.2-bin.tar.gz
```

## 3) Edit .bash_profile of "hadoop" user
```
vi .bash_profile
```
add following settings:
```
export HIVE_HOME=/home/hadoop/apache-hive-1.2.2-bin
export PATH=$PATH:/home/hadoop/apache-hive-1.2.2-bin/bin
```
to apply changes:
```
source .bash_profile
```

## 4) Create HIVE directory in Hadoop HDFS 

start hadoop if not started yet
```
start-all.sh
```
Check if all 5 daemons are active and running using JPS:
```
jps
```
Hadoop daemons:
- ResourceManager
- SecondaryNameNode
- DataNode
- NodeManager
- NameNode

Create Hive directory in HDFS:
```
hdfs dfs -mkdir -p /user/hive/warehouse
```
Assign appropriate permission to this directory:
```
hdfs dfs -chmod g+w /user/hive/warehouse
```
Assign appropriate permission to this TMP directory:
```
hdfs dfs -chmod g+w /tmp
```

## 5) Inform Hive about home directory of Hadood
Edit hive-config.sh at HIVE_HOME/bin to inform Hive about home directory of Hadood
```
cd
vi $HIVE_HOME/bin/hive-config.sh
```
add following setting to the end of the file
```
export HADOOP_HOME=/home/hadoop/hadoop-2.7.2
```
## 6) Congratulation! Its Done...
to check Hive version
```
hive --version
```
