# isogut
Initial processing, quality control and analysis of long-read sequencing data. The location of these scripts and data is on:
`/lustre/scratch126/humgen/projects/isogut`

## Pipeline

In order to run this pipeline we require nextflow to be loaded on the FARM and then run in the directoru where `isogut.nf` is located along with the sanger.config file:

`nextflow -config sanger.config isogut.nf`

## Input Data Table

To save storage space and computation time (and the current difficulty of running iRODS on farm22) we can provide a list of samples

### Download All Long-Read Sequences

**TO DO: Use the fetch_irods_lustre pipeline for this purpose that will then read into the input data table**

The raw long-read sequencing data is on iRODS under project ID 7537. To retrieve it we initiate iRODS w iinit and after authentication, extract the data with:
imeta qu -z seq -d study_id = 7537 > imeta_output.txt. 

The data is downloaded and the results are pushed to `/results/sequence_data`

We will rename the files to be the sample identifier in order to make downstream processing easier to reference. This names will of the form `isogutXXX` which is pulled from the bam SM tag. These are the Sanger names that will be corresponding to the manifest and to the nextflow input table.

### Primer Removal

Removal of primers and identification of barcodes is performed using lima
