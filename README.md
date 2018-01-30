# Install Hive on Centos 7

## 1) Download appropriate version of Pig

Chage user to "hadoop" and downlaod Hive archive (from https://pig.apache.org/releases.html) to home directory of "hadoop" user
```
su - hadoop
wget -b http://www-eu.apache.org/dist/hive/hive-1.2.2/apache-hive-1.2.2-bin.tar.gz
```

Extract archive 
tar -xvf apache-hive-1.2.2-bin.tar.gz

Edit .bash_profile of hadoop user

vi .bash_profile

add following settings:
export HIVE_HOME=/home/hadoop/apache-hive-1.2.2-bin
export PATH=$PATH:/home/hadoop/apache-hive-1.2.2-bin/bin

to apply changes:
source .bash_profile

Now its time to create HIVE directory in Hadoop HDFS 

start hadoop if not started yet
start-all.sh

Check if all 5 daemons are active and running using JPS:
jps
ResourceManager
SecondaryNameNode
DataNode
NodeManager
NameNode

Create Hive directory in HDFS:
hdfs dfs -mkdir -p /user/hive/warehouse

Assign appropriate permission to this directory:
hdfs dfs -chmod g+w /user/hive/warehouse

Assign appropriate permission to this TMP directory:
hdfs dfs -chmod g+w /tmp


Edit hive-config.sh at HIVE_HOME/bin to inform Hive about home directory of Hadood
cd
vi apache-hive-1.2.2-bin/bin/hive-config.sh



export HADOOP_HOME=/home/hadoop/hadoop-2.7.2
