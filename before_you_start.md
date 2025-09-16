**Before you start sequencing**

In our experience, there is a lot to be gained from spending a bit of time on clarifying your goals. Why do you want to do metagenomic sequencing? What are you hoping to achieve? Your sample collection, preparation and sequencing strategy should be aligned to your goals, to maximize your chances of success. 

Here, we outline some points which we have learned are important to consider.

**What is your research question?**

A common pitfall in metagenomics is to send off your samples without a clear plan. If you reached the point where you want to do metagenomic sequencing, there is a reason for it. Writing down specific aims may help clarify if your dreams are of the wild kind, or actually achievable.

Case 1 "We want to do AMR surveillance in wastewater". 
There has been a lot of studies doing shotgun metagenomics on wastewater, and one things is very clear: its an incredibly complex matrix. If you simply sequence everything, chances are you will only detect a few highly abundant AMRs, while most of your data will be something else. Are you interested in monitoring changes in particular resistance genes, linking genes to hosts, or discovering new variants? The answers to these questions will inform your sampling strategy, sequencing strategy and later, the choice of analytical tools.  

**Experimental design**

How many samples will you need and across what time points or environments? Consider biological replicates, technical replicates and potential confounders such as seasonality, diet, geography or sample matrix/composition. Proper design here reduces the risk of ambiguous downstream results. This is not specific to metagenomics, but just a general reminder.

**Controls and contamination**

Metagenomics is untargeted and therefore highly sensitive to contamination. You can assume some level of background DNA will be introduced from your reagents often called the “kitome”, a characteristic set of bacterial sequences commonly originating from DNA extraction or library prep kits (e.g., Ralstonia, Burkholderia, Sphingomonas). The only way to distinguish real biology from kitome noise is to include controls:
-	Negative controls (field blanks, extraction blanks, library blanks) help you identify contaminants.
-	Positive controls (mock communities, spike-ins) let you measure sensitivity, abundance bias, and quantification accuracy.
-	Replicates strengthen your conclusions and allow you to gauge technical variation. 
If you are doing metagenomics for diagnostic or surveillance purposes, controls are quite important and missing them cannot be fixed afterwards.

**Sample preparation**

This is a step which in our opinion is highly underestimated. If you have a specific target you may need enrichment or depletion steps (host DNA removal, rRNA depletion). On the other hand, if you want quantitative data, you should minimize manipulations and record exact volumes or weights. Spike-ins are useful for transforming relative read counts into absolute abundance estimates. If working with viruses (which can be RNA and DNA), you have to make sure you reverse transcribe RNA and synthesize double-stranded DNA before sequencing (unless you are only interested in RNA viruses in which case you can consider doing RNA-seq). 

**Sequencing strategy**
Your sequencing choice depends on your goals. Illumina short reads are ideal for accurate taxonomic surveys and gene profiling; long reads (Oxford Nanopore, PacBio) are useful for resolving genomes, plasmids, and viral populations. You should also think about sequencing depth: do you need shallow coverage to survey broad community shifts, or deep coverage to assemble novel genomes? This will later influence which databases and search methods you rely on.

**Downstream analysis planning**
Even before sequencing, it is wise to think about the databases and tools you will use. K-mer based tools (Kraken2, Kaiju, Centrifuge, custom databases) are fast and efficient for initial classification against nucleotide databases. However, when reads or contigs cannot be classified, sensitive protein-level searches (DIAMOND, MMseqs2) against comprehensive protein databases (NR, UniRef, eggNOG, KEGG, custom databases) can reveal more distant relationships. BLAST is also critical in resolving conflicting classifications. Combining these approaches makes sense when you want both speed and sensitivity: use k-mer classifiers for the first pass, protein alignment tools for unclassified or novel sequences and BLAST for confirmation.

**Practical considerations**
Finally, consider the logistics:
-	Ethics and permits (Nagoya protocol, animal/human approvals, biosafety).
-	Metadata (sample IDs, time, location, host, storage conditions).
-	Compute requirements (disk space, CPU/RAM, workflow management with Nextflow or Snakemake).
-	Data sharing (SRA/ENA submission, naming conventions, README files).
-	Contingency planning (what if yields are low, host DNA dominates, or contamination is high?).

