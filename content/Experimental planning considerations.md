[Workshop post](https://hbctraining.github.io/Intro-to-rnaseq-hpc-salmon/lessons/experimental_planning_considerations.html)

1. number and type of **replicates**
2. avoiding **confounding**
3. addressing **batch effects**

### Replicates
Experimental replicates can be performed as *technical* replicates or *biological* replicates.
![[Pasted image 20250627144416.png | center | 400]]
Since technical variation is much lower, <u>biological replicates</u> are absolutely essential for differential expression analysis.
[Treating cell line replicates](https://paasp.net/accurate-design-of-in-vitro-experiments-why-does-it-matter/)

The more biological replicates, the better the estimates of biological variation and the more precise estimates of the mean expression levels.

![[Pasted image 20250627144816.png | center | 300]]
	From the figure above, biological replicates (false discovery rate 0.05) are of greater importance than sequencing depth (number of reads).
		Note that higher depth is required for detection of lowly expressed DE genes and for performing isoform-level differential expression.

>[!NOTE]
>**General guide for replicates and sequencing depth**
>- general gene-level differential expression
>	- ENCODE guidelines suggest 30 million SE reads per sample (stranded)
>	- 15 million reads per sample is often sufficient, if there are a good number of replicates (>3)
>	- generally recommended to have read length >= 50 bp
>- gene-level differential expression with detection of lowly-expressed genes
>	- ==similarly benefits from replicates more than sequencing depth==
>	- sequence deeper with at least 30-60 million reads depending on level of expression

### Confounding
A *confounded* RNA-seq experiment is one where you cannot distinguish the separate effects of two different sources of variation in the data.

For example, sex has large effects on gene expression, and if all of our *control* mice were female and all of the *treatment* mice were male, then our treatment effect would be confounded by sex. We could not differentiate the effect of treatment from the effect of sex.

To avoid confounding, ensure animals in each condition are all the same sex, age, litter, and batch, if possible.

### Batch effects
[Negative example of Mouse ENCODE](https://f1000research.com/articles/4-121/v1)

If any of those is no, you have batches:
- Were all RNA isolations performed on the same day?
- Were all library preparations performed on the same day?
- Did the same person perform the RNA isolation/library preparation for all samples?
- Did you use the same reagents for all samples?
- Did you perform the RNA isolation/library preparation in the same location?
