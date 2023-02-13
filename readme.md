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

![Screenshot from 2023-02-13 11-01-55](https://user-images.githubusercontent.com/64088888/218415044-8f332f6c-11d1-41c2-88ce-4863d6bf1158.png)
