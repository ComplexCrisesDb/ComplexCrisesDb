<!-- badges: start -->
[![Lifecycle: experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)

# Complex Crises database (CCDB), Finance Lab, PSE

Update and Maintenance of the complex crises database by the Finance Lab (Paris School of Economics)

## Project Description 

The administrator of the two repositories is the github account ComplexCriseDb administrated by Manuel Bétin. To contribute to the project please fork the project [instruction](https://docs.github.com/en/get-started/quickstart/fork-a-repo) and contribute following the git guidelines  [instruction](https://docs.github.com/en/get-started/quickstart/contributing-to-projects). 

### General overview and structure of the project

#### Structure of the project

The structure of the project is structure to mimic the file structure used for development of [R package](https://r-pkgs.org/). 

![](inst/project_documentation/images/root_folder_example.png)

---------------

#### Data

**data** folder contain the vintages of the CCDB dataset with the appropriate version name ( [check coding conventions here](https://blog.codinghorror.com/whats-in-a-version-number-anyway/))

![](inst/project_documentation/images/data_folder_example.png)

--------------- 

#### Inst

**inst** folder contain different subfolders with diverse objectives

![](inst/project_documentation/images/inst_folder_example.png)

  - **rawdata** contain unstructured and raw data
  - **git_documentation** contain documentation to use git
  - **project_documentation** contains documentation on the CCDB project
  - **issues** contains the issues exported from github at different timespan 

-----------------

#### R

**R** folder contains the codes used throughout the project it is compose of the three git repositories

  1. **Block 1** => IMF_Report_API (private)Automatic collection of IMF reports [repository](https://github.com/manuelbetin/IMF_Report_API)
  2. **Block 2** => CCDr (public)Toolbox for NLP processing [repository](https://github.com/ComplexCrisesDb/CCDr)
  3. **Block 3** => CCDB (private) workflow for update the database [repository](https://github.com/ComplexCrisesDb/CCD_Financelab)
  
![](inst/project_documentation/images/R_folder_example.png)

Block 1 and Block 2 are independent of each others and includes respectively the codes to download the last IMF country reports from the IMF website and the code use to compute the NLP extractions.

Block 3 relies on the corpus downloaded from block 1 and the codes to extract the indices from block 2.

### Block 1: The *IMF_Report_API*

The IMF_report_API is a short code that allows for the automatic download of the last IMF reports. the code perform a query on the following IMF [webpage](https://www.imf.org/en/Publications/Search?series=IMF%20Staff%20Country%20Reports&when=During&year=2021)

![](inst/project_documentation/images/imf_webpage_api_example.png)

The output of the code is a dataset containing the metadata necessary for the download of the reports. It includes the title of the document, the document, the date and the url. This dataset is used as input for the function scrap.ccdr.files() in the CCDr package.

To properly work the IMF API requires a number of configuration steps. please refer to the specific [README](R/IMF_Report_API/README.html) for more details on the necessary steps

The dataset is saved in the following folder: "inst/rawdata/corpus/IMF_urls" and is name according to the date of export. i.e "imfreport_api_export2022-04-08.csv"

In case of manual download of the reports this step can be omitted and the files used for the corpus directly stored in "inst/rawdata/corpus/files" with the appropriate name ( [conventions]() )


### Block 2: The *CCDr* package 

The CCDr package is a Toolbox to extend the *Complex Crises Database* (CCD) the underlying data of the paper: 

- Manuel Bétin, Umberto Collodel. The Complex Crises Database: 70 Years of Macroeconomic Crises. 2021. https://halshs.archives-ouvertes.fr/halshs-03268889/ Find more info and download the database and raw text files from https://doi.org/10.7910/DVN/CN0PR9


The CCDr package is available for download on github ( [here](https://github.com/ComplexCrisesDb/CCDr)) and has a dedicated website ( [here](https://complexcrisesdb.github.io/CCDr/articles/CCDr_introduction.html)), you can fork and contribute to include updates and/or corrections. Do not hesitate to open issues ([here](https://github.com/ComplexCrisesDb/CCDr/issues)) to propose new avenues for work or highlight errors. 

You can install the package running the following command in RStudio

```R
library(devtools)
devtools::install_github("ComplexCriseDb/CCDr")
```

You can have more information and details on the package in the dedicated website ( [CCDr](https://complexcrisesdb.github.io/CCDr/)) or run the following code in R:

```R
library(CCDr)
help(CCDr)
```

### Block 3: The *CCDB* repository

The CCD_FinanceLab repository is the repository use to update the database and is composed of 4 main sub-blocks. 
(You can refer to the [README.md](R/CCD_Financelab/README.html) of the repository for more details)

1. Corpus ([Guidelines for corpus](R/CCD_Financelab/1.CCDB_corpus/README.html))

2. dictionary ([Guidelines for dictionary](R/CCD_Financelab/2.CCDB_dictionary/README.html))

3. Extraction ([Guidelines for Extraction](R/CCD_Financelab/3.CCDB_extraction/README.html))

4. output ([Guidelines for output](R/CCD_Financelab/4.CCDB_output/README.html))

Each block corresponds to a subpart of the following diagram

![](inst/project_documentation/images/CCDB_Workflow.png)

#### Corpus

The pdf files of the corpus for the update is store in the following folder: "inst/rawdata/corpus/files"

The aggregate corpus can be found in the folder: "inst/rawdata/corpus/corpus"

#### dictionary

Check the exising dictionary using the following code:

```R
library(CCDr)

# names of existing categories of crises

ccdr.lexicon() %>% names()

# keywords included in the lexicon

ccdr.lexicon_details("Severe_recession")

# create new category for the lexicon

my_new_lexicon=list(Recession=c("severe economic crisis",
                                "Severe recession",
                                "severe crisis"))
```

------------------

## Installation



## Usage


## Support

Contact: 
- Manuel Betin (manubetin@gmail.com): Administrator
- Martin Kessler (martin@findevlab.onmicrosoft.com): contributor

## Roadmap

- set up of the project based on the existing codes and documentation provided in the Phd Sovereign crises and animal spirits: A narrative of 70 years of Macroeconomic crisis, 2022, Manuel Bétin. 

- Create a production environment for the update of the dataset based on the methodology developed in the original paper.

- Update and improvement of the download of corpus to ensure rapid and automatic download of relevant documents (#next-steps)

- Update and improvement of the lexicon and the scope of indices developed (#next-steps)

- Create visualisation and explotation of the data into dashboard or surveillance metrics (#next-steps)

## Contributing

This project is financed by the FinanceLab at PSE and aimed at the dissemination of improvement of the complex crises database. Most of the work is available on open source and contributions and use of the data are open to researchers interested. 
The development team in charge of continuing the development is based on the financeLab at the Paris school of Economics.  

Most of the documentation and codes are available on github on the dedicated repositories. Forks of the different blocks of the project are recommanded to keep track of the changes and ensure the compatibility with existing code.  


## Authors and acknowledgment

Special thanks to Umberto Collodel that has largely contributed to the creation of the database and the coding of many of the blocks of the project. 

## License


## Project status

The project is currently in development, improvements in the source code and the database are expected to be published by Septembre 2022. 

## Getting started with git

To make it easy for you to get started with github, here's a list of recommended next steps.

- [Git instructions](inst/git_documentation/git_instructions_short.html)
- [Git install](inst/git_documentation/install.html)
- [Git project setup](inst/git_documentation/project-setup.html)
- [Git workflow](inst/git_documentation/workflow.html)


```
#create a new branch called "my-branch" and switch to it

git checkout -b my-branch

#make edits to your scripts, save then commit

git add  one-script.R another-script.R
git commit -m "example of commit message"

# push your changes in "my-branch" to the repository
git push -u origin my-branch

#in the github repository go to the repository and create a merge request
#once the changes have been merged, switch back to master and pull the changes

git checkout master
git pull

```


