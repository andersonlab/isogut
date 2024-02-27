# isogut
Initial processing, quality control and analysis of long-read sequencing data. The location of these scripts and data is on:
`/lustre/scratch126/humgen/projects/isogut`

## Pipeline

In order to run this pipeline we require nextflow to be loaded on the FARM and then run in the directoru where `isogut.nf` is located along with the sanger.config file:

`nextflow -config sanger.config isogut.nf`

For reference, the pipeline will perform the following steps:

### Download Long-Read Sequences

The raw long-read sequencing data is on iRODS under project ID 7537. To retrieve it we initiate iRODS w iinit and after authentication, extract the data with:
imeta qu -z seq -d study_id = 7537 > imeta_output.txt. 

The data is downloaded then with the script `./get_files.sh`.  This will download all bams to the `./sequence_data`

The files downloaded will be:

We will rename the files to be the sample identifier in order to make downstream processing easier to reference 

### Primer Removal

Removal of primers and identification of barcodes is performed using lima
