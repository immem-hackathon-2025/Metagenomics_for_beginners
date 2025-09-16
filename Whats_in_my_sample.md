# Whats in my sample?

There are thousands of questions you may ask, where metagenomics could be of interest. One of the most basic ones is perhaps "whats in my sample?" Here, we will outline some strategies for how you can go about that questions, and some of the tools out there which can help you find some answers. We will of course also mention some common pitfalls, and situations where you need to be cautious.

## Before you start analysing: QC check the raw data!

Did the sequencing work as intended? How much data did you get, and whats the quality of it? The quality (and amount) of data you get from your sequencing matters a lot for what you can do with your data in terms of analysis. Sometimes, everything is great, other times you may need to trim your data.

## Getting a first overview

Starting out, it can be very helpful to just get a rough overview of your samples. Is it all human DNA? All E.coli? Maybe there is a specific type organism you are interested, does it look like it might be in there?

At this stage, you are really just getting to know your data. Therefore, simple and fast analysis is good. A very good tool to start with is kraken (link).

- there are different databases for kraken. Some are very large, some only include certain types of taxa. Select the appropriate one.

## De novo assembly (or not)

Doing metagenomics is often about digging into the unknown. We want to discover new things. In that sense, de novo assembly is attractive. 

But, you need to have coverage, quite a lot actually. Furthermore, strain-level diversity can put obstacles in your way.

## Leaning on a database

Can be a very powerful way to gain insights into your data. There are so many databases out there, that it can be quite daunting.

## Making your own database

## So you found a possible suspect (for whats in your sample). But can you trust it?

Depends a lot on the database you are using. Once you have a suspect, there are some things you can do to feel more confident about your result.

- If you used a noisy database, try a more specific one containing your suspect.
- Is there a reference genome out there? Map your reads to it. Percentage identity? Horizontal coverage? Are there other things it could also be (perhaps you wanna do competitive mapping)?
