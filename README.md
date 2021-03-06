# deMeta
Reverse the Meta-analysis mostly used by GWAS.

A typical scenario is for using GWAS consortium meta-analysis results for a contributing group.
For example, a group has performed GWAS on its own samples, and contributed the GWAS summary statistics to a Consortium. If the group wants to perform polygenic risk prediction on it sample, it will need the summary statistics from all contributing groups except its own. Two options may achieve this goal, 1.) The analysts of the consortium can re-do the meta exlcuding the sample from requesting group; 2.) the consortium share sub-study summary statistics with each contributing groups. The first option will incur heavey workload to the analysts if more than 1 substudies wanted to be removed. The second option may sometimes not practical due to data regulation.

Other cases during daily research may also poped up. For example, you have two summary statistics from two GWAS, but one include another, you want to computed genetic correlation of the two. In this case, you need to computer the non-overlapping suammary statistics for the large GWAS.

$python Subtract_meta.py -h
usage: Subtract Meta [-h] --masf MASF [--masA1 MASA1] [--masA2 MASA2]
                     [--masEff MASEFF] [--masOR MASOR] [--masisORSE]
                     [--masP MASP] [--masSE MASSE] [--masV MASV]
                     [--masCHR MASCHR] [--masPOS MASPOS] [--masN MASN]
                     [--masZ MASZ] [--masSNP MASSNP] --ssf SSF [--ssA1 SSA1]
                     [--ssA2 SSA2] [--ssEff SSEFF] [--ssOR SSOR] [--ssP SSP]
                     [--ssSE SSSE] [--ssisORSE] [--ssV SSV] [--ssN SSN]
                     [--ssZ SSZ] [--ssSNP SSSNP] [--top1 TOP1] [--top2 TOP2]
                     [--flip] [--noIVW] --out OUT

    From meta-results remove one contributing study.

    Applicable to:
        1. Inverse variance weighted meta-analysis
        2. Sample size weighted meta-analysis
    Figures:
        1. Manhattan plots for before and after removing the sub-study
        2. QQ-plots for before and after removing the sub-study
    Notes:
        1. Only common SNPs in the two file will be analyzed. The SNPs that
        exist only in the original meta-analysis results should be added back.


    Author: Yunpeng Wang, yunpeng.wng@gmail.com;
            Jiangming Sun, jiangming.sun@med.lu.se
    Data: 1st Aug, 2020

optional arguments:
  -h, --help       show this help message and exit
  --masf MASF      Meta-analysis result file name
  --masA1 MASA1    Meta-analysis result effect allele column name
  --masA2 MASA2    Meta-analysis result the other allele column name
  --masEff MASEFF  Meta-analysis result effect (of A1) column name
  --masOR MASOR    Meta-analysis result Odds ratio (of A1) column name
  --masisORSE      Is the Meta-analysis result SE on OR scale, default on ln(OR) scale
  --masP MASP      Meta-analysis result p value (of A1) column name
  --masSE MASSE    Meta-analysis result standard error (of Beta) column name
  --masV MASV      Meta-analysis result variance (of Beta) column name
  --masCHR MASCHR  Chromosome number column name in original Meta-analysis results
  --masPOS MASPOS  Genomic position column name in original Meta-analysis results
  --masN MASN      Meta-analysis result Sample size column name
  --masZ MASZ      Meta-analysis result Z score column name
  --masSNP MASSNP  Meta-analysis result SNP column name
  --ssf SSF        Sub-study result file name
  --ssA1 SSA1      sub-study result effect allele column name
  --ssA2 SSA2      sub-study result the other allele column name
  --ssEff SSEFF    sub-study result effect (of A1) column name
  --ssOR SSOR      sub-study result Odds ratio (of A1) column name
  --ssP SSP        sub-study result p value (of A1) column name
  --ssSE SSSE      sub-study result standard error (of Beta) column name
  --ssisORSE       Is the sub-study result SE on OR scale, default on ln(OR) scale
  --ssV SSV        sub-study result variance (of Beta) column name
  --ssN SSN        sub-study result Sample size column name
  --ssZ SSZ        sub-study result Z score column name
  --ssSNP SSSNP    sub-study result SNP column name
  --top1 TOP1      max -log10(P) for original meta-analysis to plot in the manhattan (default from the data)
  --top2 TOP2      max -log10(P) for subtracted results to plot in the manhattan (default from the data)
  --flip           whether flip strand, using meta-analysis result as reference
  --noIVW          whether meta-analysis result is inverse variance weighted? Otherwise using sample size weighted
  --out OUT        Result file prefix
