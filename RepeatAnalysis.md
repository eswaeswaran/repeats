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


# GENERATE DE NOVO REPEAT LIBRARY OF GREAT TIT 

Script for RepeatModeler2:

```bash
rm -r /vol/storage/Eswaran/Classification_Repeats/Scripts
mkdir /vol/storage/Eswaran/Classification_Repeats/Scripts
nano /vol/storage/Eswaran/Classification_Repeats/Scripts/Abel-RepeatModel2DFAM3.7.bash
====================================================================
rm -r /vol/storage/Eswaran/Classification_Repeats/GreatTits
mkdir /vol/storage/Eswaran/Classification_Repeats/GreatTits
mkdir /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatModeler2



#Make Database
cd /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatModeler2
zcat /vol/storage/Eswaran/Classification_Repeats/RawData/Great_Tits/GCF_001522545.3_Parus_major1.1_genomic.fna.gz > /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatModeler2/Abel-GCF_001522545.3_Parus_major1.1_genomic.fna
#Build Database
/home/ubuntu/Programs/RepeatModeler-2.0.4/BuildDatabase -engine ncbi -name Abel-GCF_001522545.3_Parus_major1.1_genomic /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatModeler2/Abel-GCF_001522545.3_Parus_major1.1_genomic.fna

#RepeatModeler
/home/ubuntu/Programs/RepeatModeler-2.0.4/RepeatModeler -threads 28 -database Abel-GCF_001522545.3_Parus_major1.1_genomic -engine ncbi -genomeSampleSizeMax 243000000 -LTRStruct

rm -r /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatModeler2/RM_*
echo 'Job Complete'
====================================================================
mkdir /vol/storage/Eswaran/Classification_Repeats/Scripts/Submissions
chmod +x /vol/storage/Eswaran/Classification_Repeats/Scripts/Abel-RepeatModel2DFAM3.7.bash
/vol/storage/Eswaran/Classification_Repeats/Scripts/Abel-RepeatModel2DFAM3.7.bash &> /vol/storage/Eswaran/Classification_Repeats/Scripts/Submissions/Abel-RepeatModel2DFAM3.7.bash.out &


```


#  REPEAT ANNOTATION 
On de novo database for Great Tit
Script for RepeatMasker2

```bash
nano /vol/storage/Eswaran/Classification_Repeats/Scripts/Abel-RepeatMaskerRM2.0.4DFAM3.7Aves.bash
====================================================================
rm -r /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker
mkdir /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker

cd /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker
cp /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatModeler2/Abel-GCF_001522545.3_Parus_major1.1_genomic-families.fa /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/Abel-GCF_001522545.3_Parus_major1.1_genomic-families.fa  
zcat /vol/storage/Eswaran/Classification_Repeats/RawData/Great_Tits/GCF_001522545.3_Parus_major1.1_genomic.fna.gz > /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna
/home/ubuntu/Programs/RepeatMasker/RepeatMasker -e rmblast -gccalc -s -a -pa 28 -lib /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/Abel-GCF_001522545.3_Parus_major1.1_genomic-families.fa  /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna  

GENOMESIZE=`grep -v ">" /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna | perl -pe -chomp | wc -m`

perl /home/ubuntu/Programs/RepeatMasker/util/calcDivergenceFromAlign.pl -s /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna.divsum -a  /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna.GC-Adjusted.align /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna.align
perl /home/ubuntu/Programs/RepeatMasker/util/createRepeatLandscape.pl -div /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/GCF_001522545.3_Parus_major1.1_genomic.fna.divsum -t "Great Tit (Abel) Repeat Landscape" -g $GENOMESIZE > /vol/storage/Eswaran/Classification_Repeats/GreatTits/RepeatMasker/Abel-GCF_001522545.3_Parus_major1.1_repeat_landscape.html
echo 'Job Complete'
====================================================================
chmod +x /vol/storage/Eswaran/Classification_Repeats/Scripts/Abel-RepeatMaskerRM2.0.4DFAM3.7Aves.bash
/vol/storage/Eswaran/Classification_Repeats/Scripts/Abel-RepeatMaskerRM2.0.4DFAM3.7Aves.bash &>/vol/storage/Eswaran/Classification_Repeats/Scripts/Submissions/Abel-RepeatMaskerRM2.0.4DFAM3.7Aves.bash.out &
exit


```















