# Metagenomic Analysis Pipeline

![Screenshot from 2023-02-13 11-00-12](https://user-images.githubusercontent.com/64088888/218414866-a300ccc6-4db2-4453-8e38-0d407945aa0e.png)

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

## Introduction
## Installation
There are two ways to install Hadoop, i.e. Single node and 
Multi-node.
◦ A single node cluster : means only one DataNode running and 
setting up all the NameNode, DataNode, ResourceManager, and 
NodeManager on a single machine. This is used for studying and 
testing purposes.
<br>
◦ Multi-node cluster: there are more than one DataNode running and 
each DataNode is running on different machines. The multi-node 
cluster is practically used in organizations for analyzing Big Data.

PREREQUISITES
1. You must have Java installed (at least Java 8) <br>
sudo apt-get install openjdk-8-jdk
2.  Install ssh
 sudo apt-get install ssh

SSH (Secure Shell) is a software package that enables secure system administration and file transfers over insecure networks. It is used in nearly every data center and in every large enterprise.
Download the Hadoop 3.3.0 Package using the following command :

• wget http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz

Extract the archive file:
• tar -xvf hadoop-3.3.0.tar.gz

Createhadoopdirectory:
• sudo mkdir /usr/local/hadoop

Change the directory to: 
• cd hadoop-3.3.0

Move the extracted file to /usr/local/hadoop directory: 
• sudo mv * /usr/local/hadoop

Add The Hadoop And Java Paths In The Bash File (.Bashrc)
sudo gedit .bashrc

For applying all these changes to the current Terminal, execute the source command.
◦ source .bashrc
We want to make sure that Java and Hadoop have been properly installed on
our system :
◦ java –version
◦ hadoop version

##Set up Hadoop Configuration
cd /usr/local/hadoop/etc/hadoop
sudo gedit hadoop-env.sh
## Usage

