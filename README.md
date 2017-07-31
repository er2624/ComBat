Applying ComBat algorithm in Python

Key Reads/References:

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


Directly from the description in the original R code, "ComBat allows users to adjust for batch effects in datasets where the batch covariate is known, using methodology described in Johnson et al. 2007. It uses either parametric or non-parametric empirical Bayes frameworks for adjusting data for batch effects. Users are returned an expression matrix that has been corrected for batch effects. The input data are assumed to be cleaned and normalized before batch effect removal."

