# Finalproject

---
Our goal is to compare gut samples of healthy patients and breast cancer patients. Here, we can quantify the differences in bacteria present, potenitally identifying differencies in quantity and species.

Also, we can look at tissue samples from cancer patietns and compare that to the bacteria found in their gut microbiota. 

All of our data should be paired and amplicon. 

For this project we will be using:

QUIIME2 --> to quantify the amount of bacteria present in each sample. This is available in the HPC.
---
## **Step 2: Data Quality Control**

1. Run fastqc
```
module load FastQC
mkdir fastqc_raw_data_out
fastqc -t 4 fastq/*.fastq -o fastqc_raw_data_out
```
2. Run multiqc (will not work if you activate conda environment first, in such case `conda deactivate` before running multiqc)
```
module load python/3.8.6
multiqc --dirs fastqc_raw_data_out --filename multiqc_raw_data.html
```
3. Add, commit and push file to github repository. You can also transfer files using GLOBUS connect.
```
git add "multiqc_raw_data.html"
git commit -m "Adding multiqc results"
git push origin main
```
4. Go to web browser github and download `multiqc_raw_data.html`
5. Open file in web browser
---
## **Step 3: Generate Metadata File**
```
vi metadata.tsv
```
- Type `I` to make changes
- Replace Cancer with Tissue and Breast with Cancer
```
sed -i 's/old-text/new-text/g' metadate.tsv
```

## **Step 3: Import Data into QIIME 2**
### Import the data:
1. We need to change our raw files names so that they can be read by qiime
- Create directory for renamed files
```
mkdir -p casava_reads
```
  - Open the vi editor
```
vi rename.sh
```
  - Type `I` to edit and write the following:
```
#!/bin/bash
for file in fastq/*_1.fastq; do
    base=$(basename "$file" _1.fastq)
    
    cp "fastq/${base}_1.fastq" "casava_reads/${base}_S1_L001_R1_001.fastq"
    cp "fastq/${base}_2.fastq" "casava_reads/${base}_S1_L001_R2_001.fastq"
done
```
- Run rename.sh script using:
```
bash rename.sh
```
2. Let's create the following directory
```         
mkdir reads_qza
```
---

