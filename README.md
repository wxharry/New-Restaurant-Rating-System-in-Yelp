# New-Restaurant-Rating-System-in-Yelp

## How to run
We use [picocli](https://picocli.info/) to manage commands arguments.
The inputs should be like this
``` bash
Usage: Nersy [--rm] STEP SRC INPUT OUTPUT
      STEP     Specify the step of the data manipulation process
      SRC      data source to process
      INPUT    Input directory
      OUTPUT   Output directory
      --rm     Remove the output file if it exists
```


## Install Maven
Download binary version
``` bash
wget https://dlcdn.apache.org/maven/maven-3/3.8.5/binaries/apache-maven-3.8.5-bin.tar.gz
```
Unzip the downloaded package
``` bash
tar xzvf apache-maven-3.8.5-bin.tar.gz
```
Add mvn to path
``` bash
echo 'export PATH=/home/<NET_ID>/apache-maven-3.8.5/bin:$PATH' >> ~/.bashrc
```
Verify the installation
``` bash
mvn -v
```

## Build and Run on HPC
Pull the source code from Github

```bash
git pull
```

build the jar file

```
mvn clean package
```

Prepare the input files
``` bash
  hadoop fs -mkdir /user/<NET_ID>/project
  hadoop fs -mkdir /user/<NET_ID>/project/input
  hadoop fs -put <inputfile> /user/<NET_ID>/project/input
  
```

Remove the output directory in HDFS

```bash
hadoop fs -rm -r /user/<NET_ID>/project/output
```

Run with Hadoop

```
hadoop jar target/nersy-jar-with-dependencies.jar Nersy <STEP> <SRC> /user/<NET_ID>/project/input/ /user/<NET_ID>/project/output/
```

Check the results
``` bash
  hadoop fs -ls /user/xw2788/project/output
  hadoop fs -cat /user/xw2788/project/output/part-r-00000
```

## How to set up a local developing environment (No installation of Hadoop needed)
* We use Maven to manage the dependencies
* For Windows users, a winutil is needed. Be sure to download a compatible version [here](https://github.com/steveloughran/winutils) and add it to the environment of PC.
* Restart the IDEA or maybe the computer after setting up the environment

## Reference

[Hadoop: Intellij结合Maven本地运行和调试MapReduce程序 (无需搭载Hadoop和HDFS环境) - Penguin (polarxiong.com)](https://www.polarxiong.com/archives/Hadoop-Intellij结合Maven本地运行和调试MapReduce程序-无需搭载Hadoop和HDFS环境.html)

[steveloughran/winutils: Windows binaries for Hadoop versions (built from the git commit ID used for the ASF relase) (github.com)](https://github.com/steveloughran/winutils)

[大数据学习踩坑之 HADOOP_HOME and hadoop.home.dir are unset. - yucreator - 博客园 (cnblogs.com)](https://www.cnblogs.com/yuqiliu/p/14388423.html)
