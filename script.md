# Final Project
# Analyzing the Gut Microbiome in Breast Cancer Patients and Healthy Patients

---

# Step 1: Download SRR Data
### Dataset: 16S rRNA sequence data found in human stool and tissue.
1. Download FASTQ files of paired-end reads
   - Create a file named `download_sra.sh`
```
vi download_sra.sh
```
  - Enter the following workflow into the file
```bash
grep -Ff selected_srrs.txt srr_accessions.txt | while read -r SRR; do
    echo "Downloading $SRR..."
    prefetch --max-size 100G $SRR
    fastq-dump --gzip $SRR --split-files -O fastq_files/
done
```
  - Run the `download_sra.sh` script
```
bash download_sra.sh
```
