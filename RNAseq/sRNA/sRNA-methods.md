---
output:
  pdf_document:
    citation_package: natbib
    latex_engine: xelatex
    template: ./svm-r-markdown-templates/svm-latex-ms.tex
title: "Small RNA-seq Analysis"
#thanks: ""
#abstract: "This document provides an introduction to R Markdown, argues for its..."
#keywords: "pandoc, r markdown, knitr"
geometry: margin=1in
fontfamily: mathpazo
fontsize: 11pt
# spacing: double
bibliography: ref.bib
biblio-style: apsr
---

# Methods
## Library construction and sequencing
Total RNA was separated by 15% agarose gels to extract the small RNA (18-30 nt). After precipitated by ethanol and centrifugal enrichment of small RNA sample, the library was prepared according to the method and process of Small RNA Sample Preparation Kit (Illumina, RS-200-0048). The main contents are as follows:
    1) Connecting the 3' adaptor to the separated small RNA.
    2) Connecting the 5' adaptor to the separated small RNA.
    3) RT-PCR.
    4) Recycling strips of 145-160bp (22-30nt RNA).

RNA concentration of library was measured using Qubit® RNA Assay Kit in Qubit® 2.0 (Thermo Scientific, Waltham, MA) to preliminary quantify and then dilute to 1ng/μl. Insert size was assessed using the Agilent Bioanalyzer 2100 system (Agilent Technologies, CA, USA), and after the insert size consistent with expectations, qualified insert size was accurate quantitative using Taqman fluorescence probe of AB Step One Plus Real-Time PCR system (Library valid concentration>2nM). The qualified libraries were sequenced by an Illumina Hiseq 2500 platform and generate 50 bp single-end reads.

# Sequencing data analysis
Cutadapt[@cutadapt] (v1.16) was used for adapter trimming. Trimmed reads were mapped to genome by bowtie[@bowtie] (v0.11.3) (bowtie -n 1 -e 80 -l 30 -m 5 --best --strata). Novel miRNAs are predicted by miRDeep2[@mirdeep2] (v2.0.0.8) upon the detection of potential mature, star and loop sequences from the read pool. Targetfinder[@targetfinder] was used to predict small RNA binding sites on target genes from a sequence database.

Differential expression of miRNAs between experimental conditions was calculated using edgeR[@edger] (v3.12.1). Go enrichment analysis of the miRNA target genes was performed using the GOseq[@goseq] (v1.22.0) based Wallenius non-central hyper-geometric distribution, which can adjust for gene length bias. KEGG pathway enrichment analysis was done using KOBAS[@kobas] (v2.0). Other data statistic and visualizing were performed by in-house R scripts.

# Refference
