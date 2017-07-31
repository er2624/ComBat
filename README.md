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

As a final feature, if other catagories exist for the data (e.g., "age" or "status of the cancer" are the two used in the examples presented within bladderbatch data), these can also be used as covariates to normalize the data.

*NOTE: The R version provides an option to run a non-parametric version of ComBat. The Python code presented here lacks this option.

The Python code presented here is essentially the same code originally presented in the brentp link, with two new bells and whistles: ref_batch designation and mean_only option. These were added on by simply going through the linked original R code, and translating the effect of the data manipulations into R. Resulting values in Python differ from those obtained in R by no more than 1e(-5). 

The code itself is under GBM_Project_Notebooks, including two worked examples using data compiled from 7 different databanks - 6 brain tissue specific and 1 skin. To compare the results of this code to both the brentp and original R codes, the Worked_Examples section contains several applications of this code to the popular bladderbatch data set (the exact same data provided in the brentp link) under varying settings (e.g., mean_only = True, identifying numerical covariates, etc).

The code by itself is presented from Jupyter Notebook and is heavily annotated so that, if desired, each of the functions running within ComBat and the lines performing the calculations within ComBat itself can be directly lined up with the equations present in the 2007 Johnson et al. paper - e.g., the delta_star hyperparameters are explicitely identified, etc.

The code in the examples has these annotations removed, and the bladderbatch examples specifically detail what a model matrix must look like if using to identify covariates in addition to the actual batches themselves.
