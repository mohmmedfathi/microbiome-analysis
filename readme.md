# Metagenomic Analysis Pipeline

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
