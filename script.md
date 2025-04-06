# Final Project
# Analyzing the Gut Microbiome in Breast Cancer Patients and Healthy Patients

## Step 1: Download SRR Data
### Dataset: 16S rRNA sequence data found in human stool and tissue.
1. Download FASTQ files of paired-end reads
   - Create a file named `download_sra.sh`
```
vi download_sra.sh
```
  - Enter the following workflow into the file
```bash
#!/bin/bash

# Load SRA Toolkit if needed
module load sra-toolkit

# Make output directory if it doesn't exist
mkdir -p fastq_files

# Loop through each SRR in your list
while read -r SRR; do
    echo "Downloading $SRR..."
    prefetch --max-size 100G "$SRR"
    fastq-dump --gzip --split-files -O fastq_files/ "$SRR"
done < accession_list.txt
```
  - Run the `download_sra.sh` script
```
bash download_sra.sh
```
