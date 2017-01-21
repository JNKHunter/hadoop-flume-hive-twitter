## Install OpenJDK
https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-ubuntu-16-04

## Install Hadoop in pseudo distributed mode on Ubuntu 16.0.4:
https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html#Pseudo-Distributed_Operation

core-site.xml
```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/usr/local/hadoop/tmp</value>
    </property>

    <property>
        <name>hadoop.proxyuser.YOUR_USER_NAME.groups</name>
        <value>*</value>
    </property>

    <property>
        <name>hadoop.proxyuser.YOUR_USER_NAME.hosts</name>
        <value>*</value>
    </property>
	
</configuration>
```
The hadoop.proxyuser properties allows jdbc to connect as the current user 


hdfs-site.xml
```xml
<configuration>
<property>
     <name>dfs.datanode.data.dir</name>
        <value>/usr/local/hadoop/dfs/data</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>/usr/local/hadoop/dfs/name</value>
    </property>

    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

mapred-site.xml
```xml
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```

slaves
```
localhost
```

yarn-site.xml
```xml
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services.mapreduce_shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
</configuration>
```

Bash profile (~/.profile on Ubuntu)

```
export HADOOP_HOME=/usr/local/hadoop
PATH="$PATH:$HADOOP_HOME/bin"
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
```



Add the json serde jar to the hive classpath
```
<property>
    <name>hive.aux.jars.path</name>
    <value>/usr/lib/hive/lib/json-serde-1.3.8-SNAPSHOT-jar-with-dependencies.jar</value>
    <description>The location of the plugin jars that contain implementations of user defined functions and serdes.</description>
</property>
```

## Install MYSQL to use as the Hive metastore (Derby feels icky to me)
https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-16-04

## Create the Hive schema
https://cwiki.apache.org/confluence/display/Hive/Hive+Schema+Tool
