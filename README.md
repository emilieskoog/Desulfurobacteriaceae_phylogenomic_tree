# README
#### Here you can find my workflow for creating a phylogenomic tree of different Desulfurobacteriaceae. This tutorial is how I aligned and built a tree of 10 bacterial genomes that I pulled from NCBI/ had sequenced.

> Note: This is a phylogenomic tree tutorial (aligning whole genomes based on marker genes), NOT aligning single proteins of interest.

#### Another quick note before starting, this program is 'safe' to run locally (on your computer). It is not that large of a program and aligning and building a phylogenomic tree for 10 genomes only takes a few minutes. 

## :computer: Alignment using GToTree

GToTree was created by the awesome Mike Lee. Please check out his detailed explanation for how to install and use GToTree [here](https://github.com/AstrobioMike/GToTree). 

### 1. Create GToTree Environment

```
conda create -y -n gtotree -c conda-forge -c bioconda -c astrobiomike gtotree
```
### 2. Activate GToTree Environment

```
conda activate gtotree
```

### 3. Create text file with all fasta files listed

You can do this by placing all genome files in one folder. Enter into that folder ('cd' into it from terminal). Then execute:

```
ls *.fa > fasta_files.txt
```
This will take all files with the extension `.fa` and put their names into a text file called `fasta_files.txt`.

If your files have a different extension, make sure to reflect that with the `*.fa` (can change to *.fasta, etc.)

### 4. Run GToTree

Again, make sure you have activated your environment. Then execute:
```
GToTree -f fasta_files.txt -H Bacteria \
        -t -o Desulfurobacteria
```

(Read the GToTree [user manual](https://github.com/AstrobioMike/GToTree) for details on flags, etc, and cater to your data.)

### 5. Visualize tree: PART 1

GToTree will output a file with the extension `.tre`. In this case, because I declared that my output would be named Desulfurobacteria (as per my `-o Desulfurobacteria` flag), the outputted file of interest is called `Desulfurobacteria.tre`. You can take this bad boy directly to [ITOL (Interactive Tree of Life)](https://itol.embl.de/) and it's upload page ([here](https://itol.embl.de/upload.cgi)) and drag and drop that file to view your tree.

### 6. DETOUR: Build tree with IQTree

Now, by default, GToTree uses the alignment program Muscle and uses the program FastTree to take that alignment and build the tree. You can change these parameters if you'd like. I decided to use IQTree to biuld the tree instead of FastTree.

I am actually not sure if IQTree is already built into GToTree. You can go ahead and try by running the step below and if it's confused then you need to install IQTree. I already had IQTree so I conda activated my IQTree environment (because I was too lazy to potentially get errors) and executed the following below: 

But first, you need to find 2 files for inputting to IQTree. These are the `Aligned_SCGs.faa` and `Partitions.txt` (in the `run_files` folder) files that were outputted from our previous step.

```
iqtree -s Aligned_SCGs.faa \
       -spp run_files/Partitions.txt \
       -m MFP -bb 1000 -nt 4 -pre iqtree_out
```

### 7. Visualize tree: PART 2

If you did runn IQTree and have nmade it here, then our golden tree file will be whichever file has the `.treefile` extension. In my case here, it is called `iqtree_out.treefile`. I put this file into FigTree which is how I personally view my trees but you can use your preferred tree-viewing software, such as [ITOL](https://itol.embl.de/upload.cgi) (mentioned earlier)!