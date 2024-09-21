R Notebook
================

``` r
library(dada2)
```

    ## Loading required package: Rcpp

``` r
install.packages("Rcpp")
```

    ## Installing package into '/usr/local/lib/R/site-library'
    ## (as 'lib' is unspecified)

``` r
library(dada2)
packageVersion("dada2")
```

    ## [1] '1.28.0'

``` r
path<- "/home/rstudio/essai/MiSeq_SOP"
list.files(path)
```

    ##  [1] "F3D0_S188_L001_R1_001.fastq"   "F3D0_S188_L001_R2_001.fastq"  
    ##  [3] "F3D1_S189_L001_R1_001.fastq"   "F3D1_S189_L001_R2_001.fastq"  
    ##  [5] "F3D141_S207_L001_R1_001.fastq" "F3D141_S207_L001_R2_001.fastq"
    ##  [7] "F3D142_S208_L001_R1_001.fastq" "F3D142_S208_L001_R2_001.fastq"
    ##  [9] "F3D143_S209_L001_R1_001.fastq" "F3D143_S209_L001_R2_001.fastq"
    ## [11] "F3D144_S210_L001_R1_001.fastq" "F3D144_S210_L001_R2_001.fastq"
    ## [13] "F3D145_S211_L001_R1_001.fastq" "F3D145_S211_L001_R2_001.fastq"
    ## [15] "F3D146_S212_L001_R1_001.fastq" "F3D146_S212_L001_R2_001.fastq"
    ## [17] "F3D147_S213_L001_R1_001.fastq" "F3D147_S213_L001_R2_001.fastq"
    ## [19] "F3D148_S214_L001_R1_001.fastq" "F3D148_S214_L001_R2_001.fastq"
    ## [21] "F3D149_S215_L001_R1_001.fastq" "F3D149_S215_L001_R2_001.fastq"
    ## [23] "F3D150_S216_L001_R1_001.fastq" "F3D150_S216_L001_R2_001.fastq"
    ## [25] "F3D2_S190_L001_R1_001.fastq"   "F3D2_S190_L001_R2_001.fastq"  
    ## [27] "F3D3_S191_L001_R1_001.fastq"   "F3D3_S191_L001_R2_001.fastq"  
    ## [29] "F3D5_S193_L001_R1_001.fastq"   "F3D5_S193_L001_R2_001.fastq"  
    ## [31] "F3D6_S194_L001_R1_001.fastq"   "F3D6_S194_L001_R2_001.fastq"  
    ## [33] "F3D7_S195_L001_R1_001.fastq"   "F3D7_S195_L001_R2_001.fastq"  
    ## [35] "F3D8_S196_L001_R1_001.fastq"   "F3D8_S196_L001_R2_001.fastq"  
    ## [37] "F3D9_S197_L001_R1_001.fastq"   "F3D9_S197_L001_R2_001.fastq"  
    ## [39] "filtered"                      "HMP_MOCK.v35.fasta"           
    ## [41] "Mock_S280_L001_R1_001.fastq"   "Mock_S280_L001_R2_001.fastq"  
    ## [43] "mouse.dpw.metadata"            "mouse.time.design"            
    ## [45] "stability.batch"               "stability.files"

``` r
fnFs <- sort(list.files(path, pattern="_R1_001.fastq", full.names = TRUE))
fnRs <- sort(list.files(path, pattern="_R2_001.fastq", full.names = TRUE))
print(fnFs)
```

    ##  [1] "/home/rstudio/essai/MiSeq_SOP/F3D0_S188_L001_R1_001.fastq"  
    ##  [2] "/home/rstudio/essai/MiSeq_SOP/F3D1_S189_L001_R1_001.fastq"  
    ##  [3] "/home/rstudio/essai/MiSeq_SOP/F3D141_S207_L001_R1_001.fastq"
    ##  [4] "/home/rstudio/essai/MiSeq_SOP/F3D142_S208_L001_R1_001.fastq"
    ##  [5] "/home/rstudio/essai/MiSeq_SOP/F3D143_S209_L001_R1_001.fastq"
    ##  [6] "/home/rstudio/essai/MiSeq_SOP/F3D144_S210_L001_R1_001.fastq"
    ##  [7] "/home/rstudio/essai/MiSeq_SOP/F3D145_S211_L001_R1_001.fastq"
    ##  [8] "/home/rstudio/essai/MiSeq_SOP/F3D146_S212_L001_R1_001.fastq"
    ##  [9] "/home/rstudio/essai/MiSeq_SOP/F3D147_S213_L001_R1_001.fastq"
    ## [10] "/home/rstudio/essai/MiSeq_SOP/F3D148_S214_L001_R1_001.fastq"
    ## [11] "/home/rstudio/essai/MiSeq_SOP/F3D149_S215_L001_R1_001.fastq"
    ## [12] "/home/rstudio/essai/MiSeq_SOP/F3D150_S216_L001_R1_001.fastq"
    ## [13] "/home/rstudio/essai/MiSeq_SOP/F3D2_S190_L001_R1_001.fastq"  
    ## [14] "/home/rstudio/essai/MiSeq_SOP/F3D3_S191_L001_R1_001.fastq"  
    ## [15] "/home/rstudio/essai/MiSeq_SOP/F3D5_S193_L001_R1_001.fastq"  
    ## [16] "/home/rstudio/essai/MiSeq_SOP/F3D6_S194_L001_R1_001.fastq"  
    ## [17] "/home/rstudio/essai/MiSeq_SOP/F3D7_S195_L001_R1_001.fastq"  
    ## [18] "/home/rstudio/essai/MiSeq_SOP/F3D8_S196_L001_R1_001.fastq"  
    ## [19] "/home/rstudio/essai/MiSeq_SOP/F3D9_S197_L001_R1_001.fastq"  
    ## [20] "/home/rstudio/essai/MiSeq_SOP/Mock_S280_L001_R1_001.fastq"

``` r
print(fnRs)
```

    ##  [1] "/home/rstudio/essai/MiSeq_SOP/F3D0_S188_L001_R2_001.fastq"  
    ##  [2] "/home/rstudio/essai/MiSeq_SOP/F3D1_S189_L001_R2_001.fastq"  
    ##  [3] "/home/rstudio/essai/MiSeq_SOP/F3D141_S207_L001_R2_001.fastq"
    ##  [4] "/home/rstudio/essai/MiSeq_SOP/F3D142_S208_L001_R2_001.fastq"
    ##  [5] "/home/rstudio/essai/MiSeq_SOP/F3D143_S209_L001_R2_001.fastq"
    ##  [6] "/home/rstudio/essai/MiSeq_SOP/F3D144_S210_L001_R2_001.fastq"
    ##  [7] "/home/rstudio/essai/MiSeq_SOP/F3D145_S211_L001_R2_001.fastq"
    ##  [8] "/home/rstudio/essai/MiSeq_SOP/F3D146_S212_L001_R2_001.fastq"
    ##  [9] "/home/rstudio/essai/MiSeq_SOP/F3D147_S213_L001_R2_001.fastq"
    ## [10] "/home/rstudio/essai/MiSeq_SOP/F3D148_S214_L001_R2_001.fastq"
    ## [11] "/home/rstudio/essai/MiSeq_SOP/F3D149_S215_L001_R2_001.fastq"
    ## [12] "/home/rstudio/essai/MiSeq_SOP/F3D150_S216_L001_R2_001.fastq"
    ## [13] "/home/rstudio/essai/MiSeq_SOP/F3D2_S190_L001_R2_001.fastq"  
    ## [14] "/home/rstudio/essai/MiSeq_SOP/F3D3_S191_L001_R2_001.fastq"  
    ## [15] "/home/rstudio/essai/MiSeq_SOP/F3D5_S193_L001_R2_001.fastq"  
    ## [16] "/home/rstudio/essai/MiSeq_SOP/F3D6_S194_L001_R2_001.fastq"  
    ## [17] "/home/rstudio/essai/MiSeq_SOP/F3D7_S195_L001_R2_001.fastq"  
    ## [18] "/home/rstudio/essai/MiSeq_SOP/F3D8_S196_L001_R2_001.fastq"  
    ## [19] "/home/rstudio/essai/MiSeq_SOP/F3D9_S197_L001_R2_001.fastq"  
    ## [20] "/home/rstudio/essai/MiSeq_SOP/Mock_S280_L001_R2_001.fastq"

``` r
sample.names <- sapply(strsplit(basename(fnFs), "_"), `[`, 1)
print(sample.names)
```

    ##  [1] "F3D0"   "F3D1"   "F3D141" "F3D142" "F3D143" "F3D144" "F3D145" "F3D146"
    ##  [9] "F3D147" "F3D148" "F3D149" "F3D150" "F3D2"   "F3D3"   "F3D5"   "F3D6"  
    ## [17] "F3D7"   "F3D8"   "F3D9"   "Mock"

``` r
plotQualityProfile(fnFs[1:20])
```

![](essai_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
plotQualityProfile(fnRs[1:20])
```

![](essai_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
filtFs <- file.path(path, "filtered", paste0(sample.names, "_F_filt.fastq.gz"))
filtRs <- file.path(path, "filtered", paste0(sample.names, "_R_filt.fastq.gz"))
names(filtFs) <- sample.names
names(filtRs) <- sample.names
print(filtFs)
```

    ##                                                            F3D0 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D0_F_filt.fastq.gz" 
    ##                                                            F3D1 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D1_F_filt.fastq.gz" 
    ##                                                          F3D141 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D141_F_filt.fastq.gz" 
    ##                                                          F3D142 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D142_F_filt.fastq.gz" 
    ##                                                          F3D143 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D143_F_filt.fastq.gz" 
    ##                                                          F3D144 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D144_F_filt.fastq.gz" 
    ##                                                          F3D145 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D145_F_filt.fastq.gz" 
    ##                                                          F3D146 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D146_F_filt.fastq.gz" 
    ##                                                          F3D147 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D147_F_filt.fastq.gz" 
    ##                                                          F3D148 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D148_F_filt.fastq.gz" 
    ##                                                          F3D149 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D149_F_filt.fastq.gz" 
    ##                                                          F3D150 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D150_F_filt.fastq.gz" 
    ##                                                            F3D2 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D2_F_filt.fastq.gz" 
    ##                                                            F3D3 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D3_F_filt.fastq.gz" 
    ##                                                            F3D5 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D5_F_filt.fastq.gz" 
    ##                                                            F3D6 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D6_F_filt.fastq.gz" 
    ##                                                            F3D7 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D7_F_filt.fastq.gz" 
    ##                                                            F3D8 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D8_F_filt.fastq.gz" 
    ##                                                            F3D9 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D9_F_filt.fastq.gz" 
    ##                                                            Mock 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/Mock_F_filt.fastq.gz"

``` r
print(filtRs)
```

    ##                                                            F3D0 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D0_R_filt.fastq.gz" 
    ##                                                            F3D1 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D1_R_filt.fastq.gz" 
    ##                                                          F3D141 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D141_R_filt.fastq.gz" 
    ##                                                          F3D142 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D142_R_filt.fastq.gz" 
    ##                                                          F3D143 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D143_R_filt.fastq.gz" 
    ##                                                          F3D144 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D144_R_filt.fastq.gz" 
    ##                                                          F3D145 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D145_R_filt.fastq.gz" 
    ##                                                          F3D146 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D146_R_filt.fastq.gz" 
    ##                                                          F3D147 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D147_R_filt.fastq.gz" 
    ##                                                          F3D148 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D148_R_filt.fastq.gz" 
    ##                                                          F3D149 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D149_R_filt.fastq.gz" 
    ##                                                          F3D150 
    ## "/home/rstudio/essai/MiSeq_SOP/filtered/F3D150_R_filt.fastq.gz" 
    ##                                                            F3D2 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D2_R_filt.fastq.gz" 
    ##                                                            F3D3 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D3_R_filt.fastq.gz" 
    ##                                                            F3D5 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D5_R_filt.fastq.gz" 
    ##                                                            F3D6 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D6_R_filt.fastq.gz" 
    ##                                                            F3D7 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D7_R_filt.fastq.gz" 
    ##                                                            F3D8 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D8_R_filt.fastq.gz" 
    ##                                                            F3D9 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/F3D9_R_filt.fastq.gz" 
    ##                                                            Mock 
    ##   "/home/rstudio/essai/MiSeq_SOP/filtered/Mock_R_filt.fastq.gz"

``` r
out <- filterAndTrim(fnFs, filtFs, fnRs, filtRs, truncLen=c(240,160),
              maxN=0, maxEE=c(2,2), truncQ=2, rm.phix=TRUE,
              compress=TRUE, multithread=TRUE)
print(out)
```

    ##                               reads.in reads.out
    ## F3D0_S188_L001_R1_001.fastq       7793      7113
    ## F3D1_S189_L001_R1_001.fastq       5869      5299
    ## F3D141_S207_L001_R1_001.fastq     5958      5463
    ## F3D142_S208_L001_R1_001.fastq     3183      2914
    ## F3D143_S209_L001_R1_001.fastq     3178      2941
    ## F3D144_S210_L001_R1_001.fastq     4827      4312
    ## F3D145_S211_L001_R1_001.fastq     7377      6741
    ## F3D146_S212_L001_R1_001.fastq     5021      4560
    ## F3D147_S213_L001_R1_001.fastq    17070     15637
    ## F3D148_S214_L001_R1_001.fastq    12405     11413
    ## F3D149_S215_L001_R1_001.fastq    13083     12017
    ## F3D150_S216_L001_R1_001.fastq     5509      5032
    ## F3D2_S190_L001_R1_001.fastq      19620     18075
    ## F3D3_S191_L001_R1_001.fastq       6758      6250
    ## F3D5_S193_L001_R1_001.fastq       4448      4052
    ## F3D6_S194_L001_R1_001.fastq       7989      7369
    ## F3D7_S195_L001_R1_001.fastq       5129      4765
    ## F3D8_S196_L001_R1_001.fastq       5294      4871
    ## F3D9_S197_L001_R1_001.fastq       7070      6504
    ## Mock_S280_L001_R1_001.fastq       4779      4314

``` r
head(out)
```

    ##                               reads.in reads.out
    ## F3D0_S188_L001_R1_001.fastq       7793      7113
    ## F3D1_S189_L001_R1_001.fastq       5869      5299
    ## F3D141_S207_L001_R1_001.fastq     5958      5463
    ## F3D142_S208_L001_R1_001.fastq     3183      2914
    ## F3D143_S209_L001_R1_001.fastq     3178      2941
    ## F3D144_S210_L001_R1_001.fastq     4827      4312

``` r
errF <- learnErrors(filtFs, multithread=TRUE)
```

    ## 33514080 total bases in 139642 reads from 20 samples will be used for learning the error rates.

``` r
errR <- learnErrors(filtRs, multithread=TRUE)
```

    ## 22342720 total bases in 139642 reads from 20 samples will be used for learning the error rates.

``` r
plotErrors(errF, nominalQ=TRUE)
```

    ## Warning in scale_y_log10(): log-10 transformation introduced infinite values.
    ## log-10 transformation introduced infinite values.

![](essai_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
dadaFs <- dada(filtFs, err=errF, multithread=TRUE)
```

    ## Sample 1 - 7113 reads in 1979 unique sequences.
    ## Sample 2 - 5299 reads in 1639 unique sequences.
    ## Sample 3 - 5463 reads in 1477 unique sequences.
    ## Sample 4 - 2914 reads in 904 unique sequences.
    ## Sample 5 - 2941 reads in 939 unique sequences.
    ## Sample 6 - 4312 reads in 1267 unique sequences.
    ## Sample 7 - 6741 reads in 1756 unique sequences.
    ## Sample 8 - 4560 reads in 1438 unique sequences.
    ## Sample 9 - 15637 reads in 3590 unique sequences.
    ## Sample 10 - 11413 reads in 2762 unique sequences.
    ## Sample 11 - 12017 reads in 3021 unique sequences.
    ## Sample 12 - 5032 reads in 1566 unique sequences.
    ## Sample 13 - 18075 reads in 3707 unique sequences.
    ## Sample 14 - 6250 reads in 1479 unique sequences.
    ## Sample 15 - 4052 reads in 1195 unique sequences.
    ## Sample 16 - 7369 reads in 1832 unique sequences.
    ## Sample 17 - 4765 reads in 1183 unique sequences.
    ## Sample 18 - 4871 reads in 1382 unique sequences.
    ## Sample 19 - 6504 reads in 1709 unique sequences.
    ## Sample 20 - 4314 reads in 897 unique sequences.

``` r
dadaRs <- dada(filtRs, err=errR, multithread=TRUE)
```

    ## Sample 1 - 7113 reads in 1660 unique sequences.
    ## Sample 2 - 5299 reads in 1349 unique sequences.
    ## Sample 3 - 5463 reads in 1335 unique sequences.
    ## Sample 4 - 2914 reads in 853 unique sequences.
    ## Sample 5 - 2941 reads in 880 unique sequences.
    ## Sample 6 - 4312 reads in 1286 unique sequences.
    ## Sample 7 - 6741 reads in 1803 unique sequences.
    ## Sample 8 - 4560 reads in 1265 unique sequences.
    ## Sample 9 - 15637 reads in 3414 unique sequences.
    ## Sample 10 - 11413 reads in 2522 unique sequences.
    ## Sample 11 - 12017 reads in 2771 unique sequences.
    ## Sample 12 - 5032 reads in 1415 unique sequences.
    ## Sample 13 - 18075 reads in 3290 unique sequences.
    ## Sample 14 - 6250 reads in 1390 unique sequences.
    ## Sample 15 - 4052 reads in 1134 unique sequences.
    ## Sample 16 - 7369 reads in 1635 unique sequences.
    ## Sample 17 - 4765 reads in 1084 unique sequences.
    ## Sample 18 - 4871 reads in 1161 unique sequences.
    ## Sample 19 - 6504 reads in 1502 unique sequences.
    ## Sample 20 - 4314 reads in 732 unique sequences.
