# isogut
Initial processing, quality control and analysis of long-read sequencing data. The location of these scripts and data is on:
`/lustre/scratch126/humgen/projects/isogut`

## Raw Sequence Data

The raw long-read sequencing data is on iRODS under project ID 7537. To retrieve it we initiate iRODS w iinit and after authentication, extract the data with:
imeta qu -z seq -d study_id = 7537 > imeta_output.txt. 

The data is downloaded then with the script `./get_files.sh`.  This will download all bams to the `./sequence_data`
