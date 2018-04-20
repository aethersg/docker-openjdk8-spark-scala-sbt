# docker-openjdk8-spark-scala-sbt

This image contains the following softwares:

* OpenJDK 64-Bit v1.8.0_161
* Scala v2.12.5
* SBT v1.1.4
* Apache Spark v2.3.0

## Run Spark image
### Run the latest image i.e. Apache Spark `2.3.0`

    docker run -it -p 4040:4040 -p 8080:8080 -p 8081:8081 -h spark --name=spark judetan/docker-openjdk8-spark-scala-sbt


The above step will launch and run the image with:

* `root` is the user we logged into.
 * `spark` is the container name. `--name=spark`
 * `spark` is host name of this container. `-h spark`
 	* This is very important as Spark Slaves are started using this host name as the master.
 * The container exposes ports 4040, 8080, 8081 for Spark Web UI console(s).

## Check softwares and versions

### Host name

    root@spark:~# hostname
    spark

### Java

    root@spark:~# java -version
    openjdk version "1.8.0_162"
    OpenJDK Runtime Environment (build 1.8.0_162-8u162-b12-1~deb9u1-b12)
    OpenJDK 64-Bit Server VM (build 25.162-b12, mixed mode)

### Scala

    root@spark:~# scala -version
    Scala code runner version 2.12.5 -- Copyright 2002-2018, LAMP/EPFL and Lightbend, Inc.

### SBT

Running `sbt about` will download and setup SBT on the image.

### Spark

```
root@spark:~# spark-shell
Spark context Web UI available at http://spark:4040
Spark context available as 'sc' (master = local[*], app id = local-1524207811656).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 2.3.0
      /_/
         
Using Scala version 2.11.8 (OpenJDK 64-Bit Server VM, Java 1.8.0_162)
Type in expressions to have them evaluated.
Type :help for more information.

scala> 

```
## Spark commands
All the required binaries have been added to the `PATH`.

### Start Spark Master

    start-master.sh

### Start Spark Slave

    start-slave.sh spark://spark:8088

### Execute Spark job for calculating `Pi` Value

    spark-submit --class org.apache.spark.examples.SparkPi --master spark://spark:8088 $SPARK_HOME/examples/jars/spark-examples*.jar 100
    .......
    .......
    Pi is roughly 3.140495114049511


OR even simpler

    $SPARK_HOME/bin/run-example SparkPi 100
    .......
    .......
    Pi is roughly 3.1413855141385514

Please note the following command expects Spark Master and Slave to be running. 

### Start Spark Shell

    spark-shell --master spark://spark:8088

### View Spark Master WebUI console

 `via port 8080 `
### View Spark Worker WebUI console

`via port 8081 `

### View Spark WebUI console
Only available for the duration of the application.

`via port 4040 `

## License [![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)
Copyright &copy; 2018 Jude tan<br>
Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).