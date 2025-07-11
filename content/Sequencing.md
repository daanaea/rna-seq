#rna-seq 

>[!SUMMARY]
>Number of clusters = number of reads.
>Number of sequencing cycles = length of reads.
>
>Plasmidsaurus (that uses Oxford Nanopore sequncing method) does it for Rijo-Ferreira lab.

### Sequencing methods
#### Oxford Nanopore
Third generation of sequencing.


#### Illumina
- parallelized, can transcribe billions of strands
- used a paired-end strands

>[!SUMMARY]
>**Sequencing by synthesis**
>Sequencing by synthesis ([SBS](https://www.illumina.com/science/technology/next-generation-sequencing/sequencing-technology.html)) is a next generations sequencing (NGS).
>Idea: track the addition of labeled nucleotides as the DNA chain is copied.

1. First, we add adapters to the ends of the DNA as part of *sample prep*. Can also add more modification for reduced cycle amplification (e.g. sequencing bind site, indices and regions complementary to flow cell oligos).
2. Secondly, we do *cluster generation*: each fragment molecule is isothermally amplified. The **flow cell** is a glass slide with lanes. Each lane is a channel coated with a lawn, composed of **two types of oligos**. 
3. The strand that attaches to the oligo is the *forward* strand. Then, the reverse strand gets made, and the forward strand gets washed away. The library is bound to the flow cell.
4. Using PCR, we do **bridge amplification** of that strand to populate a huge cluster. We wash everything away leaving only forward strands.
5. Then, **sequencing primers** bind to the forward strands. (We add primers to be able to elongate DNA strands and amplify those.)
	![[Pasted image 20250629155837.png | center | 300]]
6. Fluorescent nucleotides are added to the strands, along with DNA polymerase. 
	- In each sequencing cycle, a mix of modified nucleotides (A, T, C, G) is added. These nucleotides have:
		- fluorescent tag: each type of base (A, T, C, G) is labeled with its own colored fluorophore (a molecule that absorbs light energy and re-emits it as a fluorescence)
		- terminator: ensure only one nucleotide can be added to the DNA strand at a time.
	- The attached base is naturally picked.
7. After addition of one abuse, the sequencer takes an image. The cameras detect the specific fluorescent color emitted from each cluster, identifying the added base.
8. Then, a chemical cleavage (breaking a particular chemical bond) step removes the fluorescent dye and the reversible terminator, allowing the next nucleotide to be added in the subsequent cycle.
9. Single end ends here, but we do similar cycles for paired end after making reverse strands and washing away forward strands. Need **Unique Dual Indexes** (384 samples/flowcells). 
10. This cycle of adding a single base, imaging, and cleaving is repeated millions of times (e.g. 100-300 cycles), building up the whole DNA sequence.
11. We filter and map by demultiplexing.
12. Then, we compare to reference genome. We want to know **average read depth** (how often that same nucleotide appears; WGS: 30x, cancer rare mutations: 1500x) and **coverage** (ARD of a specific region of DNA).


[Really cool video describing whole process](https://www.youtube.com/watch?v=fCd6B5HRaZ8)
[Another, more in-depth explanation](https://youtu.be/WKAUtJQ69n8?si=A9RYgkUxjHB32c-6)

>[!NOTE]
>**Primers vs adapters**
>Primers bind to DNA/RNA to serve as a starting point for DNA polymerase (an enzyme) to begin synthesizing a new DNA strand.
>Adapters are added to the ends of DNA fragments during library preparation for HTS to enable sequencing process itself. They help clusters to stay isolated from each other and bind to the flow cell.
>Both are synthetic.

#### Sanger chain-termination (old and slow)
N/A
- outdated and slow, one strand
- it took 32 years to transcribe a human genome


>[!NOTE]
>**Paired-end and single-read sequencing**
>Paired-end sequencing facilitates detection of genomic rearrangements and repetitive sequence elements (also, gene fusions and novel transcripts). `_1` is forward, `_2` is reverse direction
>- easier to detect insertion-deletion (indel) variants 


#### Sequencing errors profiles
In "Per base sequence quality", it is not unexpected to see a drop in quality towards end of reads for Illumina.
For Illumina, the quality of nucleotide base calls are related to the **signal intensity and purity of the fluorescent signal**. Low intensity fluorescence or the presence of multiple different fluorescent signals can lead to a drop in the quality score assigned to the nucleotide. 

##### Expected
As sequencing progresses from the first cycle to the last cycle, we often anticipate a drop in the quality of the base calls.
- **Signal decay:** as sequencing proceeds, the fluorescent signal intensity decays with each cycle, yielding decreasing quality scores at the 3' end of the read, due to
	- degrading fluorophores
	- a proportion of the strands in the cluster not being <u>elongated</u>
- **Phasing:** as the number of cycles increase, the signal starts to blur as the cluster loses synchronicity (some strands fail behind). Yields decrease in quality scores at the 3' end of the read
##### Worrisome
- **Overclustering:** sequencing facilities can overcluster the flow cells, which results in small distances between clusters and an overlap in the signals
	- can be interpreted as a single cluster, generating lower score reads across the *entire read*
- **Instrumentation breakdown:** any sudden drop in quality or a large percentage of low quality reads across the read could indicate this


