# Windows安装Spark2.1

1、下载Spark2.1   地址：[Index of /dist/spark (apache.org)](https://archive.apache.org/dist/spark/)

2、下载winutils    地址：[kontext-tech/winutils: winutils.exe hadoop.dll and hdfs.dll binaries for hadoop windows (github.com)](https://github.com/kontext-tech/winutils)

3、设置环境变量

```bash
SPARK_HOME
PATH
```

4、执行命令

```bash
cd C:\Users\chenxilin\Install\BigData\hadoop-2.7.7\bin>
winutils.exe chmod 777 C:\tmp\hive
```

5、启动spark-shell

```bash
cd C:\Users\chenxilin\Install\BigData\spark-2.1.3-bin-hadoop2.7\bin
spark-shell.cmd
```



