---
layout: article
titles:
  en      : &EN       Conda installation and use
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN
key: page-Conda
---

The power of UNIX shell for bioinformatics is that many programs have been created for analyses, which we can then run in our UNIX shell terminal (e.g. RAxML-NG for phylogenetic analyses). <br />

Many of these programms can be installed from source but this can be very tedious and difficult. Package managers exist to help with this, with the most common UNIX one being [conda](https://docs.conda.io/projects/conda/en/latest/index.html). <br />

Here we will cover how to install conda, install the advanced manager mamba within conda, create environments and install programs

## Installing conda
Conda must be installed on your UNIX system before you can download and use any packages. It has two flavours: miniconda which is a basic, lightweight instalation and anaconda which comes with more pre-installed packages. <br />
The instructions for installing the latest version of conda can be found on the [documents page](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html). Select your operating system from the list and install the relevant conda package, following the instructions carefully.<br />
If installed correctly, you should see `(base)` at the start of your prompt in your terminal.<br />
**NOTE** Many conda packages do not come for the Windows version of conda. It is highly recommended you use a Linux or Mac computer for bioinformatics analyses. 


## Installing and using mamba
Mamba is a re-implemented version of conda which allows for quicker downloads, better error messages and a smooth installation process for packages. It works within the conda environment and is installed in your base environment (i.e. you see `(base)` at the start of your temrinal) with the following command
```console
conda install mamba -n base -c conda-forge
```
After this, you can use mamba anywhere that you see conda in instructions (e.g. `conda install` becomes `mamba install`)


## Keeping conda up to date
Conda and related packages often get updated regularly so it is good to keep your packages up to date. The following command updates all packages in an environment
```console
mamba update --all
```

#Using environments
Many packages will use the same dependancies (other packages needed to run) and the versions or installations may conflict with each other, creating issues. It is **strongly** suggested that you install workflows or even individual programs in their own environments. <br />
You can create an environment named 'test' like so
```console
mamba create -n test
```
Once created, we can activate the environment like so
```console
mamba activate test
```
You will see the start of your terminal prompt now changes from `(base)` to `(test)`.<br />
You can deactivate (go back to (base)) with the following command
```console
mamba deactivate
```

## Installing packages
Conda has a lot of packages available, especialyl for bioinformatics analyses, The easiest way to find these is through google (i.e. google 'conda package name').<br />
Many of the bioinformatics packages are stored online in the bioconda channel, which you must state when installing the package. For example, lets install the package MAFFT (multiple alignment software) in our test environment.<br />
First ensure your test environment is active using the commands above (you should see `(test)` at the start of your terminal prompt). Then execute this command:
```console
mamba install -c bioconda mafft
```
This will download MAFFT and all associated dependancies. Once finished, the program is ready to use. You can uninstall if needed by typing 
```console
mamba uninstall mafft
```



