My working folder for this project on the UofU CHPC: /uufs/chpc.utah.edu/common/home/gompert-group4/projects/schaturvedi/lyc_args/

I copied the filtered vcf file from the main data folder to this project folder:

```bash
mkdir vcf
cp ../sc_lycaeides_data_processing_2023/Variants/morefilter_variants.vcf ./vcf/
```
We currently have 89,294 SNPs in our filtered vcf. 

I then used bcftools to get the details of all the individuals and the populations we have in the current file.

```bash
module load bcftools

#list all the individuals in the current vcf
 bcftools query -l morefilter_variants.vcf

 #count number of individuals in the current vcf
 bcftools query -l morefilter_variants.vcf | wc -l #3903

 #create a list of all the individuals in the current vcf
 bcftools query -l morefilter_variants.vcf > all_individuals.txt

 #create a list of all the populations in the current vcf
 morefilter_variants.vcf | cut -d '-' -f 1 |grep -o '[^0-9]*' | uniq > all_populations.txt #87 populations
```

SUMMARY: WE CURRENTLY HAVE 3903 INDIVIDUALS SPANNING 87 POPULATIONS AND WE HAVE CALLED 89,294 VARIANTS. 

# 1. Preparing the input file for ArgWeaver

The ARGWeaver program can only handle upto 100 individuals at a time. So I decided to subset the main vcf file to only get few individuals across all species/hybrids we currently have in the dataset. [Here] (https://docs.google.com/spreadsheets/d/1BoQ_zMOSQMFbnDQyQUjsOTpUrj0nobVzOOEQ_V504Ak/edit#gid=702836423) are the final list of individuals and populations I selected to include in this analyses.

I used vcftools to subset individuals for the final file.

# 2. Installation
I installed ARGweaver using conda to make sure I can get the package installed hastle free. Here is the installation (note this program uses Python 2.7)

```bash
module load python2.7

conda create -n argweav_env python=2.7
conda activate argweav_env
conda install -y -c genomedk argweaver

#test using code from the github website
arg-sim \
    -k 8 -L 100000 \
    -N 10000 -r 1.6e-8 -m 1.8e-8 \
    -o test1/test1

This test worked so it was successfully installed.
```
