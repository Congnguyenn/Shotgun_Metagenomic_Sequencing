# SHOTGUN METAGENOMIC SEQUENCING

## I. PRE-PROCESSING STAGE.
### 1.1 Adapter and quality trimming: fastp/Trimmomatic
**Reasons why you used fastp instead of trimmomatic**
- Automatically detect adapters
- Others author selected fastp mainly because the high performance (faster than trimmomatic or Cutadapt) despite performing far more operations than similar tools.
- Correct mismatched base pairs in overlapped regions

**Results**
Read1 before filtering:
total reads: 3889245
total bases: 587275995
Q20 bases: 504940278(85.9801%)
Q30 bases: 496296310(84.5082%)

Read2 before filtering:
total reads: 3889245
total bases: 587275995
Q20 bases: 505073547(86.0028%)
Q30 bases: 493559464(84.0422%)

Read1 after filtering:
total reads: 2837975
total bases: 412677751
Q20 bases: 396763805(96.1437%)
Q30 bases: 392740705(95.1689%)

Read2 after filtering:
total reads: 2837975
total bases: 412677751
Q20 bases: 395725107(95.892%)
Q30 bases: 389852127(94.4689%)

Filtering result:
reads passed filter: 5675950
reads failed due to low quality: 1620856
reads failed due to too many N: 3814
reads failed due to too short: 477870
reads with adapter trimmed: 2077164
bases trimmed due to adapters: 121134626

### 1.2 Identifying and removing host: Bowtie2/ phiX/ EukDetect/whokaryote
**Reasons why you used fastp instead of trimmomatic**
- EukDetect detects eukaryotes in shotgun metagenomic data using eukaryotic gene markers
- Uses a database of 521,824 universal marker genes from 241 conserved gene families

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
