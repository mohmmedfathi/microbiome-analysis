Perform QC on the raw reads

./qc_raw_reads.sh
Step 3: Trim reads using sickle

./trim_reads.sh
Step 4: Perform QC on the trimmed reads

 ./qc_trimmed_reads.sh

Step 5: Perform de novo assembly using spades

./assemble.sh
Step 6 : Polish the draft assembly using pilon

This is meant to improve the draft assembly. The scaffolds will be used. You can also modify the script to use the contigs and compare the result

./polish.sh
Step 7: Perform QC for both raw assembly and polished assembly

./qc_assembly.sh
Step 8: Generate draft genome by reordering contigs against a reference genome using ragtag\

./reorder_contigs.sh
