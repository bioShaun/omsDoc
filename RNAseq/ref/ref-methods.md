---
output:
  pdf_document:
    citation_package: natbib
    latex_engine: xelatex
    template: ./svm-r-markdown-templates/svm-latex-ms.tex
title: "RNA-seq Analysis Method"
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

## Library construction and sequencing
RNA were prepared and sequenced on Illumina Hiseq 4000 platform. RNA quantity and integrity were determined by using Nanodrop 2000 (Thermo Scientific, Waltham, MA) and Bioanalyzer 2100 (Agilent Technologies, Santa Clara, CA). RNA-seq libraries were constructed using the Illumina TruSeq RNA Library Prep Kit v2(Illumina, San Diego, CA) following standard protocols. Poly(A)-containing transcripts was enriched with Oligo(dT)-Coated magnetic beads from total RNA. For each sample, adapters with unique barcodes were ligated to the end-polished cDNA fragments. The libraries were amplified by PCR and quantitated by Qubit 2.0 (Thermo Scientific, Waltham, MA).

## Quantification and functional enrichment analysis
Kallisto (0.42.4)[@kallisto] were applied for quantification with default parameters. Differential expression of genes (DEGs) between experimental conditions was calculated using edgeR (3.12.1)[@edger]. Go enrichment analysis of the DEGs was performed using the GOseq (1.22.0)[@goseq] based Wallenius non-central hyper-geometric distribution, which can adjust for gene length bias in DEGs. KEGG pathway enrichment analysis of the DEGs was done using KOBAS (2.0)[@kobas]. Other data statistic and visualizing were performed by in-house R scripts.

\newpage

# Refference
