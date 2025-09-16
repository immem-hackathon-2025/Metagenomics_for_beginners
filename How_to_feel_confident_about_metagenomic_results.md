# Feeling confident about your pathogen identification

So, you got a result, thats a great! Maybe you found an interesting pathogen in your sample? Perhaps an unexpected one? But how do you know if its real? Here, we will outline some of the strategies you can employ to feel more confident (yes, even with metagenomic data!), and some cases where you need to be cautious.

## Could your pathogen be a contaminant?

If you are working with clinical samples, you need to consider this question very carefully. Now is the time to use those controls that you included when you did your sequencing.

Knowledge of the pathogen identified is also important. How (un)likely is it that you should find this particular pathogen? 

## Can you trust your database?

There are loads of databases containing taxonomic information. Some of them are very comprehensive, but also very noisy. Others are much smaller, but more curated. Contamination can also be on the database side!

If your initial hit came from one of those large and not very curated databases, you should start by checking against a different database.

## Which tool did you use to get your result?

Several very popular tools for metagenomics are based on kmer-based classification or read-mapping. These tools have the advantage of being super efficient in dealing with large datasets, and you get to skip the resource-consuming (and challenging) step of metagenome assembly. But working with reads (and particularly short reads) also means some of the reads get classified/mapped wrongly. For example, bacterial genomes contain regions with low complexity, where reads may map (or partially map) even though they are unrelated to the genome they hit. Depending on the database you used, some of the genomes in there may be contaminated, or include small nonsense contigs, which your reads may end up aligning to. So if you found a pathogen using this type of tool, you need to follow-up with some additional analysis.

Is there a good reference genome for the pathogen you found? Then your first follow up should be to download it and map your reads to it. Second, you will want to look at how the reads distribute across the genome, and with what level of sequence identity. 






