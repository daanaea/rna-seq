#rna-seq 
[Workshop post](https://hbctraining.github.io/Training-modules/planning_successful_rnaseq/slides/Lib_prep_2019.pdf)

>[!SUMMARY]
>Done in wet lab.
>1. We extract DNA from cells.
>	- Purification column
>	- Centrifuge
>	- How does this work?.. [high-level overview](https://www.youtube.com/watch?v=WKAUtJQ69n8)
>	- DNA and RNA are split, and RNA is reverse-transcribed into DNA
>2. DNA fragmentation is carried out via sonication (very small, fast vibration breaking apart cells enzymatically with catalysts.
>3. ==Adapter sequences== are added to both ends of DNA fragments. They allow the DNA fragments to bind to the **flow cell** (the specialized surface where sequencing reactions occur).
>4. The *library* (a collection of short DNA fragments with adapters) is loaded onto a **flow cell**. Each fragment binds to the flow cell and then undergoes ==bridge amplification==, creating many copies of the same fragment to ensure strong signal.
>	- All copies from same cell carry same **UMI** (Unique Molecular Identifier, a short random DNA). We can group those to remove amplification effect when calculating real expression.
>5. [[Sequencing]] by synthesis is when we read the DNA. ==Sequencing primers== bind to the adapter sequences on the DNA clusters.
>	- In each sequencing cycle, a mix of modified nucleotides (A, T, C, G) is added. These nucleotides have
>		- fluorescent tag: each type of base (A, T, C, G) is labeled with its own colored fluorophore (a molecule that absorbs light energy and re-emits it as a fluorescence)
>		- terminator: ensure only one nucleotide can be added to the DNA strand at a time
>	- After addition of one abuse, the sequencer takes an image. The cameras detect the specific fluorescent color emitted from each cluster, identifying the added base.
>	- Then, a chemical cleavage step removes the fluorescent dye and the reversible terminator, allowing the next nucleotide to be added in the subsequent cycle.
>	- This cycle of adding a single base, imaging, and *cleaving* (breaking a particular chemical bond) is repeated millions of times (e.g. 100-300 cycles), building up the whole DNA sequence.
>
>The images from each cycle are processed to generate raw sequence reads (FASTQ files), which are then aligned to a ==reference genome==.

High quality RNA are needed for mRNA libraries. Degraded samples should only be used to make a "total" RNA-seq library (rRNA removal). 

**RNA enrichment**
- polyA tailed messenger RNA: mRNA-seq
- total RNA (rRNA removed): "total" RNA-seq

**mRNA (polyA) purification** is done via mRNA enrichment: nRMA binds beads coated with oligo dT primer and non-polyadenylated transcripts are washed away.
Transcripts lost in polyA purification:
- Ribosomal/Transfer RNA
- Histone mRNA
- Long-noncoding RNA
- Nascent intron containing transcripts
- Micro RNA
- Degraded RNA
- Many viral transcripts
- Prokaryote/Bacterial transcripts
	- polyA is the degradation signal

If polyA tail is no longer attached to transcript, it results in differential loss of transcripts between samples.

>[!NOTE]
>**PCR (Polymerase Chain Reaction)**
>A lab technique to make millions of copies of a specific DNA fragment.

