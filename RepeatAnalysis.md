# Generate a de novo repeat library using RepeatModeler2

Script for RepeatModeler2:

```bash
rm -r /path/to/your/scripts
mkdir /path/to/your/scripts
nano /path/to/your/scripts/scriptname.bash
====================================================================
rm -r /path/to/your/species
mkdir /path/to/your/species
mkdir /path/to/your/species/RepeatModeler2

#Make Database
cd /path/to/your/species/RepeatModeler2
zcat /path/to/genome/species_genomic.fna.gz > /path/to/your/species/RepeatModeler2/species_genomic.fna
#Build Database
/path/to/Programs/RepeatModeler-2.0.4/BuildDatabase -engine ncbi -name species_genomic
/path/to/your/species/RepeatModeler2/species_genomic.fna

#RepeatModeler
/path/to/Programs/RepeatModeler-2.0.4/RepeatModeler -threads 28 -database species_genomic -engine ncbi -genomeSampleSizeMax 243000000 -LTRStruct

rm -r /path/to/your/species/RepeatModeler2/RepeatModeler2/RM_*
echo 'Job Complete'
====================================================================
mkdir /path/to/your/scripts/Submissions
chmod +x /path/to/your/scripts/scriptname.bash
/path/to/your/scripts/scriptname.bash &> /path/to/your/scripts/scriptname.bash.out &
exit

```

#  Repeat Annotation using RepeatMasker2
On de novo database 
Script for RepeatMasker2

```bash
nano  /path/to/your/scripts/scriptname.bash
====================================================================
rm -r /path/to/your/species/RepeatMasker
mkdir /path/to/your/species/RepeatMasker

cd /path/to/your/species/RepeatMasker
cp  /path/to/your/species/RepeatModeler2/species_genomic-families.fa /path/to/your/species/RepeatMasker/species_genomic-families.fa  
zcat /path/to/genome/species_genomic.fna.gz > /path/to/your/species/RepeatMasker/species_genomic.fna
/path/to/Programs/RepeatMasker/RepeatMasker -e rmblast -gccalc -s -a -pa 28 -lib /path/to/your/species/RepeatMasker/species_genomic-families.fa     /path/to/your/species/RepeatMasker/species_genomic.fna

GENOMESIZE=`grep -v ">"  /path/to/your/species/RepeatMasker/species_genomic.fnaa | perl -pe -chomp | wc -m`

perl /path/to/Programs/RepeatMasker/util/calcDivergenceFromAlign.pl -s
/path/to/your/species/RepeatMasker/species_genomic.fna.divsum -a
/path/to/your/species/RepeatMasker/species_genomic.fna.GC-Adjusted.align
/path/to/your/species/RepeatMasker/species_genomic.fna.align
perl /path/to/Programs/RepeatMasker/util/createRepeatLandscape.pl -div
/path/to/your/species/RepeatMasker/species_genomic.fna.divsum -t "Species Name Repeat Landscape" -g $GENOMESIZE > /path/to/your/species/RepeatMasker/species_repeat_landscape.html
echo 'Job Complete'
====================================================================
chmod +x  /path/to/your/scripts/scriptname.bash
 /path/to/your/scripts/scriptname.bash &>  /path/to/your/scripts/scriptname.bash.out &
exit


```















