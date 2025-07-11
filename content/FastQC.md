#rna-seq

[Workshop post](https://hbctraining.github.io/Training-modules/planning_successful_rnaseq/lessons/QC_raw_data.html)

- quick overview of any likely sequencing problems
- summary graphs and tables to quickly access your data
- export of results as an HTML-based report

[Manual](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)


### `FASTQ` file format
Consists of four lines. Has a header starting with `@`.

| Line | Description                                                                                                     |
| ---- | --------------------------------------------------------------------------------------------------------------- |
| 1    | always begins with `@` and then information about the read                                                      |
| 2    | the actual DNA sequence                                                                                         |
| 3    | always begins with `+` and sometimes the same info in line 1                                                    |
| 4    | has a string of characters which represent <u>quality scores</u>; must have same number of characters as line 2 |

*Different quality encoding scales exist (differing by offset in the ASCII table), but note the most commonly used is `fastqsanger` by Illumina since mid-2011*.

```
Quality encoding: !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHI
                  |         |         |         |         |
   Quality score: 0........10........20........30........40  
```

Each quality score represents the probability that the corresponding nucleotide call is incorrect
$$Q = -10 \cdot \log_{10}(P)$$
where $P = 10^{-Q/10}$ is the probability that a base call is erroneous.

Phred quality score of 10 corresponds to 90% base call accuracy, 20: 99%, 30: 99.9%, 40: 99.99%.

### HTML report

- Per base sequence quality
- Per sequence quality scores
- Per base sequence content
	- distribution of A, T, C, G across reads, per base location
	- always FAIL/WARNING, because first 10-12 bases result from the "random" hexamer priming
- Per sequence GC content
	- in general, a central peak corresponds to the expected % GC for the organism
	- distribution should be normal, unless *overrepresented sequences* (sharp peaks on a normal distribution; causes saturation of other genes' expression) or *contamination* with another organism (broad peak)
>[!NOTE]
>Guanine-Cytosine base pairs form three hydrogen bonds (compared to two in AT), which is more stable. There is a positive correlation between GC content and gene expression level.

- Sequence duplication levels
	- number of duplicated sentences in the library
	- number of PCR cycles and amount of input are controlled only during library prep, can just detect *a low complexity library* during RNA-seq if there are too many duplicates
- Overrepresented sequences
	- at least 20 bp sequences that occur in more than 0.1% of the total number of reads
	- detect *contamination* of vector or adapter sequences: if GC % was off, this table can help identify the source

