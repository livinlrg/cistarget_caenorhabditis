# Caenorhabditis cisTarget databases

Using motif information from cis-bp (https://cisbp.ccbr.utoronto.ca/), and chip-seq data from the modERN project (https://epic.gs.washington.edu/modERNresource/), cisTarget databses were created to predict gene regulatory networks using SCENIC (https://scenic.aertslab.org/). Here, those databases are freely available to run gene regulatory network prediction on your own single cell data from either C. elegans or C. briggsae. As more databases are created for additional species, they will be added here.

If you use these databases, please cite this publication:
__

### Motif database creation
1. Curation of the motif databases
   - All motif from cis-bp were pulled in the fall of 2024 for C. elegans and C. briggsae. These motifs were curated for experiments using wild-type alleles.
   - These motifs were converted to cluster buster format using a custom R script.
   - Any TF that was found to have an orthologous gene from the reciprocal species was added to the list of motifs for that species.
2. Creating prediction regions
   - With a custom R script, bed files containing either 500 bp upsteam of every CDS, or 2000 bp upstream and the gene body were generated.
   - Fasta files using these bed files was then extracted with bedtools.
3. cisTarget databses were then generated for the motif based data using create_cistarget_motif_databases.py available through (https://github.com/aertslab/create_cisTarget_databases).

### Chip-seq database creation for C. elegans
1. Chip-seq data curation
   - Predicted peak data was pulled from the modERN project website.
   - For each experiemnt, the predicted peaks were converted into bed files using a custom R script then subsequently converted into a bigWig file.
2. Creating prediction regions
   - For every gene, a prediction region was generated using the modERN datasets predicted primary target. If a peak existed for that gene, then that prediction region was used. Otherweise, 1000 bp upstream of the target gene was used.
3. cisTarget databases were then generated for the chip-seq based data using create_cistarget_track_databases.py
