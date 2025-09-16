**General worflows**

***1. QC & Trimming***

1.1. Fastq quality overview 

1.2. Adapter and quality trimming

***2. Host & rRNA Depletion***

2.1. Host DNA removal

Map against a comprehensive host reference (e.g., hg38 with alternate/decoy contigs) using a sensitive preset (e.g., Bowtie2, minimap2), then discard mapped pairs to reduce host carryover. Record the host-mapping rate per sample, and confirm that host depletion did not inadvertently correlate with case/control status (i.e., avoid confounding).

2.2. rRNA removal

For DNA metagenomics, this step (e.g., SortMeRNA, barrnap) is optional; apply only if rRNA reads are disproportionately abundant or hinder specific downstream steps (e.g., assembly), and document the impact on retained depth.

***3. Exploring Taxonomic Composition***

3.1 Read-level classification

- Marker-based (MetaPhlAn4): High precision via clade-specific markers; robust to contamination; coverage limited to marker catalog.
- k-mer–based (Kraken2/Centrifuge): Very sensitive and fast; relies on reference index composition and LCA/weighted assignment. Pair with confidence thresholds to reduce over-assignment, and ensure the reference index (and taxonomy map) is version-locked.
  
3.2 Abundance re-estimation & unresolved taxa

Apply a Bayesian/EM-based abundance re-estimation tools (e.g., Bracken) to adjust k-mer assignments and improve species quantification.

***4.	MAG Assembly***

4.1 De novo assembly

Assemble quality-filtered, host-depleted reads with a metagenome assembler (e.g., MEGAHIT, MetaVelvet if you require Velvet-based workflows). For complex communities, consider co-assembly or sample-wise assemblies plus cross-mapping; capture N50/L50/total length as baseline QC.

4.2 Contig filtering & coverage calculation

Filter very short/low-coverage contigs. Map reads back with a aligner (e.g., Bowtie2, minimap2) and compute coverage (e.g., samtools). Use a genome quality assessor (e.g., CheckM/CheckM2) early to gauge completeness/contamination trends. Remove very short contigs (commonly <1–2.5 kb for binning) and low-coverage. 

4.3. Binning

Bin contigs by coverage, GC%, and tetranucleotide features with a binner (e.g., MetaBAT2); optionally run multiple binners (e.g., MaxBin2) and reconcile with an ensemble tool. Preserve parameters and contig lists per bin.

4.4. MAG QC, filtering, and dereplication

Apply MIMAG criteria: prefer ≥90% completeness and ≤5% contamination for “high-quality”; for near-complete MAGs, presence of 23S/16S/5S rRNAs and ≥18 tRNAs strengthens credibility. Remove low-quality or redundant bins and dereplicate with dRep (e.g., 99% ANI) to produce a non-redundant MAG set.

4.5. Gene annotation & Functional profiling

Call ORFs with gene predictor (e.g., Prodigal in meta mode) and annotate against curated references (UniRef90, KEGG Orthology, eggNOG) using fast aligner (e.g., MMseqs2 or DIAMOND). Summarize at gene-family and pathway levels (e.g., KEGG modules, MetaCyc) and retain per-MAG gene catalogs for downstream comparative genomics.

4.6. Taxonomic classification of MAGs

Classify MAGs with a genome taxonomy tool (e.g., GTDB-Tk), which uses marker phylogeny and ANI to representatives/type strains. Save both the GTDB labels and any legacy/NCBI labels to simplify cross-database comparisons.

***5.	Choice of Taxonomy Database***

Databases disagree:

Taxonomy can be name-centric (governed by formal nomenclature and type strains) or genome-centric (driven by whole-genome relatedness thresholds and normalized ranks). Different design goals lead to different boundaries and names.

- NCBI Taxonomy (name-centric, literature-driven): Curated from the literature and community submissions. Names aim to reflect the ICNP code and LPSN. Synonyms, provisional taxa, and user submissions coexist, so historical/clinical names are well represented, even if boundaries are uneven in genome space.
  - Strengths: Ubiquitous, essential for submissions and clinical interoperability.
  - Caveats: Polyphyly or paraphyly can persist; some names lag modern genome evidence.

- GTDB (genome-centric, phylogenomically normalized ranks): Builds concatenated marker alignments (e.g., bac120 for Bacteria, ar122 for Archaea) to infer a genome-wide phylogeny. Uses relative evolutionary divergence to normalize ranks above species so that rank boundaries are consistent along the tree. Define species primarily by ANI to type strains or selected representatives (~95% ANI).
  - Strengths: Consistent, reproducible genome-based boundaries; powered for MAGs and comparative genomics.
  - Caveats: Names may differ from clinical/legacy usage (e.g., Shigella merged within E. coli as heterotypic synonyms; Clostridium sensu lato split).

- MetaPhlAn database (marker-centric, SGB-aware): Curate clade-specific marker genes from high-quality isolate genomes and MAGs; leverage species-level genome bins (SGBs) that cluster genomes and each clade is represented by markers with high specificity. Where possible, SGBs are mapped to GTDB/NCBI names; unresolved SGBs retain placeholder labels.
  - Strengths: High precision at read-level without assembly; resilient to low-level contamination.
  - Caveats: Limited to taxa with curated markers.

- Kraken2/Centrifuge databases (k-mer/FM-index, build-time choices matter): Build the DB by selecting reference genomes (often NCBI RefSeq/GenBank). Kraken2 uses exact k-mers and assigns reads by LCA over taxa hit by those k-mers; The taxonomy they attach to is typically NCBI Taxonomy from the build date.
  - Strengths: Broad coverage, fast classification; easy to customize (include/exclude genomes, add MAGs).
  - Caveats: Results are only as good as the DB you built (contaminated or mislabeled genomes propagate errors). Version-lock the FASTA set and taxonomy.

- Practical reconciliation & policy
  - Pick a primary taxonomy per analysis tier (e.g., GTDB for MAGs; NCBI for clinical reporting).
  - Maintain a synonym/crosswalk table (GTDB name, NCBI scientific name, LPSN status, known synonyms).
  - Document DB release/version and build recipes (date, genome sources, filters).

**Low Biomass Samples**

Besides enrichment strategies at sample preparation, host read removal in low-biomass samples can leave too few microbial reads for reliable assembly; in such cases, assembly-free taxonomic profiling (often k-mer–based with re-estimation) is the pragmatic choice. AND strengthen validity by adding explicit decontamination steps to rule out false positives:

- Negative controls (extraction/library blanks) sequenced in the same batches; remove taxa enriched in blanks (scaled to DNA conc/read depth).
- Counterfactual sample types processed with the same wet-lab environment (e.g., tissue vs blood) to flag kit/environment signatures.
- Prevalence/abundance filters (e.g., taxa present mainly in low-biomass samples and in blanks) plus breadth-of-coverage checks against suspicious species’ references (true positives show broad, even coverage; contaminants show sparse spikes).
