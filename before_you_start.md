**Before you start sequencing**

In our experience, there is a lot to be gained from spending a bit of time on clarifying your goals. Why do you want to do metagenomic sequencing? What are you hoping to achieve? Your sample collection, preparation and sequencing strategy should be aligned to your goals, to maximize your chances of success. 

Here, we outline some points which we have learned are important to consider.

**What is your research question?**

A common pitfall in metagenomics is to send off your samples without a clear plan. If you reached the point where you want to do metagenomic sequencing, there is a reason for it. Writing down specific aims may help clarify if your dreams are of the wild kind, or actually achievable.

Here, we list a few common scenarios where metagenomics can be applied, and some of the points you will need to consider. 

_**Case 1** "Working with complex environmental samples"._

_Many natural environments are naturally super complex. Therefore, the first question you need to clarify would be whether its important to get a generel overview of the composition of sample, or if you are actually just interested in a specific component of the sample. If you simply sequence everything (in the hope of looking at everything), you will only find the most abundant members of the community targeted._ 

_An example of a complex environment that is currently of high interest for pathogen surveillance is wastewater. Wastewater samples can be used for many different types of surveillance, but most of the attractive targets are present at low relative abundance. For example, if your interest in wastewater is for surveillance of a specific type of AMR genes, you should consider enriching for them during sample preparation. Do you dream of linking AMR genes to their hosts? Well, thats a unfortunately a very tall order, since AMR genes are often mobile. Long-read sequencing would be very helpful for such a goal, but you will need to explore whether you can get sufficient depth (maybe combine with an enrichment strategy?), and the sample must be handled very gently (to avoid fragmentation, otherwise you will still only get short reads). Do you need to be quantitative about your results? Likewise a challenging goal, but you might consider using spike-ins or mock communities to that end. At any rate, make sure to take very detailed measurements during sample collection._

_If you simply want to explore a new environment, thats of course fine too. Just remember that for complex samples, we only see the dominant members._

_**Case 2** Sequencing the genomes of the uncultured majority._

_Lots of bacteria are really hard to culture, others grow very slowly. Metagenomics has been successfully applied in such cases, but the success is highly dependent on sampling collection and sequencing strategy. Unfortunately, we dont have publications for all failed attempts, but anybody working with metagenomics on a regular basis will have experience with failed attempts!._

_MAGs ("metagenome-assembled genomes") can be generated directly from environmental samples, and they have provided important new insights to the microbial dark matter out there. There are many excellent tools available, which we will not attempt to list here. However, if you are used to work with assemblies from cultured isolates, there are a couple of things to be aware of. MAGs differ from regular genomes in several ways. First, note that MAGs are not complete genomes (regardless of what checkM says!). In general, you should assume that a MAG contains the core genes of the bacterium, but not the accessory genes. This is because genes that are variably present within and across samples are nearly impossible to bin. Second, note that MAGs are typically a kind of "consensus" genome, where data from multiple bacterial strains have been co-assembled. Keep in mind that it is not an isolate, but the genome is likely derived from a mix of strains (depending on the strain-level diversity in your sample(s)_

_Sometimes, a sample of an uncultured bacterium can be obtained from an environment with low complexity. For example, a bacterial infection may be caused by a single isolate that spreads rapidly in an environment normally devoid of bacteria. If your sample comes from an infection, your main problem is likely to be the host DNA. If the host is a human, there are a lot of kits and protocols available. They tend to sound better in the brochure than in real life, but they do work (at least sometimes). On the other hand, if you are able to obtain a relatively pure sample of your target organism, but in low quantity, it is possible to amplify the sample before sequencing._

**Experimental design**

Thinking about how to conduct your experiment is of course not special for metagenomics, but there are perhaps some specific sources of bias and confounders that should pay extra attention to.

Start by minimizing technical and procedural sources of bias at the design stage:
- Randomize samples across preparation (extraction/library) batches and sequencing runs.
- Use blocking so each analytical batch contains a balanced mix of study groups (e.g., case/control).
- Keep detailed, structured metadata for kit lot, operator, run ID, and any deviations from SOPs.
- When repeated measures exist (e.g., multiple sites per subject or longitudinal timepoints), distribute then across different preparation and sequencing batches.

Control for confounding sample properties:
- Baseline subject characteristics (e.g., oral metagenomes, where age, diet, oral hygeine, and periodontitis severity are influential)
- Sampling environment (e.g., seasonality and geography)

Perfectly matched cohorts are rare in practice, so prioritize (1) documenting these variables with standardized methods, (2) reducing extreme imbalance at enrollment or sampling (simple stratification or frequency matching), and (3) including key variables as covariates in the statistical analysis. 

**Controls and contamination**

Metagenomics, especailly low biomass sample, is untargeted and therefore highly sensitive to contamination. You can assume some level of background DNA will be introduced from your reagents often called the “kitome”, a characteristic set of bacterial sequences commonly originating from DNA extraction or library prep kits (e.g., Ralstonia, Burkholderia, Sphingomonas). Contiminants can also be introduced from laboratory environments. The only way to distinguish real biology from contiminant noise is to include controls:

-	Negative controls (field blanks, extraction blanks, library blanks) help you identify contaminants.
-	Positive controls (mock communities, spike-ins) let you measure sensitivity, abundance bias, and quantification accuracy.
-	Replicates strengthen your conclusions and allow you to gauge technical variation. 

If you are doing metagenomics for diagnostic or surveillance purposes, controls are critically important - and missing them cannot be fixed afterwards.

**Sample collection**

Reproducibility begins with a SOP covering who collects, where, when, and how. 

For clinical collections, specify anatomical site, swabbing strokes, pre-collection restrictions (e.g., fasting, no tooth brushing/rinsing), and time-of-collection.
For environmental sampling, define surface area, contact time, and aspectic handling.
Immediately stabilize samples with a validated stabilization buffer or store at -80 °C as soon as possible to preserve the metagenomes at the time of collection.

**Sample preparation**

This is a step which in our opinion is highly underestimated. Your protocol for sample preparation should be aligned to your research question (which should therefore be as precise as possible).

Metagenomic samples have a major advantage over amplicon sequencing approaches (i.e. PCR targeting the 16S rRNA gene), which are always biased by the primers. If your goal is to obtain an unbiased estimate of the composition of an environmental sample, you should make sure to choose a DNA extraction strategy that introduces minimal bias. Choose extraction chemistries that achieve broad lysis (mechanical bead beating plus enzymatic/chemical steps) so gram-positive bacteria, fungi, and encysted forms are not under-presented. If you want quantitative data, you should also minimize manipulations and record exact volumes or weights. Spike-ins are useful for transforming relative read counts into absolute abundance estimates.

For low biomass or host-rich clinical samples, or if you have a specific target in mind, you may need enrichment or depletion steps (host DNA removal -e.g., selective lysis, methyl-binding, or hybrid capture-, rRNA depletion) to increase microbial read yield of your target. 

If working with viruses (which can be RNA and DNA), you have to make sure you reverse transcribe RNA and synthesize double-stranded DNA before sequencing (unless you are only interested in RNA viruses in which case you can consider doing RNA-seq). 

Keep extraction kit lots consistent within a study where possible; if a lot change is unavoidable, distribute groups across lots.

**Sequencing strategy**

Your sequencing choice depends on your goals. Illumina short reads are ideal for accurate taxonomic surveys and gene profiling; long reads (Oxford Nanopore, PacBio) are useful for resolving genomes, plasmid/AMR context, and viral populations. 

You should also think about sequencing depth: do you need shallow coverage to survey broad community shifts, or deep coverage to assemble novel genomes? This will later influence which databases and search methods you rely on. Regardless of platform, plan pilot runs to assess depth vs. diversity saturation and verify that negtaive controls remain low and distinct from biological samples.

**Downstream analysis planning**

Even before sequencing, it is wise to think about the databases and tools you will use. K-mer based tools (Kraken2, Kaiju, Centrifuge, custom databases) are fast and efficient for initial classification against nucleotide databases. However, when reads or contigs cannot be classified, sensitive protein-level searches (DIAMOND, MMseqs2) against comprehensive protein databases (NR, UniRef, eggNOG, KEGG, custom databases) can reveal more distant relationships. BLAST is also critical in resolving conflicting classifications. Combining these approaches makes sense when you want both speed and sensitivity: use k-mer classifiers for the first pass, protein alignment tools for unclassified or novel sequences and BLAST for confirmation.

**Practical considerations**
Finally, consider the logistics:
-	Ethics and permits (Nagoya protocol, animal/human approvals, biosafety).
-	Metadata (sample IDs, time, location, host, storage conditions).
-	Compute requirements (disk space, CPU/RAM, workflow management with Nextflow or Snakemake).
-	Data sharing (SRA/ENA submission, naming conventions, README files).
-	Contingency planning (what if yields are low, host DNA dominates, or contamination is high?).

