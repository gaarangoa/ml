FROM gaarangoa/ml:stable 

RUN wget https://raw.githubusercontent.com/bcbio/bcbio-nextgen/master/scripts/bcbio_nextgen_install.py
RUN python bcbio_nextgen_install.py /usr/local/share/bcbio --tooldir=/usr/local --genomes GRCh37 --aligners bwa --aligners bowtie2