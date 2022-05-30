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

  1. **Block 1** => *IMFdocsDownloader* (private) Rpackage:  API for the download of IMF reports [repository](https://github.com/manuelbetin/IMF_Report_API)
  2. **Block 2** => *CCDr* (public) Rpackage: Toolbox for NLP processing [repository](https://github.com/ComplexCrisesDb/CCDr)
  3. **Block 3** => CCDB (private) source code for the update the database [repository](https://github.com/ComplexCrisesDb/CCD_Financelab)

![](inst/project_documentation/images/R_folder_example.png)

Block 1 and Block 2 are independent packages that includes respectively the functions to download the last IMF country reports metadata from the IMF website and the function used to compute the NLP extractions on the reports.

Block 3 uses the country reports downloaded and perform the NLP necessary to update the CCDB dataset.

### Block 1: The *IMFdocsDownloader*

The IMFdocsDownloader package provide the functions to query the metadata for the IMF reports. the code perform a query on the following IMF [webpage](https://www.imf.org/en/Publications/Search?series=IMF%20Staff%20Country%20Reports&when=During&year=2021)

![](inst/project_documentation/images/imf_webpage_api_example.png)

You can install the package running the following command in RStudio

```R
library(devtools)
devtools::install_github("manuelbetin/IMFdocsDownloader")
```

The output of the code is a dataset containing the metadata necessary for the download of the reports. It includes the title of the document, the summary of the report document, the date of publication and the url. This dataset is used as input for the function scrap.ccdr.files() in the CCDr package that formally download the pdfs of the reports.

To properly work the functions of the package **IMFdocsDownloader** use RSelenium and need a number of configuration steps. please refer to the documentation of the package for more details.

The function **imfAPI.geturls()** perform the query for the selected year and return a
dataset containing the necessary information for the download of the reports.

### Block 2: The *CCDr* package

The CCDr package is a Toolbox to extend the *Complex Crises Database* (CCD) the underlying data of the paper:

- Manuel Bétin, Umberto Collodel. The Complex Crises Database: 70 Years of Macroeconomic Crises. 2021. https://halshs.archives-ouvertes.fr/halshs-03268889/ Find more info and download the database and raw text files from https://doi.org/10.7910/DVN/CN0PR9


The CCDr package is available for download on github ([here](https://github.com/ComplexCrisesDb/CCDr)) and has a dedicated website ( [here](https://complexcrisesdb.github.io/CCDr/articles/CCDr_introduction.html)), you can fork and contribute to include updates and/or corrections. Do not hesitate to open issues ([here](https://github.com/ComplexCrisesDb/CCDr/issues)) to propose new avenues for work or highlight errors.

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
Using the dataset of metadata from **Block 1** the CCDr package allows for:

- The download of the pdf of the country reports
- The compilation of the corpus of country reports into a usable list of text
- The extraction of relevant transcripts corresponding to specific categories of crisis
- The extraction of the term frequencies of the available categories of crisis

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

The corpus refers to the collection of text documents that underline the NLP. At the stage of the
project the corpus is composed of 22,000 country reports from the International Monetary Fund for the
period 1950-2021.

- The pdf files of the corpus for the update is store in the following folder: "inst/rawdata/corpus/files"

- The aggregate corpus can be found in the folder: "inst/rawdata/corpus/corpus"

#### dictionary

The dictionary is the collection of keywords identified and classified in different categories of crisis

The existing dictionary contains 20 crisis categories. For details about the construction of the lexicon
please refer to the working paper (XXX)

To access the existing dictionary use the following code:

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

This project is financed by the FinanceLab at PSE and aimed at the dissemination of improvement of the complex crises database (CCDB). Most of the work is available on open source and contributions and use of the data are open to researchers interested.
The development team in charge of continuing the development is based on the financeLab at the Paris school of Economics.  

Most of the documentation and codes are available on github on the dedicated repositories. Forks of the different blocks of the project are recommanded to keep track of the changes and ensure the compatibility with existing code.  

## Authors and acknowledgment

Special thanks to Umberto Collodel that has largely contributed to the creation of the database and the coding of many of the blocks of the project.

## License


## Project status

The project is currently in development, improvements and updates in the source code and the database are expected to be published by Septembre 2022.
