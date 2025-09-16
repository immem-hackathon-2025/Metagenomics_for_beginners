What’s in my sample?
Once your sequencing data is in hand, the next big question is: what is actually in my sample? The answer depends on your research goals, the sequencing strategy you chose, and the databases and tools you prepared beforehand.
First-pass classification
The most common starting point is to use fast k-mer–based classifiers (such as Kraken2, Bracken, Centrifuge, or Kaiju). These tools match your reads against large nucleotide or translated databases and provide a quick overview of which taxa are present and in what proportions. They are efficient, scalable to large datasets, and excellent for getting a first sense of community composition.
However, their accuracy depends heavily on the quality and completeness of the reference database. Sequences from organisms not well represented in the database may remain unclassified or be misclassified.
Going deeper with protein-level searches
For reads or contigs that cannot be confidently assigned, you can turn to protein-based similarity searches. Proteins evolve more slowly than nucleotides, which means a distant organism may still be detectable through conserved proteins even if its genome is absent from your nucleotide database.
Here, DIAMOND (a faster alternative to BLASTx/BLASTp) and MMseqs2 are commonly used. These tools can align your data against comprehensive protein databases such as NR, UniRef, or eggNOG, revealing homology that k-mer methods may miss. This step is particularly valuable if your interest lies in detecting novel viruses, AMR genes, or functional pathways.
Validation and interpretation
When you encounter a surprising or critical finding, it is good practice to validate it with BLAST (blastn, blastx, blastp). Although slower, BLAST provides detailed alignment statistics and is widely recognized as the gold standard. Results from BLAST are easy to interpret and can be presented directly in publications or reports.
Functional insights
Beyond taxonomy, many studies aim to understand the functional potential of the community. Tools like HUMAnN or eggNOG-mapper can link your sequences to pathways, enzymes, and metabolic functions. Specialized databases (e.g., CARD for antimicrobial resistance genes, VFDB for virulence factors) allow you to focus on traits of interest. This connects your research question back to biology — not just who is there, but what can they do.
Contamination awareness
Interpreting “what’s in my sample” always requires caution. Negative controls should be analyzed alongside your real data to identify background signals — the so-called kitome — that arise from DNA in extraction or library kits. Taxa found equally or predominantly in blanks should be treated as probable contaminants. This step cannot be skipped if your study involves low-biomass or diagnostic samples.
Assembly and novelty
Sometimes you will want to go beyond read classification and attempt assembly. By assembling reads into longer contigs or bins, you can reconstruct draft genomes (MAGs) or viral contigs, which can then be quality-checked (e.g., with CheckM or CheckV) and annotated (e.g., with Prokka or DRAM). This approach can reveal entirely new organisms or viral lineages absent from databases. It also enables host–gene linkage, for example connecting an AMR gene to a specific bacterial genome.
Reporting with confidence
Finally, deciding how confident you are in your results is critical. Establish thresholds for the minimum number of reads, relative abundance cut-offs, contig length, and alignment quality before interpreting findings. Report the exact versions of databases and tools you used, and describe the results of your controls. This transparency ensures your work is reproducible and defensible.
________________________________________
Short summary:
•	Start broad with k-mer classifiers for a rapid overview.
•	Use protein-level searches (DIAMOND, MMseqs2) to rescue unclassified reads and detect distant homologies.
•	Confirm key findings with BLAST.
•	Explore function with specialized databases.
•	Guard against contamination by comparing with controls.
•	Assemble when you seek novelty or host–trait linkage.
