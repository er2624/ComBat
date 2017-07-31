Applying ComBat algorithm in Python

Key Reads/References

The original paper:

Johnson WE, Rabinovic A, Li C (2007). Adjusting batch effects in microarray
expression data using Empirical Bayes methods. Biostatistics 8:118-127.  

PMC article:

Jeffrey T. Leek, W. Evan Johnson, Hilary S. Parker, Andrew E. Jaffe
and John D. Storey (). sva: Surrogate Variable Analysis. R package
version 3.4.0.

"User Manual" link to latest version:

http://bioconductor.org/packages/release/bioc/vignettes/sva/inst/doc/sva.pdf

The actual R code:

https://github.com/jtleek/sva-devel/blob/master/R/ComBat.R

Link to original translation from R into Python expanded upon here:

https://github.com/brentp/combat.py

Description:

Directly from the description in the original R code, "ComBat allows users to adjust for batch effects in datasets where the batch covariate is known, using methodology described in Johnson et al. 2007. It uses either parametric or non-parametric empirical Bayes frameworks for adjusting data for batch effects. Users are returned an expression matrix that has been corrected for batch effects. The input data are assumed to be cleaned and normalized before batch effect removal." 

In brief, if samples can be identified as having come from a particular batch, and the user is interested in teasing out information across a collective pool of batches, it is possible to remove confounded, non biologically or experimentally relevant information from the samples while simultaneously preserving at least some biological and experimentally relevant truth (as asssessed by both quantitiative, statistical methods - e.g., spearman correlation, etc - and qualitative analytical methods, such as clustering of data in MDS). 

Python Code Presented Here:

The latest version of the R code contains both a feature to normalize batches with respect to location (mean) only and an option to set one batch as reference, normalzing all other batches to that reference batch while the reference batch itself remains unchanged.

As described in the "User Manual" link, these features can be crucial: when comparing, for example, multiple data sets that came from various cell types cultured under different growth conditions (some with serum, some without, some as neurospheres, some as immortalized cells, etc), it would not be expected that the variance across, say, cells derived from a brain tissue sample would be the same as the variance across cells derived from a skin tissue sample - although two different brain tissue sample sets would be expected to be more similar to each other then either one of them to a skin tissue sample. 

Additionally, if the purpose of batch normalization is to use the adjusted data for machine learning, it would likely enchance predictive accuracy if the data sets the algorithm is to be applied to have been normalized to the data set the algorithm was taught on - which is precisely what the reference batch normalization feature does.

Using a translation of the ComBat function developed by brentp

