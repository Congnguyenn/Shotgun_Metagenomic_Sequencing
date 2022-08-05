#SHOTGUN METAGENOMIC SEQUENCING

## I. PRE-PROCESSING STAGE.
### 1.1 Adapter and quality trimming: fastp/Trimmomatic






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
