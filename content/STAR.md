#rna-seq 

To resolve geneInfo.tab error, install [pre-release version](https://github.com/dobinlab/STAR_pre_releases/releases/tag/2.7.11b_alpha_2024-02-09).

### FASTA and GTF files
We use FASTA for alignment and GTF for quantification.

A FASTA file contains a reference genome or a reference transcriptome.

A GTF (Gene Transfer Format) is a tab-delimited text file that holds information about gene structure and annotations on a genome
- each row describes one specific feature
- key columns:
	- `seqname`, `source`, `feature` (gene, exon or CDS for coding sequence)
	- `start` and `end` of the feature on the chromosome
	- `strand` (forward + or reverse -) 
	- `attribute` is a list of key-value pairs, giving extra information like gene_id and transcript_id

### Command

STAR genome index
```bash
	STAR --runThreadN 8 \ 
		--runMode genomeGenerate \ 
		--genomeDir genome_dir \ 
		--genomeFastaFiles genome_dir/Saccharomyces_cerevisiae.fa \ 
		--sjdbGTFfile genome_dir/Saccharomyces_cerevisiae.gtf \ 
		--sjdbOverhang 99
```

Alignment
```bash

STAR --runThreadN 8 \ 
	--genomeDir genome_dir \ 
	--readFilesIn "$TRIMMED_READ1" "$TRIMMED_READ2" \ 
	--readFilesCommand gunzip -c \ 
	--outFileNamePrefix "$OUTPUT_SAM_PREFIX" \ 
	--outSAMtype BAM SortedByCoordinate \ 
	--outSAMunmapped Within \ 
	--outFilterType BySJout \ --outFilterMismatchNmax 999 \ --outFilterMismatchNoverLmax 0.04 \ --outFilterMultimapNmax 20 \ --alignIntronMin 20 \ --alignIntronMax 1000000 \ --alignMatesGapMax 1000000 \ --alignSJoverhangMin 8 \ --alignSJDBoverhangMin 1 \ --quantMode GeneCounts \ --sjdbScore 1 \ --limitBAMsortRAM 8000000000


```

### `_.final.out`

>[!NOTE]
>**Bad example: reads that we are trying to align are twice longer than needed.**
>- Average input read length | 195
>- Uniquely mapped reads number | 5
>- Average mapped length | 96.40
>- Number of reads unmapped: too short | 701512
>
>`head -n 4 SRR1553531_1.fastq`: check whether the length of reads matches.




### BAM files
```Bash
echo "Indexing BAM file..." samtools index SRR1553531_Aligned.sortedByCoordinate.bam
```

```Bash
head SRR1553531_ReadsPerGene.out.tab
wc -l SRR1553531_ReadsPerGene.out.tab # Count number of genes
```

Binary Alignment Map is a compressed, binary version of a SAM file (Sequence Alignment/Map).


