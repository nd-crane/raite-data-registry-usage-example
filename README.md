# This is a usage example for importing the RAITE dataset

## Installation Requirements

DVC is required to import the RAITE dataset. You can find complete instructions [here](https://dvc.org/doc/install) on how to install DVC.

If installiong with conda it is recommeneded to set your default solver as libmamba. You can find instructions [here](https://www.anaconda.com/blog/conda-is-fast-now) on installing and setting your default solver as libmamba. Alternatively, you can also following the DVC installation instructions and install mamba within your dvc envirnoment.

### Testing

#### Installing with conda (libmamba default solver):

**Local storage**
```bash
conda install -c conda-forge dvc
```

**Remote storage**
```bash
conda install -c conda-forge dvc-ssh
```

**Google Drive**
```bash
conda install -c conda-forge dvc-gdrive
```

##### Installing with conda (libmamba not default solver):

**Mamba solver for faster solves**
```bash
conda install -c conda-forge mamba
```

**Local storage**
```bash
mamba install -c conda-forge dvc
```

**Remote storage**
```bash
mamba install -c conda-forge dvc-ssh
```

**Google Drive**
```bash
mamba install -c conda-forge dvc-gdrive
```

###### Installing with Pip:

**Local storage**
```bash
pip install dvc
```
**Remote storage**
```bash
pip install dvc[ssh]
```
**Google Drive**
```bash
pip install dvc[gdrive] 
```

Or, if you use PDM to manage Python packages, after cloning this repo, you can have DVC by running this command:

```bash 
pdm update
```
## Directory Requirements

If you plan to use DVC in conjunction with a SSH connection to the CRC a local configuration file must be set-up to establish your username. 


Run the following command to set-up a local file. Replace '<CRC user>' with your CRC user.

```bash 
dvc remote modify --local cvrl_remote user <CRC user>
```

## Usage

Once you have DVC installed in your environment, 
you can use the RAITE data registry repository [https://github.com/nd-crane/raite-data-registry](https://github.com/nd-crane/raite-data-registry) to list, import, and download the datasets used in the RAITE. Please take a look at the examples in the following sections.

*Remember:* You don't need to clone this repository for that.

### **Listing data**

To explore the currently available datasets of this DVC repository, you can run the `dvc list` command over the folder `data` as follows:

```bash
dvc list https://github.com/nd-crane/raite-data-registry data/
```

To view the content of a particular dataset in the registry, you can run the `dvc list` with `-R` and specify the dataset name in the data folder. 
For example, to list the content of the initial crane dataset, you can run the following commands:

```bash
dvc list -R https://github.com/nd-crane/raite-data-registry data/raite_2023 # from within a CRC machine
```



### **Data downloads**
You can download a specific dataset from the registry by running the `dvc get` command. It is analogous to using direct download tools like wget (HTTP).

To obtain the raite2023 dataset with the videos from the matches, execute the following command for downloading:

```bash
dvc get  https://github.com/nd-crane/raite-data-registry data/raite_2023/cleaned_matches
```

If you don't have access to CRC machines at the University of Notre Dame, add the flag `--remote` to specify `gdrive` as a remote location. See the example below.
```bash
dvc get --remote gdrive https://github.com/nd-crane/raite-data-registry data/raite_2023/cleaned_matches
```

### **Data import**
You can import a specific dataset from the registry by running the `dvc import` command. 
It uses the same syntax as the `dvc get` command but saves the dependency information.
You must also be in a directory that is git repo and initialize the dvc environment before using the import dvc command.

For example, to import the raite2023 dataset (saving the dependencies), you can run the following:

```bash
# Only in the first time

# (optional) Initialize Git only if you are inside a folder that is not currently a Git repository
git init 

# Initialize dvc repo
dvc init
```
Finally, run the dvc import command:
```bash
dvc import https://github.com/nd-crane/raite-data-registry data/raite_2023/cleaned_matches
```
Again, if you cannot access CRC machines at the University of Notre Dame, you must add the flag `--remote gdrive` to the previous command. 
Note: In addition to downloading the data, `dvc import` saves information about the local project's dependency on the data source (the raite-data-registry repo).
DVC generates a special import `.dvc` file containing such dependency information in that case. 
The generated file is `cleaned_matches.dvc` in the previous example.

Whenever the dataset changes in the registry, you can bring data up to date with the `dvc update` command followed by the name of the generated `.dvc` file.\
For example, to update the raite 2023 cleaned_matches dataset, you can run the following:
```bash
dvc update cleaned_matches.dvc
```


*Note*: When using pdm, add `pdm run` at the beginning of the DVC commands.

If you encounter any problems, please don't hesitate to reach out to Priscila Moreira at pmoreira@nd.edu.

 
