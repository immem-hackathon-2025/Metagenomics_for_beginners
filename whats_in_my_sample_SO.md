**General worflows**

***1. QC & Trimming***

1.1. Fastq quality overview 

1.2. Adapter and quality trimming

***2. Host & rRNA D***

2.1. Align reads to the host reference sequence (hg38): bowtie2 or any other sensitive aligners

2.2. Align reads to the rRNA database: sortmerna, etc


***3. Exploring taxonomic composition***

3.1. Classification of reads
- Species-specific sequence-based: metaphlan4
- Kmer pattern-based: kraken2, centrifuge

3.2.	Abundance estimation at specific taxon level + resolving unidentified taxa (species obviously)
- Bayesian estimation: Braken

***4.	MAG Assembly***

4.1.	De novo assembly: megahit, metavelvet

4.2. Filter low-quality contigs
- QC: CheckM
- Calculate read depth: bowtie2+samtools

4.3. Bin contigs to MAGs
- Binning by contig abundance or/and GC%, tetranucleotide frequencies: Metabat2

4.4. ilter low-quality MAGs
- QC: completeness, contamination, and rRNA/tRNA prediction
- Dereplication

4.5. Gene annotation & Functional profiling
- ORF prediction: prodigal
- Align ORFs to database (Uniref90, KEGG...): MMseqs2, DIAMOND
4.6. Taxonomic classification of MAGs
- Align MAGs with taxonomy database:
  - Phylogenetic placement + ANI: GTDB-tk
 
***5.	Choice of taxonomy database***

-	NCBI: submission, user-defined names prioritized, many species names are not following the LPSN standards
-	GTDB: ANI-based species-level clusters, represented and named after the type strain
-	Metaphlan db: primarily GTDB compatible
-	Kraken2 db: NCBI compatible

Discrepencies between databases: same isolate genomes are classified to different names due to different annotation methods.
  - i. Case: No Shigella spp. in GTDB since they are treated as heterotypic synonyms of E. coli.
So you should know the details about your database

**Low biomass samples**

Besides the enrichment at the sample preparation step, host read removal of low biomass samples significantly decreases the amount of reads remaining for the downstream analysis. Thus, MAG assembly sometimes cannot be the case to find what is in the sample. 
In that case, we propose sticking to the taxonomic composition estimated by the assembly-free methods, probably kmer-base methods. 
But add the additional decontamination steps to rule out the false-positive species. It could be done in multiple ways:
- Negative controls (blanks)
- Other sample data, processed with exact same laboratory experiments, but expected to have the distinct composition (e.g., tissue vs. blood)
