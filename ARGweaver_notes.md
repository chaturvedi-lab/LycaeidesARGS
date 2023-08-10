These are my notes to run ARGweaver (https://github.com/mdrasmus/argweaver/) on the UofU CHPC for the lycaedies data processing. 

# 1. Installation
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
