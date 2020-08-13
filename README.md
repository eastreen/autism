### Methods ###

#### DNA extraction and sample preparation ####

Genetic material was taken from 194 patients with ASD. During preparation of paired-end libraries 3 different capture assays were used: TruSeq DNA Exome for 73 samples (hg19 build); SureSelect Human All Exon V7 for 120 samples (hg38 build); SureSelect Human All Exon V6+UTR r2 for 1 sample (hg38 build). DNA sequencing was performed on Illumina HiSeq 4000 generating 35-100 nucleotide reads.

#### QC and mapping ####

Quality check of raw data was run with FastQC (version 0.11.9) and did not raise major concerns regarding quality of reads. Paired-end reads were aligned using bwa (0.7.17-r1188) to hg19 human reference genome for 73 subjects and hg38 for 121 subjects. Raw aligned BAM files were then subjected to sorting, deduplication and base quality score recalibration as per GATK Best Practices for data preprocessing (GATK version 4.1.6).

#### SNP calling ####

Consequently, base recalibrated BAM files were used in Germline short variant discovery workflow (GATK version 4.1.6). Each sample was submitted to HaplotypeCaller separately with an appropriate BED file of intervals. Since 3 different capture assays were used for library preparation, 3 groups of samples were subjected to joint-genotyping separately. Consolidated GVCF files were submitted to an exact test of excess heterozygosity (ExcessHet > 54.69); that was the only instance of hard filtering. The rest of the filtering process was done with VariantRecalibrator. Truth sensitivity level 99.60 for SNPs and 95.00 for INDELs were chosen. Resulting hg38 VCF call-sets were lifted-over to hg19 build using Assembly Converter, and all 3 VCF call-sets were then merged with bcftools (1.10.2).

#### SNP calling anno ####

The whole call-set was intersected with several databases using ANNOVAR: refGene, cytoBand, ClinVar, Exac03, avSNP147, dbNFSP version 3.0a, gnomAD Exome.

#### CNV calling ####

CNV calling of WES data was performed by exomecn.mops function with default parameters (R package cn.mops version 1.32.0).

#### CNV calling anno ####

CNV call-set was intersected with Database of Genomic Variants (DGV) by ANNOVAR.

![coverage](./coverage.png) 
