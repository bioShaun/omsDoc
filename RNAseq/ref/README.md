---
output:
  pdf_document:
    citation_package: natbib
    latex_engine: xelatex
    template: ./svm-r-markdown-templates/svm-latex-ms.tex
title: "分析结果文件说明"
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


\newpage
# fastqc

## 文件列表

|文件名[^1]|目录|文件类型|文件说明|
|:--------------------|:--------|:--------|:-------------------------------------|
|fastqc_general_stats(.txt/.xlsx)|主目录|表格|数据基本统计信息|
|样品名.clean_fastqc|fastqc_results|目录|该样品 FastQC 分析结果|
|样品名.clean_fastqc.html|fastqc_results|html 报告|该样品 FastQC 报告|
|样品名.gc_distribution.line(.png/.pdf)|gc_plot|图片|该样品 GC 分布图|
|样品名.reads_quality.bar(.png/.pdf)|reads_quality_plot|图片|该样品 reads 质量分布图|

## 表格

### fastqc_general_stats

|表头|说明|
|:--------|:--------------------|
|Sample_ID|样品名|
|Reads_number(M)|测序 reads 数目，单位兆 (Mega)|
|Reads_length(bp)|测序长度|
|Data_size(G)|测序 reads 数据量，单位千兆 (Giga)|
|Q30(%)|测序 reads 平均质量值超过30 (准确率>99.9%) 的比例|
|GC(%)|GC 含量|


## 图片

### gc_distribution

不同碱基使用不同颜色表示，N 代表测序中不确定的碱基。y 轴为不同碱基的比例，x 轴代表碱基在 reads 中的位置 (因为将 read1, read2放在同一张图展示，图片的右半部分展示的是 read2 的 GC 分布情况，x 轴数值减去 read 长度为该碱基在 read2 中的位置)。在随机文库中，不同碱基在 reads 中的位置不存在偏好，因此通常情况下，代表各碱基的线条会相对平稳。但因为在建库时使用的6pb随机引物会引起 reads 前几个碱基的偏好性，因此图片中前几个碱基位置会出现比较大的波动。

### reads_quality

x 轴代表数据质量值，y 轴代表不同质量值序列所占比例。质量值大于30 (准确率高于99.9%) 的高质量的序列在图中使用深色表示。

## 其他

### 样品名.clean_fastqc

文件说明参考FastQC 官方文档([https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/][fastqc_mannual])。

\newpage
# mapping

## 文件列表

|文件名|目录|文件类型|文件说明|
|:--------------------|:--------|:--------|:-------------------------------------|
|mapping_stats(.txt/.xlsx)|主目录|表格|比对结果统计|
|mapping_stats_plot(.png/.pdf)|主目录|图片|比对率统计图|

## 表格

### mapping_stats

|表头|说明|
|:----------------------------|:---------------------------------------|
|Sample|样品名|
|Number of input reads|进行比对分析的 reads 总数|
|Average input read length|reads 平均长度|
|Uniquely mapped reads number|能够比对到基因组唯一位置的 reads 数量|
|Uniquely mapped reads %|能够比对到基因组唯一位置的 reads 比例|
|Average mapped length|reads 比对到基因组的平均长度|
|Number of splices: Total|比对到剪切位点的 reads 数目|
|Number of splices: Annotated (sjdb)|比对到已注释的剪切位点的 reads 数量|
|Number of splices: GT/AG|比对到 GT/AG 剪切位点的 reads 数目|
|Number of splices: GC/AG|比对到 GC/AG 剪切位点的 reads 数目|
|Number of splices: AT/AC|比对到 AT/AC 剪切位点的 reads 数目|
|Number of splices: Non-canonical|比对到非经典剪切位点的 reads 数量|
|Mismatch rate per base, %|reads 单碱基错配率|
|Deletion rate per base|reads 单碱基缺失率|
|Deletion average length|reads 缺失平均长度|
|Insertion rate per base|reads 单碱基插入率|
|Insertion average length|reads 插入平均长度|
|Number of reads mapped to multiple loci|比对到基因组多个位置的 reads 数量|
|% of reads mapped to multiple loci|比对到基因组多个位置的 reads 比例|
|Number of reads mapped to too many loci|比对到基因组过多位置的 reads 数量 (默认为超过10个位置)|
|% of reads mapped to too many loci|比对到基因组过多位置的 reads 比例 (默认为超过10个位置)|
|% of reads unmapped: too many mismatches|因错配过多没有比对到基因组的 reads 比例|
|% of reads unmapped: too short|因比对到基因组长度过短没有比对到基因组的 reads 比例|
|% of reads unmapped: other|因其他原因没有比对到基因组的 reads 比例|
|Number of chimeric reads|chimeric reads (同一 reads 比对到基因组不同区域) 的数量|
|% of chimeric reads|chimeric reads 的比例|


## 图片

### mapping_stats_plot

蓝色，橙色和黄色分别代表只比对到基因组一个位置 (unique mapped reads)，比对到基因组多个位置 (multiple mapped reads) 和无法比对到基因组 (unmapped reads) 的 reads 的比例。

\newpage

# rseqc

## 文件列表

|文件名|目录|文件类型|文件说明|
|:-----------------------------------------------|:-------------------|:----------|:---------------------------|
|样品名.inner_distance_freq.txt|inner_distance|表格|该样品插入片段长度统计表|
|样品名.inner_distance.bar(.png/.pdf)|inner_distance|图片|该样品插入片段分布图|
|inner_distance.bar(.png/.pdf)|inner_distance|图片|所有样品插入片段分布图|
|样品名.geneBodyCoverage.txt|genebody_coverage|表格|该样品基因区域 reads 覆盖统计表|
|样品名.genebody_coverage.point(.png/.pdf)|genebody_coverage|图片|该样品基因区域 reads 覆盖分布图|
|genebody_coverage.point(.png/.pdf)|genebody_coverage|图片|所有样品基因区域 reads 覆盖分布图|
|样品名.read_distribution.txt|read_distribution|表格|该样品 reads 在基因区域分布统计|
|样品名.read_distribution.pie(/.pdf)|read_distribution|图片|该样品 reads 在基因区域分布图|
|read_distribution.bar(.png/.pdf)|read_distribution|图片|所有样品 reads 在基因区域分布图|

## 表格

### inner_distance_freq

|表头|说明|
|:----------------------------|:---------------------------------------|
|V1[^2]|插入片段长度区间起始|
|V2|插入片段长度区间终止|
|V3|插入片段长度区间内 reads 数目|

### genebody_coverage
第一行为不同等分区域。
第二行为每个等分区域 reads 数目。

### read_distribution

|表头|说明|
|:----------------------------|:---------------------------------------|
|Total Reads|总 reads 数目|
|Total Tags|总 tag 数目，read 如果在比对过程中被剪切成两段，则计做2个 tag|
|Total Assigned Tags|能够唯一分配到各基因区域的 tag 数量|
|Group|不同基因区域|
|Total_bases|各区域总碱基长度|
|Tag_count|各区域 tag 数目|
|Tags/Kb|各区域每10kb长度内 tag 数目|

## 图片

### inner_distance

x 轴代表文库插入片段长度，可以理解为 read1 和 read2在基因组中的距离，该值为负数代表 read1 和 read2 有部分重叠 (overlap)。(文库片段长度 = 插入片段长度 + read1长度 + read2长度)

### genebody_coverage

将所有基因的转录本按照比例100等分，分别计算每个区域上的 reads 覆盖情况，进行标准化之后得到基因5'端至3'端的整体表达情况。右图展示了基因区域 reads 覆盖的情况。通常情况下 reads 在5'端和3'端的覆盖度是一致的，若 reads 覆盖在5'或3'端存在明显的偏好，说明样品 RNA可能存在不完整的情况。

### read_distribution

统计落在不同基因区域 (包括上下游10kb) 的 reads 的比例。我们使用饼图展示单独每个样品的情况，使用条形图展示所有样品的情况。图中，不同颜色代表不同的基因区域，区域大小代表 reads 的多少。

\newpage

# quantification

## 文件列表

|文件名|目录|文件类型|文件说明|
|:---------------------------------------------------|:-----------------------|:----------|:-------------------------|
|abundance(.tsv/.h5)|kallisto/样品名|表格|kallisto 定量结果|
|Gene.count(.txt/.xlsx)|expression_summary|表格|基因 readcount 统计表|
|Gene.tpm(.txt/.xlsx)|expression_summary|表格|基因 tpm 统计表|
|Gene_expression(.png/.pdf)|expression_summary|图片|基因整体表达展示图|
|Gene_expression.density_plot(.png/.pdf)|expression_summary|图片|基因整体表达密度图|
|Gene_expression.boxplot(.png/.pdf)|expression_summary|图片|基因整体表达盒形图|
|Gene_expression.violin(.png/.pdf)|expression_summary|图片|基因整体表达小提琴图|
|Sample.correlation.heatmap(.png/.pdf)|expression_summary|图片|样品表达相关性热图|
|PCA_plot(.png/.pdf)|expression_summary|图片|样品主成分分析散点图|
|A组\_vs\_B组.edgeR.DE_results(.txt/.xlsx)|differential_analysis/A组\_vs\_B组|表格|A组\_vs\_B组 差异分析总表|
|A组\_vs\_B组.A组-UP.edgeR.DE_results(.txt/.xlsx)|differential_analysis/A组\_vs\_B组|表格|在A组中表达量显著高于B组的基因的差异分析结果|
|A组\_vs\_B组.A组-UP.edgeR.DE_results.diffgenes(.txt/.xlsx)|differential_analysis/A组\_vs\_B组|表格|在A组中表达量显著高于B组的基因列表|
|A组\_vs\_B组.B组-UP.edgeR.DE_results(.txt/.xlsx)|differential_analysis/A组\_vs\_B组|表格|在B组中表达量显著高于A组的基因的差异分析结果|
|A组\_vs\_B组.B组-UP.edgeR.DE_results.diffgenes(.txt/.xlsx)|differential_analysis/A组\_vs\_B组|表格|在B组中表达量显著高于A组的基因的差异分析结果|
|A组\_vs\_B组.ALL.edgeR.DE_results.diffgenes(.txt/.xlsx)|differential_analysis/A组\_vs\_B组|表格|A组\_vs\_B组分析中所有差异表达基因的列表|
|A组\_vs\_B组.Volcano_plot(.png/.pdf)|differential_analysis/A组\_vs\_B组|图片|A组\_vs\_B组差异分析火山图|
|Diff.gene.count(.txt/.xlsx)|expression_summary|表格|差异表达基因 readcount 统计表|
|Diff.gene.tpm(.txt/.xlsx)|expression_summary|表格|差异表达基因 tpm 统计表|
|Diff.genes.heatmap(.png/.pdf)|expression_summary|图片|差异表达基因聚类热图|

## 表格

### abundance
|表头|说明|
|:------------|:---------------------------------------|
|target_id|转录本在数据库中的编号|
|length|转录本长度|
|eff_length|转录本有效长度，可以理解为测序片段来自转录本的所有可能的位置之和，eff_length = 转录本长度 - 测序片段长度 + 1|
|est_counts|转录本定量 count 值|
|tpm|转录本定量 tpm 值|

### Gene.count
第一列为基因 ID，后续每一列为一个样品的基因 readcount 值。

### Gene.tpm
第一列为基因 ID，后续每一列为一个样品的基因 tpm 值。

### A组_vs_B组.edgeR.DE_results[^3]

|表头|说明|
|:----------------------------|:---------------------------------------|
|Gene_ID|基因在数据库中的编号|
|样品名|样品的基因表达 tpm 值|
|logFC|A组样品表达量相对于B组样品表达量的变化倍数进行log2转换的结果|
|PValue|edgeR 软件统计校验P值，P值越小代表基因表达差异在统计学上越显著|
|FDR|使用 BH 方法进行多重校验后的 P值|


## 图片

### Gene_expression[^4]

使用 log10 标准化后基因表达值进行作图，左上角和右下角分别为基因表达箱型图和小提琴图，横坐标为不同样品，纵坐标为标准化后的基因表达值；下图为基因的表达密度，横坐标为标准化后的基因表达值，纵坐标为不同表达值密度值。

### Sample.correlation.heatmap

使用 log10 标准化后的基因表达值计算样品间的皮尔逊相关系数 (Pearson correlation coefficient) 作图。颜色靠近红色代表相关性系数高于平均，靠近绿色代表相关性系数低于平均。

### PCA_plot

x 轴为占据最大变异的成分，y 轴为占据第二大的变异成分。如果样品间的差异足够显著，则在图中反映出来的结果就是代表这些样品的点会分布在不同的区域。

### A组_vs_B组.Volcano_plot

x 轴为 logFC 值，y 轴为 FDR 值。图中红色点和绿色点为通过差异筛选阈值 (|logFC| >= 1 并且 FDR <= 0.05) 的差异基因。

### Diff.genes.heatmap

x 轴方向代表不同样品，y 轴方向代表不同基因。不同颜色代表基因表达量高低。颜色靠近红色代表基因表达高于平均值，靠近绿色代表低于平均值。

\newpage

# enrichment

## 文件列表

|文件名|目录|文件类型|文件说明|
|:----------------------------------------------------|:---------------------|:---------|:-------------------------|
|A组\_vs\_B组.ALL.go.enrichment(.txt/.xlsx)|go/A组\_vs\_B组|表格|A组\_vs\_B组分析中所有差异表达基因 GO 富集分析结果|
|A组\_vs\_B组.A组-UP.go.enrichment(.txt/.xlsx)|go/A组\_vs\_B组|表格|A组表达显著高于B组的差异基因 GO 富集分析结果|
|A组\_vs\_B组.B组-UP.go.enrichment(.txt/.xlsx)|go/A组\_vs\_B组|表格|B组表达显著高于A组的差异基因 GO 富集分析结果|
|A组\_vs\_B组.go.enrichment.barplot(.png/.pdf)|go/A组\_vs\_B组|图片|GO 富集分析柱状图|
|ALL.(MF/BP/CC).GO.DAG(.png/.pdf)|go/A组\_vs\_B组/DAG|图片|A组\_vs\_B组分析中所有差异表达基因 GO 富集有向无环图|
|A组-UP.(MF/BP/CC).GO.DAG(.png/.pdf)|go/A组\_vs\_B组/DAG|图片|A组表达显著高于B组的差异基因 GO 富集有向无环图|
|B组-UP.(MF/BP/CC).GO.DAG(.png/.pdf)|go/A组\_vs\_B组/DAG|图片|B组表达显著高于A组的差异基因 GO 富集有向无环图|
|A组\_vs\_B组.ALL.kegg.enrichment(.txt/.xlsx)|kegg/A组\_vs\_B组|表格|A组\_vs\_B组分析中所有差异表达基因 KEGG 富集分析结果|
|A组\_vs\_B组.A组-UP.kegg.enrichment(.txt/.xlsx)|kegg/A组\_vs\_B组|表格|A组表达显著高于B组的差异基因 KEGG 富集分析结果|
|A组\_vs\_B组.B组-UP.kegg.enrichment(.txt/.xlsx)|kegg/A组\_vs\_B组|表格|B组表达显著高于A组的差异基因 KEGG 富集分析结果|
|A组\_vs\_B组.kegg.enrichment.barplot(.png/.pdf)|kegg/A组\_vs\_B组|图片|KEGG 富集分析柱状图|
|\*pathview.png|kegg/A组\_vs\_B组/\*pathway|图片|KEGG 富集分析通路图，原始通路图|
|\*pathview.gene.png|kegg/A组\_vs\_B组/\*pathway|图片|KEGG 富集分析通路图，将通路中分子名称修改为对应基因的名称|

\newpage

## 表格

### A组\_vs\_B组.ALL.go.enrichment[^5]

|表头|说明|
|:----------------------------|:---------------------------------------|
|category|GO 编号|
|over_represented_pvalue|差异基因在该 GO Term 的富集显著性P值|
|qvalue|BH 校正后的显著性P值|
|numDEInCat|富集到该 GO Term 的差异基因数目|
|numInCat|注释到该 GO Term 的所有基因数目|
|term|GO 名称|
|ontology|GO 分类|
|DE_id|富集到该 GO 通路的差异基因编号|

### A组\_vs\_B组.ALL.kegg.enrichment[^6]

|表头|说明|
|:----------------------------|:---------------------------------------|
|#Term|KEGG 通路名称|
|Database|数据库名称，我们的分析中为 KEGG PATHWAY|
|ID|KEGG 通路编号|
|Input number|富集到该 KEGG 通路的差异基因数目|
|Background number|该通路的基因数目|
|P-Value|差异基因在该 KEGG 通路的富集显著性P值|
|Corrected P-Value|BH 校正后的显著性P值|
|Input|富集到该 KEGG 通路的差异基因编号|
|Hyperlink|该 KEGG 通路在 KEGG 网站的链接地址|


## 图片

### A组\_vs\_B组.go.enrichment.barplot

对该比较组的全部3个 GO 富集分析结果，分别选择显著富集 (Pvalue < 0.05) 的 15 条进行绘图 (若不足15条，全部选择)，在图中以蓝色，红色和绿色进行区分。x 轴为显著富集的 GO Term 名称，y 轴为　-log10(Pvalue)。

### ALL.(MF/BP/CC).GO.DAG[^7]

使用富集程度最高的5个 GO Term 作为主节点，并用方框表示，通过包含关系将关联的该分类 (MF,BP,CC) 下的 GO Term 全部展示。从上至下所定义的功能范围精细，颜色越深代表富集程度越高。

### A组\_vs\_B组.kegg.enrichment.barplot

对该比较组的全部3个 KEGG 富集分析结果，分别选择显著富集 (Pvalue < 0.05) 的 15 条进行绘图 (若不足15条，全部选择)，在图中以蓝色，红色和绿色进行区分。x 轴为显著富集的 KEGG通路名称，y 轴为　-log10(Pvalue)。

### pathview

预先从 KEGG 网站 ([http://www.genome.jp/kegg/][kegg_site]) 下载原始的 KEGG 通路图。使用 pathview 软件将差异基因在原始图片中根据差异分析logFC值进行标注，正值靠近橙色，负值靠近蓝色。带有 gene 后缀的图片将原始图片中的分子名称替换为相应基因的名称。

\newpage

<!-- # 名词解释

>**readcount:**
>
>**tpm:**
> -->


[^1]: 括号中为文件的后缀，为方便老师使用，同一文件会保存成不同格式，使用"/"分隔不同后缀名。
[^2]: 针对没有表头的表格，使用V1，V2，V3...Vn代表表格表格第一道n列。
[^3]: A组_vs_B组.A组-UP.edgeR.DE_results，A组_vs_B组.B组-UP.edgeR.DE_results表头与A组_vs_B组.edgeR.DE_results相同，故不重复说明。
[^4]: Gene_expression图中包含Gene_expression.density_plot，Gene_expression.boxplot和Gene_expression.violin三个图，因此不对这三个图进行单独说明
[^5]: A组\_vs\_B组.A组-UP.go.enrichment，A组\_vs\_B组.B组-UP.go.enrichment与该表表头相同，故不重复说明。
[^6]: A组\_vs\_B组.A组-UP.kegg.enrichment，A组\_vs\_B组.B组-UP.kegg.enrichment与该表表头相同，故不重复说明。
[^7]: A组-UP.(MF/BP/CC).GO.DAG，B组-UP.(MF/BP/CC).GO.DAG与该图作图方法相同，故不重复说明。

[fastqc_mannual]:https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/
[kegg_site]:http://www.genome.jp/kegg/
