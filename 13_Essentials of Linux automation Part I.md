# 13. Essentials of Linux automation Part I

Much of these would be something that you have covered before. So we are just recapping back some of the important points here. 

## 13.1. Linux file system hierachy

The Linux file system hierarchy is a standardized directory structure that organizes system files, user data, and applications in a logical manner. Understanding this structure is crucial for managing bioinformatics projects effectively.

**(a) Root directory structure**
`/ (root):` The top-level directory containing all other directories
`/home:` Contains user home directories

**(b) Key system directories**
- `/bin:` Essential command binaries that contains basic commands like `ls`, `cp`, `mv`

- `/usr`: User programs and data such as `/usr/bin` for non-essential command binaries and `/usr/lib` Libraries for programs

- `/etc`: System configuration files

You can set up a project organization like this:

```
project/
├── data/
│   ├── raw/          # Original data
│   └── processed/    # Cleaned and filtered data
├── scripts/          # Analysis scripts
├── results/          # Analysis outputs
└── docs/             # Documentation
```

## 13.2. Essential Linux commands

Linux commands are the primary tools for interacting with the system and processing data. These commands form the foundation of data analysis pipelines.

**(a) File operations**

Here are some of the basic file manipulation commands:

- `cp` (copy):

```
# Just examples. Do not run. 
cp patient001.txt backup/
cp dna_sequence.fasta backup/
```

- `mv` (move):

```
# Just examples. Do not run. 
mv old_records/ archived_records/
mv raw_sequences/ processed_sequences/
```

- `rm` (remove):

```
# Just examples. Do not run. 
rm old_patient_data.txt
rm -r failed_experiments/          # Remember that you would need to use -r flag to remove folder
```

- `mkdir` (move):

```
# Just examples. Do not run. 
mkdir patient_cohort_2024
mkdir protein_analysis_results
```

**(b) Text processing commands**

Here are some commands for viewing and manipulating text files:

- `head` / `tail` (view beginning or end of files):

```
# Just examples. Do not run. 
head -n 10 patient_list.txt
head -n 20 sequence.fastq
```

- `cat` (display file contents):

```
# Just examples. Do not run. 
cat patient_summary.txt
cat gene_expression.csv
```

- `less` / `more` (view beginning or end of files):

```
# Just examples. Do not run. 
less medical_report.txt
less alignment_results.txt
```

**(c) Data manipulation commands**

Here are some advanced text processing tools:

- `grep` (search text patterns):

```
# Just examples. Do not run. 
grep "diabetes" patient_records.txt
grep "ATCG" dna_sequences.fasta
```

- `awk` (pattern scanning and processing):

```
# Just examples. Do not run. 
awk '$3 > 140' blood_pressure.txt
awk '$4 > 30' quality_scores.txt
```

- `sed` (stream editor for text transformation):

```
# Just examples. Do not run. 
sed 's/patient/PATIENT/' records.txt
sed 's/A/T/' dna_sequence.txt
```

**(d) Pipes and rediction**

Pipes and redirection are powerful features that allow combining commands and controlling data flow between them.

- `|` (pipe): Send output of one command to another
- `>` (redirect output): Write output to a file (overwrite)
- `>>` (append): Add output to end of file
- `<` (input redirection): Read input from file

```
# Just examples. Do not run. 
grep "high_risk" patients.txt | sort | uniq > high_risk_patients.txt
cat sequences.fasta | grep "ATCG" | wc -l > sequence_count.txt
```

**(e) File compression**

File compression is essential in bioinformatics due to the large size of genomic and medical data. Understanding different compression methods and their appropriate use cases helps manage storage efficiently and optimize data transfer.

**(a) gzip/gunzip**

This is the most common compression utility in Linux.


```
# Compress a single file
gzip patient_data.txt                 # Creates patient_data.txt.gz
gzip -c input.fastq > input.fastq.gz  # Compress while keeping original

# Decompress
gunzip patient_data.txt.gz              # Restores original file
gunzip -c input.fastq.gz > input.fastq  # Decompress while keeping compressed file
```

**(b) bzip2/bunzip2**

This offers better compression than gzip but is slower.

```
# Compress files
bzip2 large_alignment.sam       # Creates large_alignment.sam.bz2
bzip2 -k original_data.txt      # Keep original file (-k flag)

# Decompress
bunzip2 compressed_data.bz2
bunzip2 -k archive.bz2         # Keep compressed file
```

**(c) tar**

This combines multiple files into a single archive, optionally with compression.

The syntax for tar is as below:

```
tar [options] [archive_name] [files/directories to be compressed]
```

**The common operation flags** are as below

c - Create new archive
x - Extract archive
t - List contents of archive
r - Append files to archive
u - Update existing files in archive
f - Specify archive filename (almost always used)
v - Verbose output (shows processing files)
z - Use gzip compression (.tar.gz)
j - Use bzip2 compression (.tar.bz2)
p - Preserve permissions
k - Don't overwrite existing files

Here's some example that you can try out using the files XXXXX. 

```
# Create tar archive (without compression)
tar -cf project_backup.tar project_folder/

# Create compressed tar archive with gzip
tar -czf project_backup.tar.gz project_folder/
tar -czf patient_cohort.tar.gz patient_data/ analysis_scripts/ results/

# Create compressed tar archive with bzip2
tar -cjf project_backup.tar.bz2 project_folder/

# Extract tar archive
tar -xf project_backup.tar

# Extract compressed archive
tar -xzf project_backup.tar.gz
tar -xjf project_backup.tar.bz2

# List contents of tar archive
tar -tf project_backup.tar
tar -tzf project_backup.tar.gz
```

**(e) System monitoring**

It is important to understand system resources and managing files efficiently for bioinformatics work.

**(a) Process monitoring**

```
# View running analysis processes
top
ps aux | grep "analysis"

# Monitor sequence alignment job
htop
```

**(b) Disk usage**

```
# Check storage space
df -h

# Check directory sizes
du -sh */
```


