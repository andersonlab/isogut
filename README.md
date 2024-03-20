# isogut
Initial processing, quality control and analysis of long-read sequencing data. The location of these scripts and data is on:
`/lustre/scratch126/humgen/projects/isogut`

## Pipeline

The quality control steps are located on the [iso-seq]([url](https://isoseq.how/umi/cli-workflow.html)) docs 

<img width="824" alt="image" src="https://github.com/andersonlab/isogut/assets/127568449/b9288144-bb67-4848-a2d5-9ceaf8e0d038">

In order to run this pipeline we require nextflow to be loaded on the FARM and then run in the directoru where `isogut.nf` is located along with the sanger.config file:

`nextflow -config sanger.config isogut.nf`

### Input Data Table

To save storage space and computation time (and the current difficulty of running iRODS on farm22) we can provide a list of samples that we are using in our analysis. This will work well for the purposes of this pilot but won't scale to institute wide sequence data. See below the note on how we can try to fetch the data from iRODS using HGI pipeline, in effect this will just populate the table below.

eg: 
`/lustre/scratch126/humgen/projects/isogut/input_samples.tsv`

| long_read            | short_read          | long_read_path                       |
|---------------|------------------|----------------------------|
| Isogut14548283| 5892STDY13265992 | /lustre/path/to/sample_1   |
| Isogut14548284| 5892STDY13265994 | /lustre/path/to/sample_2   |
| Isogut14548285| 5892STDY13430519 | /lustre/path/to/sample_3   |

**TO DO: Use the fetch_irods_lustre pipeline for this purpose that will then read into the input data table as a bash script runner**

The raw long-read sequencing data is on iRODS under project ID 7537. To retrieve it we initiate iRODS w iinit and after authentication, extract the data with:
imeta qu -z seq -d study_id = 7537 > imeta_output.txt. 

The data is downloaded and the results are pushed to `/results/sequence_data`

We will also need to rename the files to be the sample identifier in order to make downstream processing easier to reference. This names will of the form `isogutXXX` which is pulled from the bam SM tag. These are the Sanger names that correspond to the various metadata we may want to incoperate down the line.

### Primer Removal

Removal of primers and identification of barcodes is performed using lima

`lima ${bam_path} /lustre/scratch126/humgen/projects/isogut/qc/primers.fasta \$sample_name.fl.bam --isoseq`

The 10x 3' version of the primers is located:
`/lustre/scratch126/humgen/projects/isogut/qc/primers.fasta`

### Barcode Removal

### Tag Removal

### Refining Reads
