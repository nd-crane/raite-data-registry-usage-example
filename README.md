# This is a usage example for importing the RAITE dataset

## Requirement

DVC is required to import the RAITE dataset. You can find instructions [here](https://dvc.org/doc/install) to install DVC.

If you use PDM to manage Python packages, after cloning this repo, you can have DVC by running this command:

```bash 
pdm update
```


## Usage

Once you have DVC installed in your environment, 
you can use the RAITE data registry repository [https://github.com/nd-crane/raite-data-registry](https://github.com/nd-crane/raite-data-registry) to list, import, and download the datasets used in the RAITE. See examples in the next sections.

*Remember:* You don't need to clone this repository for that.

### **Listing data**

To explore the currently available datasets of this DVC repository, you can run the `dvc list` command over the folder `data` as follows:

```bash
dvc list https://github.com/nd-crane/raite-data-registry data/
```

To view the content of a particular dataset in the registry, you can run the `dvc list` with `-R` and specify the dataset name in the data folder. 
For example, to list the content of the initial crane dataset, you can run the following command:

```bash
dvc list -R https://github.com/nd-crane/raite-data-registry data/raite_2023
```

### **Data import workflow**
You can import a specific dataset from the registry by running the `dvc import` command. It is analogous to using direct download tools like wget (HTTP).
For example, to import the initial crane dataset, you can run the following:

```bash
# Only in the first time
dvc init
```

```bash
dvc import  https://github.com/nd-crane/raite-data-registry data/raite_2023
```

Besides downloading the data, `dvc import`  saves information about the dependency that the local project has on the data source (the raite-data-registry repo).
In that case, DVC generates a special import `.dvc` file containing such dependency information. In the previous example, the generated file is `raite_2023.dvc`.

Whenever the dataset changes in the registry, you can bring data up to date with the `dvc update` command followed by the name of the generated `.dvc` file. For example, to update the initial crane dataset, you can run the following:
```bash
dvc update raite_2023.dvc
```

### **Data downloads**
You can download a specific dataset from the registry by running the `dvc get` command. It uses the same syntax as the `dvc import` command but doesn't save the dependency information.

To obtain the initial crane dataset, execute the following command for downloading:

```bash
dvc get  https://github.com/nd-crane/raite-data-registry data/raite_2023
```



*Note*: When using pdm, add `pdm run` at the beginning of the DVC commands.

 
