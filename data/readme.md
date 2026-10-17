# Source Data and Setup

This project uses the **2023 adult wave of IACOFI**, the Bank of Italy's survey on financial literacy and digital financial skills in Italy.

The source dataset contains **4,862 respondents aged 18–79** and **219 variables**.

## Downloading the dataset

1. Visit the [Bank of Italy's official survey page](https://www.bancaditalia.it/statistiche/tematiche/indagini-famiglie-imprese/alfabetizzazione/index.html?com.dotmarketing.htmlpage.language=1).
2. In the **2023 Survey** section of the English page, select **Database - STATA**.
3. Extract the downloaded archive and locate `Database_ENG.dta`.
4. Preserve the original filename and file contents. Do not open and re-save the source file using another statistical application.

Official resources:

- [2023 English Stata dataset](https://www.bancaditalia.it/statistiche/tematiche/indagini-famiglie-imprese/alfabetizzazione/Database_STATA_EN.zip?language_id=1)
- [2023 data description and questionnaire](https://www.bancaditalia.it/statistiche/tematiche/indagini-famiglie-imprese/alfabetizzazione/Data-description-2023.pdf?language_id=1)

## File location

Place the extracted file in the location required by your execution environment:

| Environment | Expected path |
|---|---|
| Local Jupyter | `data/raw/Database_ENG.dta`, relative to the repository root |
| Google Colab | `My Drive/The_Confidence_Trap/data/raw/Database_ENG.dta` in your own Google Drive |

Create the `raw` directory if it does not exist. The notebook creates the remaining working directories during execution.

## Input validation

Before starting the analysis, the notebook checks the source file against the registered input.

| Property | Expected value |
|---|---|
| Filename | `Database_ENG.dta` |
| File size | 1,365,604 bytes |
| Number of rows | 4,862 |
| Number of columns | 219 |
| SHA-256 checksum | `aded6652c0e6e200bd1b31090096c5a5d082f916a5dc8a666fe0e4ced71c583a` |

These checks help ensure that the analysis uses the same source data as the documented project.

If a newly downloaded file has a different checksum, investigate whether the publisher has updated the dataset. Do not bypass the validation without understanding the difference.

## Access and redistribution

The anonymised microdata are distributed by the Bank of Italy for research purposes, subject to the conditions stated on its website.

Download the dataset directly from the publisher and consult those conditions before use.

This repository does not include:

- The original microdata.
- Respondent-level processed datasets.
- Respondent-level analytical checkpoints.

The notebook retains aggregate tables and figures so that readers can inspect the methodology and reported results without downloading the microdata.
