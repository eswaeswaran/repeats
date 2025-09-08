# DOWNLOADING BIRD GENOMES
Reference genome of great tit from ncbi: GCF_001522545.3_Parus_major1.1.
Script for downloading the reference genome for great tits (Abel) with additional annotations.

```bash
rm -r /vol/storage/Eswaran/Classification_Repeats/RawData/Great_Tits
mkdir /vol/storage/Eswaran/
mkdir /vol/storage/Eswaran/Classification_Repeats
mkdir /vol/storage/Eswaran/Classification_Repeats/RawData
mkdir /vol/storage/Eswaran/Classification_Repeats/RawData/Great_Tits

rsync --recursive --times --verbose rsync://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/001/522/545/GCF_001522545.3_Parus_major1.1/ /vol/storage/Eswaran/Classification_Repeats/RawData/Great_Tits
```

Script for downloading genomes for outgroup birds (blue tit and ground tit).
```bash
rm -r //vol/storage/Eswaran/Classification_Repeats/RawData/Outgroup_Birds
mkdir /vol/storage/Eswaran/Classification_Repeats/RawData/Outgroup_Birds

wget -O /vol/storage/Eswaran/Classification_Repeats/Outgroup_Birds/RawData/GCF_000331425.1_PseHum1.0_genomic.fna.gz //vol/storage/Eswaran/Classification_Repeats/RawData//Outgroup_Birds https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/331/425/GCF_000331425.1_PseHum1.0/GCF_000331425.1_PseHum1.0_genomic.fna.gz
wget -O /vol/storage/Eswaran/Classification_Repeats/RawData//Outgroup_Birds/cyaCae2.fa http://public-genomes-ngs.molgen.mpg.de/CYANISTES/cyaCae2.fa
gzip -9 /vol/storage/Eswaran/Classification_Repeats/RawData//Outgroup_Birds/cyaCae2.fa
echo 'Job Complete'
```

Script for downloading genomes for outgroup birds - BLACK CAPPED CHICKADEE (Poecile atricapillus).
```bash
rsync --recursive --times --verbose rsync://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/030/490/865/GCF_030490865.1_bPoeAtr1.hap1/ /vol/storage/Eswaran/Classification_Repeats/RawData/Outgroup_Birds
```

Script for downloading genomes for outgroup birds - PITTA SORDIDA (HOODED PITA).
```bash
rsync --recursive --times --verbose rsync://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/013/390/025/GCA_013390025.1_ASM1339002v1/ /vol/storage/Eswaran/Classification_Repeats/RawData/Outgroup_Birds
```

Script for downloading genomes for outgroup birds - NEOPELMA CHRYSOCEPHALUM (SAFFRON-CRESTED TYRANT_MANAKIN).
```bash
rsync --recursive --times --verbose rsync://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/003/984/885/GCA_003984885.2_ASM398488v2/ /vol/storage/Eswaran/Classification_Repeats/RawData/Outgroup_Birds
```
