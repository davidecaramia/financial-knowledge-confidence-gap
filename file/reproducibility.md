# Reproducibility and Execution Notes

This document describes the execution environments, validation history and publication changes associated with the analysis.

## Scope

The notebook contains the completed project analysis and retains its saved analytical outputs. Reported estimates, tables and figures are generated programmatically from the original Bank of Italy dataset.

Obtain the source data separately by following [`data/README.md`](../data/README.md).

Execution does not require access to the authors' accounts or private Google Drive folders.

## Software environment

The submitted notebook records **Python 3.13.15** and the analytical package versions listed in `requirements.txt`.

A separate local validation used **Python 3.12.14**, with the same versions of NumPy, pandas, SciPy, statsmodels, Matplotlib, PyArrow and seaborn. **Python 3.12** is the documented local setup.

JupyterLab provides the notebook interface. Its version does not enter the statistical calculations, while analytical package versions can affect fitted results, file formats and plotting behaviour.

## Google Colab setup

The first code cell mounts the user's Google Drive and uses the following project root:

```text
My Drive/The_Confidence_Trap/
```

Before execution, place the source dataset at:

```text
The_Confidence_Trap/data/raw/Database_ENG.dta
```

Colab's default environment can change. To match the recorded analytical package versions, run the following command in a temporary setup cell before executing the analysis:

```python
%pip install numpy==2.1.3 pandas==2.2.3 scipy==1.16.3 statsmodels==0.15.0 matplotlib==3.10.0 pyarrow==23.0.1 seaborn==0.13.2
```

If installation requires a runtime restart, restart it before running the notebook from the beginning.

The environment-information cell prints the installed versions for inspection.

## Local Jupyter setup

Create a Python 3.12 virtual environment and install the dependencies from `requirements.txt`.

From the repository root:

```bash
python -m venv .venv
```

Activate the environment on macOS or Linux:

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

Place the source file at:

```text
data/raw/Database_ENG.dta
```

The notebook supports execution from either the repository root or the `notebooks/` directory. It resolves the project root locally and skips Google Drive mounting outside Colab.

Run all cells sequentially from a clean kernel. Later modules depend on objects created in earlier stages.

## Documented validation

### Original analysis

The project documentation records an independent execution of the submitted analysis in an isolated local directory.

After adapting Colab authentication and redirecting the two Google Drive paths:

- All **70 analysis and setup cells** completed successfully.
- All **26 fitted models** converged and passed the essential diagnostic checks.
- The workflow produced **43 CSV tables**.
- It generated **nine figures**, each in PNG and PDF format, including the report version of the outcome-probability figure.

The primary adjusted contrasts reproduced the report:

| Outcome | Adjusted difference | 95% confidence interval |
|---|---:|---:|
| Financial incidents | +8.2 percentage points | +2.7 to +13.7 |
| Careful affordability | −9.7 percentage points | −16.6 to −2.8 |
| Long-term financial goals | +5.6 percentage points | −1.3 to +12.5 |

### Publication notebook

The accompanying validation record documents a further complete local execution on **29 September 2026**, after the notebook setup was adapted for publication.

- All **71 code cells** ran sequentially in a fresh, isolated local project.
- No cells were substituted or skipped.
- All **26 models** converged and passed the essential diagnostics.
- All **43 generated CSV tables** matched the previously validated run using `rtol=1e-12` and `atol=1e-12`.
- The `size_bytes` column in export manifests was excluded from comparison because it records file sizes rather than analytical results.
- Both supported working directories—the repository root and `notebooks/`—resolved correctly.

The Colab-specific mounting code was retained, but it was not retested in a live Colab session during this publication check.

These results document computational consistency with the specified workflow. They do not remove the statistical assumptions or interpretive limitations discussed in the report.

## Changes made for publication

The original submitted files were kept separately. The documented publication changes were limited to:

1. Updating the notebook introduction and adding execution guidance.
2. Making Google Drive mounting conditional on execution in Colab.
3. Adding local project-root resolution while preserving the Colab folder convention.
4. Reusing the project-root variable when exporting the final report figure.
5. Clearing the saved outputs of the two modified setup cells while retaining analytical outputs.
6. Removing student numbers, university email addresses and the old Google Drive link from the report's first-page author block.

All authors remain credited. The report retains its analytical content, figures, citations and AI-use declaration.

The publication changes do not alter variable definitions, model specifications, estimates, confidence intervals or analytical figure settings.

The figures included in `assets/` are copies of the validated analytical outputs.

## Generated files

Execution creates the following outputs:

| Location | Generated content |
|---|---|
| `data/processed/` | Derived respondent-level datasets and analytical checkpoints |
| `outputs/` | Tables, figures and execution metadata |

The notebook also creates working configuration files. Generated working files are excluded from version control through `.gitignore`.

Only selected aggregate figures are included in the published `assets/` directory.

## Interpreting saved outputs

The notebook's saved outputs document the submitted execution. Recorded package versions, dates and original Colab paths are historical execution information.

Readers do not need to reproduce the authors' original Google Drive paths or possess access to their accounts.
