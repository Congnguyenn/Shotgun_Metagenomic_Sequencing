# SHOTGUN METAGENOMIC SEQUENCING

## I. PRE-PROCESSING STAGE.
### 1.1 Adapter and quality trimming: fastp
**Reasons why you used fastp instead of trimmomatic**
- Automatically detect adapters
- Others author selected fastp mainly because the high performance (faster than trimmomatic or Cutadapt) despite performing far more operations than similar tools.
- Correct mismatched base pairs in overlapped regions

**Result:**
	Before filtering	% passed	% failed	low quality	too many N	too short	low complexity
2111RD03_S33_L001	4657700	85.83	14.17	9.71	0.22	4.16	0.07
2111RD02_S26_L001	3163330	82.97	17.03	9.64	0.21	6.15	1.02
2111RD01_S25_L001	2421216	88.74	11.26	8.48	0.17	2.43	0.19
2111RD01_S19_L001	7778490	77.62	22.38	12.31	0.06	9.94	0.07
709_S20_L001	2110400	53.26	46.74	18.37	0.04	28.04	0.28
merged	20131136	79.14	20.86	11.46	0.13	9.00	0.26

### 1.2 Verify the quality of sequencing: fastQC

### 1.3 Identifying and removing host: Bowtie2
- Remove both anchovy and human DNA: Coilia nasus (Japanese grenadier anchovy) and GRCh38.p14
--> Why human DNA still remains in the bracken result ?
--> How to completely remove human DNA ?

## II. TAXONOMY ASSIGNMENT and VISUALIZATION
### 2.1 Taxonomy assignment: Kraken2 | Estimate abundance: bracken | Visualize data: krona   
- Kraken2 database: Minikraken: preliminary testing has shown the accuracy of a reduced Kraken 2 database to be quite similar to the full-sized Kraken 2 database, while Kraken 1's MiniKraken databases often resulted in a substantial loss of per-read sensitivity.
- braken: at 3 levels: Phylum, Genus, Species
**Question**
- Human DNA still remain in the bracken result --> can I remove it and re-calculate the percentage

## Why the unclassified taxa is too high?
- Didier Andrivon: 'unclassified' could relate to bacterial taxa assigned to the general clades listed on the legend (Proteobacteria, Clostridiales, etc...) based on sequence similarities/blasts, but not to any given genus within these clades.
- Alex Ignatov: a large portion of sequences (taxa) had frequency of occurrence below of certain threshold (1% for an example) and they have not been included into analysis.
- My opinion: Not found in the database and repeated regions

 **--> What should we do ?:**
 --> to solve the repeat regions: I performed low-complexity filtering with fastp (threshold=30%)
 low-complexity: The complexity is defined as the percentage of base that is different from its next base (base[i] != base[i+1]).
 The threshold for low complexity filter (0~100). Default is 30, which means 30% complexity is required. (int [=30])
 - Result: Remove low complexity can enhance the result (reduce human DNA) but it does not significant (32284 reads are removed)
 --> to solve the frequency of occurrence: I suggest, increase the input sample and coverage (how much? --> unknown)
 --> How about using MetaPhlAn3 (maker genes-based) instead of kraken2 (k-mer based): https://www.sciencedirect.com/science/article/pii/S2001037021004931

## Finding the similar paper:
### Shotgun sequence-based metataxonomic and predictive functional profiles of Pe poke, a naturally fermented soybean food of Myanmar
- Data: available
- Method: shotgun - ONT technology - assembly based

### A shotgun metagenomics approach to detect and characterize unauthorized genetically modified microorganisms in microbial fermentation products
- Data: available
- Method: shotgun - ONT + illumina - assembly based

### Shotgun Metagenomics of a Water Kefir Fermentation Ecosystem Reveals a Novel Oenococcus Species
- Data: available
- Method: shotgun - assembly based

### New insights of bacterial communities in fermented vegetables from shotgun metagenomics and identification of antibiotic resistance genes and probiotic bacteria

## Reference:
1. https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-019-6289-6
Rather similar between read-based and assembly-based method. Functional analysis: read-based produces more information but also be over-predicted

Assembly-based depends on
    Number of sequences
    Richness and evenness (high diversity --> harder)
    require more computational resource

Read-based depends on
    Similarity comparation:
        the aims are just functional or taxonomic profile 
        drawback: the sequence could be too short to produce accurate assignment
        Short-reads are not enough information to annotate functional (not discriminative enough)
    K-mer frequency counting: (Kraken2 or Centrifuge)
        This method can be only used for taxonomy (not function at all)
    Identification of phylogenetic marker genes (maker gene profilling)
2. https://aura.abdn.ac.uk/bitstream/handle/2164/10167/NBT_R37313C_line_edit_SJ_1493899923_1_final_for_self_archiving.pdf;jsessionid=3F3C8B95A4B2B3DA9FB371A09B0F2715?sequence=1
3. https://bioinformaticsworkbook.org/dataAnalysis/Metagenomics/MetagenomicsP1.html#gsc.tab=0   

4. https://journals.asm.org/doi/10.1128/mSystems.00522-20
    They (hosts) were not removed since reference genomes were not available for all food substrates.
