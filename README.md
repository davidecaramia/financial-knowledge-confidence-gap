# Financial Knowledge, Confidence and Behaviour

**Exploring the gap between financial knowledge and self-assessment among Italian adults.**

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![statsmodels](https://img.shields.io/badge/statsmodels-Weighted%20Logit-4051B5)](https://www.statsmodels.org/)
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/davidecaramia/financial-knowledge-confidence-gap/blob/main/notebooks/confidence_trap.ipynb)

## Overview

How closely does people's confidence in their financial knowledge reflect their tested knowledge? And how is this relationship associated with financial incidents and everyday financial behaviour?

This project investigates these questions using the **Bank of Italy's IACOFI 2023 survey**, covering **4,862 adults aged 18–79**.

The analysis combines a source-data audit, survey-weighted descriptive statistics, logistic regression, adjusted probabilities and robustness checks. Its purpose is to provide evidence that can inform financial-education outreach and content.

[Read the report](report/project_report.pdf) · [Explore the notebook](notebooks/confidence_trap.ipynb) · [Access the data instructions](data/README.md)

## Research questions

The analysis focuses on three questions:

1. How common is the mismatch between low tested financial knowledge and a more favourable self-assessment?
2. How does this mismatch vary across demographic groups?
3. Among people with low objective knowledge, how is self-assessment associated with financial incidents, purchasing behaviour and long-term financial goals?

The models estimate adjusted associations. They do not establish that confidence causes financial outcomes.

## Defining the knowledge-confidence gap

The primary mismatch indicator identifies respondents who combine:

- An **objective financial knowledge score of 3 or below out of 7**.
- A **self-assessment of average or above-average knowledge**.

The threshold follows the Bank of Italy comparison adopted in the report. Alternative definitions are examined separately.

| Population | Survey-weighted prevalence | Unweighted count |
|---|---:|---:|
| Respondents with valid knowledge and self-rating information who meet the mismatch definition | **15.1%** | 712 out of 4,453 |
| Low-knowledge respondents who rate their knowledge as average or higher | **38.7%** | 712 out of 1,607 |

These percentages use different denominators. The first describes the mismatch in the jointly observed sample; the second describes self-assessment within the low-knowledge group.

## Financial outcomes

Among respondents with low objective knowledge, adjusted outcome probabilities differ by self-rating after accounting for measured knowledge, age, gender, education and macro-region.

The primary comparison is **Average minus Low self-rating**. Differences are expressed in **percentage points**, with 95% confidence intervals.

| Outcome | Adjusted difference | 95% confidence interval | Interpretation |
|---|---:|---:|---|
| Reports at least one financial incident | **+8.2 pp** | +2.7 to +13.7 | Higher estimated probability; limited local data support |
| Carefully considers affordability before purchasing | **−9.7 pp** | −16.6 to −2.8 | Lower estimated probability |
| Sets and pursues long-term financial goals | **+5.6 pp** | −1.3 to +12.5 | Positive but inconclusive difference; limited local data support |

![Adjusted financial outcome probabilities by self-rating among low-knowledge respondents](assets/adjusted_outcome_probabilities.png)

Each model is fitted to the full available sample for its outcome. Predictions are then standardised over the corresponding low-knowledge subgroup, retaining observed knowledge scores and demographic characteristics and averaging with survey weights.

The target subgroups contain:

- **1,427 respondents** for financial incidents.
- **1,488 respondents** for careful affordability.
- **1,383 respondents** for long-term financial goals.

Open markers and daggers in the figure identify estimates with limited local data support.

## Robustness and demographic patterns

The robustness checks show that the strength of the findings depends on the outcome and specification.

- **Financial incidents:** the contrast remains positive, with confidence intervals excluding zero in all five examined specifications. Local-support warnings remain.
- **Affordability:** the contrast stays negative, but its confidence interval includes zero after income adjustment.
- **Long-term goals:** the contrast becomes clearer in income-complete samples. Much of this change is already visible before income is added as a covariate.

In the adjusted mismatch profiles, respondents with **upper-secondary education** remain the highest-probability education category.

Age rankings are less stable. The leading category changes from **30–49** in the primary model to **18–29** after income adjustment.

![Adjusted demographic patterns in the knowledge-confidence mismatch](assets/adjusted_mismatch_demographics.png)

## Implications for financial education

The results motivate three possible directions for educational outreach:

1. **Combine knowledge questions with self-assessment.** This can help identify educational needs that respondents may not recognise themselves.
2. **Link educational content to practical decisions.** Financial-risk recognition and affordability checks provide concrete starting points.
3. **Test the outreach strategy.** Compare personalised knowledge feedback with a standard invitation and measure participation, completion and subsequent decision-making.

These are proposals informed by the survey findings. Their effectiveness would need to be evaluated through a dedicated pilot.

## Analytical workflow

| Module | Main activities |
|---|---|
| **1. Analysis protocol and raw-data audit** | Register the source file, verify its checksum and dimensions, map missing-response codes and define analytical variables |
| **2. Data cleaning and variable construction** | Calculate knowledge scores, construct outcomes and covariates, and validate analytical checkpoints |
| **3. Weighted descriptive analysis** | Examine knowledge, confidence, mismatch prevalence, demographics and financial outcomes |
| **4. Adjusted models and robustness checks** | Fit weighted logistic models, estimate adjusted probabilities and contrasts, and assess sensitivity to samples and additional covariates |

The financial-outcome models include an interaction between objective knowledge and self-rating.

Inference uses **respondent-level HC1 robust covariance estimates** and **delta-method confidence intervals** for adjusted probabilities and contrasts.

The workflow includes **26 registered model specifications**, covering primary models, paired sample comparisons and sensitivity analyses.

Four models receive priority in the report:

- One model profiling the knowledge-confidence mismatch.
- Three models for the primary financial outcomes.

Shopping around for financial products is treated as a secondary outcome because it applies to a smaller, restricted population.

## Repository contents

| Path | Contents |
|---|---|
| [`notebooks/confidence_trap.ipynb`](notebooks/confidence_trap.ipynb) | Complete analysis with saved tables and figures |
| [`report/project_report.pdf`](report/project_report.pdf) | Full project report |
| [`assets/`](assets/) | Selected aggregate figures generated by the analysis |
| [`data/README.md`](data/README.md) | Dataset source, download instructions and validation information |
| [`requirements.txt`](requirements.txt) | Recorded analytical dependencies and notebook interface |
| [`docs/reproducibility.md`](docs/reproducibility.md) | Execution guidance, validation notes and publication changes |

Raw microdata and respondent-level processed files are not distributed with the repository.

Running the notebook generates working directories, analytical checkpoints, tables and figures locally or in the user's own Google Drive.

## Data source

The project uses the **2023 adult wave of IACOFI**, the Bank of Italy's Survey on Financial Literacy and Digital Financial Skills in Italy.

The source dataset contains **4,862 respondents and 219 columns**.

Download the English Stata dataset from the [Bank of Italy's official survey page](https://www.bancaditalia.it/statistiche/tematiche/indagini-famiglie-imprese/alfabetizzazione/index.html?com.dotmarketing.htmlpage.language=1), following the instructions in [`data/README.md`](data/README.md).

Keep the source filename **`Database_ENG.dta`** and preserve the original file bytes. The notebook checks the source file's checksum and dimensions before analysis.

Consult the publisher's conditions of use before working with the microdata.

## Running in Google Colab

1. Download and extract the 2023 English Stata dataset.
2. In your own Google Drive, create:

   ```text
   The_Confidence_Trap/data/raw/
   ```

3. Place `Database_ENG.dta` inside the `raw` folder.
4. Open the notebook using the Colab badge at the top of this README.
5. Connect your Google Drive when prompted.
6. Run the notebook cells sequentially.

The remaining directories are created automatically. Access to the authors' Google Drive accounts is not required.

The notebook prints the installed package versions. See [`docs/reproducibility.md`](docs/reproducibility.md) for instructions on matching the recorded analytical environment.

## Running locally

The documented local setup uses **Python 3.12**.

From the repository root, create a virtual environment:

```bash
python -m venv .venv
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

Or on Windows using PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Install the dependencies and open the notebook:

```bash
python -m pip install -r requirements.txt
jupyter lab notebooks/confidence_trap.ipynb
```

Before execution, place the source file at:

```text
data/raw/Database_ENG.dta
```

The notebook detects local execution and skips Google Drive mounting. Run all cells in order from a clean kernel, since later modules depend on objects created earlier.

Saved outputs allow the methods and results to be inspected without downloading the microdata or rerunning the models.

## Reproducibility

The accompanying validation notes document a complete local execution of the publication notebook:

- All **71 code cells** completed.
- All **26 fitted models** converged and passed the essential diagnostic checks.
- The **43 generated CSV tables** matched the previously validated results, subject to the comparison rules described in the documentation.

The notes also distinguish local validation from the Colab-specific setup, which was not retested in a live Colab session during the publication check.

See [`docs/reproducibility.md`](docs/reproducibility.md) for environment details, numerical tolerances and publication changes.

## Limitations

- **Observational design:** cross-sectional associations may reflect reverse causality or unmeasured confounding.
- **Self-assessment:** respondents rate their knowledge relative to other people. The mismatch indicators are operational definitions, not direct measurements of individual overestimation.
- **Local data support:** some self-rating and outcome combinations are supported by relatively few observations.
- **Income non-response:** including income changes the available sample, so the analysis separates sample restrictions from additional covariate adjustment.
- **Explanatory focus:** the workflow supports interpretation rather than predictive deployment. Out-of-sample classification performance was not evaluated.

## Authors and acknowledgements

Developed collaboratively by:

- [Davide Francesco Caramia](https://github.com/davidecaramia)
- [Nicolò Bachiorri](https://github.com/nicolobachiorri)
- [Hervé Mottaran](https://github.com/hervemottaran)

The work was developed for the **Data Science Lab** course at **Università degli Studi di Milano-Bicocca**, academic year **2025/2026**.

This is an independent academic project. References to the Bank of Italy and Italy's Committee for Financial Education as potential stakeholders do not imply their participation or endorsement.

Claude and ChatGPT supported coding, methodological discussion, translation, editorial revision and LaTeX formatting. The project team reviewed analytical decisions and interpretations. An AI-use declaration is also included in the submitted report.
