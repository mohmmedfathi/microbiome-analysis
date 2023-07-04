# Metagenomic Analysis Pipeline

![Screenshot from 2023-02-13 11-00-12](https://user-images.githubusercontent.com/64088888/218414866-a300ccc6-4db2-4453-8e38-0d407945aa0e.png)

<br>
<br>


<br>

![Screenshot from 2023-02-13 11-03-50](https://user-images.githubusercontent.com/64088888/218415435-71e089e3-a604-43ad-ba3e-85e3ad4ad0c1.png)

<br>

<br>


![Screenshot from 2023-02-13 11-05-40](https://user-images.githubusercontent.com/64088888/218416004-f38cf3e5-f20e-4790-90f3-36f54d747d7b.png)


![Figure4_README](https://user-images.githubusercontent.com/64088888/209128528-73c13ea8-35bc-44c5-bcb4-d155f562de17.jpg)
## Download and install anaconda(version 3 recommended)
### :beginner: Add channels

```
conda config --add channels conda-forge\
conda config --add channels bioconda\
conda config --add channels daler\
conda config --add channels defaults\
```
### :beginner: Download the polishing tool pilon

```
mkdir apps\
wget https://github.com/broadinstitute/pilon/releases/download/v1.23/pilon-1.23.jar -O apps/pilon.jar
```
### :beginner: Activate the analysis environment
```
source activate microbiomeENV
```
### :warning: Add permission to all scripts
```
chmod +x *.{sh}
```
![Screenshot from 2023-02-13 11-02-51](https://user-images.githubusercontent.com/64088888/218415240-443e68a8-bc6d-4618-838e-1c677e5a5357.png)



## pipeline step : 

### step 1 : download data
### :hammer: Step 2: Perform QC on the raw reads
```
./qc_raw_reads.sh
```
### :hammer: Step 3: Trim reads using sickle
```
./trim_reads.sh
```
### :hammer: Step 4: Perform QC on the trimmed reads

```
 ./qc_trimmed_reads.sh
```
### :hammer: Step 5: Perform de novo assembly using spades

```
./assemble.sh
```
### :hammer: Step 6 : Polish the draft assembly using pilon 
This is meant to improve the draft assembly. The scaffolds will be used. You can also modify the script to use the contigs and compare the result 
```
./polish.sh
```
### :hammer: Step 7: Perform QC for both raw assembly and polished assembly
```
./qc_assembly.sh
```


## :warning: citation
this work is done depends on 
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5830445/



<br>
<br>

<hr>


# Hadoop 
Hadoop, a distributed computing framework, can greatly enhance the scalability and efficiency of processing large-scale metagenomics data.
we will provides a guide and code examples for leveraging Hadoop in metagenomics analysis.

## Introduction :microbe:
This repository aims to provide a comprehensive guide on how to use Hadoop for metagenomics analysis, including setup instructions, usage guidelines, and example code snippets. It covers the necessary steps to process metagenomics data in a distributed manner using Hadoop MapReduce,Spark.

## Built With : 
* ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
* ![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)
* ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
* ![Apache Hadoop](https://img.shields.io/badge/Apache%20Hadoop-66CCFF?style=for-the-badge&logo=apachehadoop&logoColor=black)
* ![Apache Spark](https://img.shields.io/badge/Apache%20Spark-FDEE21?style=flat-square&logo=apachespark&logoColor=black)
* ![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)

## Installation


There are two ways to install Hadoop

Single node and Multi-node. 
<br>
* A single node cluster : means only one DataNode running and setting up all the NameNode, DataNode, ResourceManager, and NodeManager on a single machine. This is used for studying and testing purposes.
* Multi-node cluster: there are more than one DataNode running and each DataNode is running on different machines. The multi-node cluster is practically used in organizations for analyzing Big Data.


## for single node cluster

⚠️ PREREQUISITES

You must have Java installed (at least Java 8)

```
sudo apt-get install openjdk-8-jdk
```

<br>

### SSH :beginner: 

(Secure Shell) is a software package that enables secure system administration and file transfers over insecure networks. It is used in nearly every data center and in every large enterprise. <br>

Install ssh :open_file_folder: :

```bash
sudo apt-get install ssh  
```



### Download the Hadoop 3.3.0 Package using the following command 🛠️ : <br>

* wget http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz

* Extract the archive file: • tar -xvf hadoop-3.3.0.tar.gz 

* Create hadoop directory: • sudo mkdir /usr/local/hadoop

* Change the directory to: • cd hadoop-3.3.0

* Move the extracted file to /usr/local/hadoop directory: • sudo mv * /usr/local/hadoop

* Add The Hadoop And Java Paths In The Bash File (.Bashrc) sudo gedit .bashrc

<br>

![WhatsApp Image 2023-07-03 at 11 15 05 PM](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/c103dfd9-aaac-4091-a8d6-b79b5a058839)

<br>
:pushpin: For applying all these changes to the current Terminal, execute the source command. <br>
◦ source .bashrc  <br>
We want to make sure that Java and Hadoop have been properly installed on our system : 
* java –version 
* hadoop version

<br>

##  :radio_button: Set up Hadoop Configuration 
```bash
cd /usr/local/hadoop/etc/hadoop sudo gedit hadoop-env.sh
```

<br>

![WhatsApp Image 2023-07-03 at 11 18 38 PM](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/eff39034-d4f3-49c8-8832-6fe628a430f8)

<br>

 :radio_button: Edit core-site.xml file: <br>
sudo gedit core-site.xml 

![WhatsApp Image 2023-07-03 at 11 26 52 PM](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/d6d9057e-8d63-40f4-b712-893fc7675981)
<br>

 :radio_button: Edit hdfs-site.xml
sudo gedit hdfs-site.xml
![WhatsApp Image 2023-07-03 at 11 28 25 PM](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/e9122366-f85e-43c2-809e-a0413ad1c181)

<br>
 :radio_button: Edit yarn-site.xml file:
sudo gedit yarn-site.xml

![WhatsApp Image 2023-07-03 at 11 29 16 PM](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/a32eae88-d4d3-4398-8a5e-731be8f3bea5)

<br>
 :radio_button: Edit mapred-site.xml file:
sudo gedit mapred-site.xml

![WhatsApp Image 2023-07-03 at 11 30 21 PM](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/a9fa8ed1-4dd2-4107-8db1-8206a02031c4)
<br>

### Create Master And Workers Files
Connect to localhost :bangbang: :
```bash
ssh localhost
ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
```


Make 2 directory to name node and data node
```
sudo mkdir -p /usr/local/hadoop_store/hdfs/namenode
sudo mkdir -p /usr/local/hadoop_store/hdfs/datanode
```

Change permissions to the login user.
```
sudo chmod 777 -R /usr/local/hadoop_store/hdfs/namenode
sudo chmod 777 -R /usr/local/hadoop_store/hdfs/datanode
sudo chmod 777 -R /usr/local/hadoop
sudo chown hduser:hadoop /usr/local/hadoop
```

Format HDFS :mega:
Go to nameNode Folder and Run the Following Command :eyes:
• 🔨  hdfs namenode –format

![7](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/5cf0e5b6-b00d-4b67-8204-e2608f648ed3)

to run hadoop cluster 
start-all.sh :unlock:

![8](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/c1145ecc-abbb-45b9-9ce9-95292203fd81)

Now, open your browser: http://localhost:9870

![9](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/ef50505e-6f01-4001-9b11-d722b41ffa14)

to open hadoop cluster use http://localhost:8088

![10](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/22c74913-09a3-4029-a5ab-0b110c26ed99)


![multi](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/cd69013a-b465-4c37-b7ee-14ef543a7c08)

 ### multi node cluster 

We will build a multi-node cluster using two Ubuntu boxes in this tutorial. In my humble opinion, the best way to do this for starters is to install, configure and test a “local” Hadoop setup for each of the two Ubuntu boxes, and in a second step to “merge” these two single-node clusters into one multi-node cluster in which one Ubuntu box will become the designated master (but also act as a slave with regard to data storage and processing), and the other box will become only a slave.

step :one:&nbsp; : **SSH access**
<br>
we need to make hduser in master connect to slave without require password,you just have to add the hduser@ata-master public SSH key (which should be in $HOME/.ssh/id_rsa.pub) to the authorized_keys file of hduser@node-1 and node-2


![sshKey](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/34131473-105e-46b7-8b6c-cbdb57f66d7c)

<br>

step :two:&nbsp; :  edti /etc/hosts in master and slaves machine by use  <br>
sudo nano /etc/hosts
:x: add hosts photo in ata folder

step 3️⃣:&nbsp; :  edit workers file in hadoop config use, make this slave and master machine
sudo nano /usr/local/hadoop/etc/hadoop/workers
add work photo in ata folder

step 4️⃣:&nbsp; : verify hostname of all machine to each other , in any machine run this 

ssh ata-master 
ssh node-1
ssh node-2

![mssh2](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/c2a117cf-1a54-45dd-bfda-f5c569e7f25b)


step 5️⃣:&nbsp; : we need to remove temporary data (namenode) in each machine that created in single node cluster
by use : sudo rm -r /tmp/hadoop*
sudo rm -r /tmp/hsper_data

:x: add phoot rmTmp,rmTmp2 in ata/mm just crop photo to add from cd /tmp command 
![rmTmp](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/37ccec25-c287-4141-8b5e-4a6869306176)
![rmTmp](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/10a59de3-6c26-48cc-a7d2-d040c9c7829b)
![rmTmp2](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/2aafe65c-ec9e-4481-af2a-10fabb4d539e)
step 6️⃣:&nbsp; : now we need to reformat cluster that created since single node cluster (do this command in master only):
  hdfs namenode -format

![rmTmpAndFormatHDFS](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/d6f88244-ca37-4a46-a9b9-265c97d90130)


step 7️⃣:&nbsp; : now in master run namenode,datenode and resourceManager

use this command in master start-all.sh


![master](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/67a18510-180b-429b-82c3-c36c77c3f2fb)



step :eight:&nbsp; : check name node and datnode in cluster by run command java jps in master and slaves 

![testJps](https://github.com/mohmmedfathi/golang-learning/assets/64088888/18af75b3-3c32-44d6-aad5-e43ea7b15096)

<hr>

![jps](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/65dfce9a-8716-49b9-b397-689bfb831d83)

<hr>

![yarnStart](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/15d77118-1d77-4368-8fa1-efa4398783dc)

<hr>
Now, open your browser: http://localhost:9870

![guiAfterAddNode2](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/05c53c55-b774-45a8-90a4-2c60c6f22913)

to open hadoop cluster use http://localhost:8088
![clusterAfterNode2](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/f48df71a-b4d4-481f-b4cd-f7b3b22c2929)


<hr>
 
### add spark framework to cluster ❕

what is spark :bulb: :
Spark is an open-source distributed computing system for big data processing. It offers high-speed processing, fault tolerance, and supports various tasks like batch processing, real-time streaming, machine learning, and graph processing. It's flexible, integrates with other tools, and is widely used for efficient data analysis.

step :one: :  Download Apache spark latest version

```
wget http://apache.claz.org/spark/spark-2.4.0/spark-2.4.0-bin-hadoop3.3tgz
```
step :two: : extract spark in master machine and move it to spark folder 
```
	tar -xzf spark-2.4.0-bin-hadoop3.3.tgz
	mv spark-2.4.0-bin-hadoop3.3 spark
```

step :three: : edit worker file in spark on master 

![sparkwo](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/3a2a0e7e-2940-44a4-9112-f20b2a72e11e)

step :four: : edit spark-env.sh in master 

![sdfs](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/03d75e50-2730-44dc-9112-49ad2231eabd)


step :five: :  edit spark-defaults.conf for history server and yarn cluster


![default](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/c96819fa-85ae-4a7a-b0eb-e33f9fcab232)


now we need to make all this config on slaves use

![carbon](https://github.com/mohmmedfathi/golang-learning/assets/64088888/cd7d52bb-425c-4ec0-ae3c-e2d9d331465a)



![editSparkConf](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/47e2622f-0b67-40c7-adac-378e5129332c)


now check gui on browser http://192.168.1.7:8080/



#### Distribute data in cluster (on node-1 and node-2)

my data is two file, file for forward DNA sequence and reverse DNA sequence so run this command to put data in cluster

![carbon (1)](https://github.com/mohmmedfathi/golang-learning/assets/64088888/62a6ab6b-f649-435a-a397-5f9c1180cf04)

<hr>

![addR1ToCluster](https://github.com/mohmmedfathi/microbiome-analysis/assets/64088888/98b51fbc-046d-41c6-bb82-5178bb34955a)


the combination of Spark and HDFS provides a versatile and scalable platform for data processing, making it well-suited for a wide range of tasks including ML processing, graph analysis, genome assembly, and bioinformatics using R and Bioconducto

### conclusion
**By following the instructions and examples provided in this repository**, you will be able to leverage **Hadoop and Spark** to efficiently analyze metagenomics data in a distributed manner. Whether you are working with a small-scale dataset or dealing with big data, Hadoop and Spark can help you process and analyze the data effectively, enabling you to gain valuable insights into the microbial communities.

We hope that this repository serves as a valuable resource for researchers and practitioners in the field of metagenomics analysis. By harnessing the power of Hadoop and Spark, you can unlock new possibilities in understanding and exploring the complex world of microbiomes.


