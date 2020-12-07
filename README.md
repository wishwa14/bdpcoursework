# Map-Reduce Analysis

This document will illustrate the step by step guide to analyse football data of first official match in 1872 up to 2020.

## Build the project
```
mkdir /Documents/bdpproject
cd /Documents/bdpproject/
git clone https://github.com/wishwa14/bdpcoursework.git
cd bdpcoursework
mvn clean install
```
## Set up the environment

```
docker pull suhothayan/hadoop-hive-pig:2.7.1
docker run -p 8088:8088 -p 50070:50070 --name hadoop-hive-pig -v /Documents/bdpproject:/resource -d suhothayan/hadoop-hive-pig:2.7.1
```
## Login to the container and manage dataset for processing

```
docker exec -it <container id> bash
cd resource
unzip dataset/results.zip
```

## Copy dataset into hdfs

```
hdfs dfs -mkdir coursework
hdfs dfs -mkdir coursework/matches
hdfs dfs -put dataset/results.csv oursework/matches
```

## The total number of matches played, ended with a result and drawn.

```
yarn jar bdpcoursework/target/bdp-coursework-1.0-SNAPSHOT.jar com.wishwa.matches.Drawn coursework/matches /output/coursework
```
### Check the successful execution
```
hdfs dfs -ls /output/coursework
-rw-r--r--   1 root supergroup          0 2020-12-06 22:34 /output/coursework/_SUCCESS
-rw-r--r--   1 root supergroup      23720 2020-12-06 22:34 /output/coursework/part-r-00000
```
### Check the results
```
hdfs dfs -cat /output/coursework/part-r-00000
Number of matches Drawn 	9592
```
## Total number of matches played in each city.
```
yarn jar bdpcoursework/target/bdp-coursework-1.0-SNAPSHOT.jar com.wishwa.matches.CityGroup coursework/matches /output/coursework
```
### Check the successful execution
```
hdfs dfs -ls /output/coursework
-rw-r--r--   1 root supergroup          0 2020-12-06 22:34 /output/coursework/_SUCCESS
-rw-r--r--   1 root supergroup      23720 2020-12-06 22:34 /output/coursework/part-r-00000
```
### Check the results
```
hdfs dfs -cat /output/coursework/part-r-00000
6th of October City	5
Aachen	2
Aalborg	7
Aarau	1
Aarhus	2
Abeokuta	2
Aberdare	1
Aberdeen	15
……………
```





