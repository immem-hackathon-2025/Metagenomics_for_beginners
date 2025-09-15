# Thoughts on metagenomic analysis on wastewater samples

## Why wastewater? 
Wastewater is of increasing interest for pathogen surveillance. In many places, surveillance using fx qPCR is already implemented (fx. SARS-CoV-2, influenza). Another target is to look for AMR. 

Wastewater is attractive as a target, because samples can be collected without involving humans directly. If correctly collected it can also be unbiased, i.e. a representative sample of the human population targeted.

## Challenges with wastewater

The main challenge working with wastewater is the extreme complexity of the samples. From a pathogen surveillance perspective, we may be primarily interested in fecal matter from humans - which is in itself a complicated community, even if taken from a single human - in this case, it is pooled from as potentially very large pool of people. Furthermore, there are lots of other things in wastewater.

### Working with metagenomic sample with a very complex composition

- de novo assembly is difficult or perhaps even impossible. As a rule of thumb, you probably need something like 20x coverage to assembly anything. If you have strain-level diversity in the sample (and that is very likely with wastewater from humans), your data may not assemble, or assemble into some kind of hybrid genome
- Using a reference database can be a powerful way to increase sensitivity. But it raises challenges in terms of the quality of the database. And obviously, you cannot find anything not in the database.
- AMR is particularly challenging in this case, because genes are frequently passed around horizontally. Linking an AMR gene to its host is not trivial.

### What can we do?

- Specify your research question: why do you want to do metagenomics on wastewater (specifically)?
- It there a specific type of bacteria or viruses you are interested in? Fx a specific species?
- Which possibilities are there for enriching for your target?
- Are there parts of the sample you are definitely not interested in, which we could try to remove before sequencing?
- Is your analysis exploratory or targeted?
- Do you need to be quantitative?

### When can you be confident about a result?

#### Is species X in the sample or not? 

- It is very hard (if not impossible) to conclude that something is NOT in a sample. You may be able to put up some ballpark estimates of whether you think you would have a chance of seeing species x, given the sequencing depth and method of sample preparation. But in generel, you shouldnt use metagenomics for this kind of question.
- If you have data to suggest that species X is in your sample, there are ways to gain confidence in your conclusion.

Do you have a reference genome for your species? Mapping reads to the reference can be very informative, analyse the coverage.





