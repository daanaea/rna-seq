#rna-seq 

Adapter trimming is a useful step of pre-alignment QC, which removes low quality reads and contaminating adapter sequences (which occur when the length of DNA sequences is longer than the DNA insert).


>[!NOTE]
><u>Adapter sequences</u> are synthetic DNA sequences added *in vitro* (in the lab) during the preparation of DNA/RNA libraries for high-throughput sequencing.
>Adapters provide specific binding sites for the sequencing primers. (For example, during Illumina sequencing by synthesis, these primers bind to the adapter sequences and initiate the synthesis of new DNA strands, allowing the sequencing machine to "read" the sequence of DNA fragments.)

### Command
```bash
	fastp \
		-i data/raw_reads/SRR1553531_1.fastq \ 
		-I data/raw_reads/SRR1553531_2.fastq \ 
		-o data/trimmed_reads/SRR1553531_1.trimmed.fastq.gz \ 
		-O data/trimmed_reads/SRR1553531_2.trimmed.fastq.gz \ 
		--json data/fastp_results/SRR1553531.json \
		--html data/fastp_results/SRR1553531.html \ 
		--detect_adapter_for_pe \
		--thread 8
```
Output trimmed FASTQ files. `--thread 8` is the number of CPU cores used.
```bash
	echo $totalreads
```

%% ### HTML report
 %%








