# Team FDA Drugs

Code and data for examining teams associated with FDA Orange Book patents and
related scientific papers. The repository includes descriptive tables,
regression results, and Python/R notebooks.

## Included data

| File | Contents |
| --- | --- |
| `Data/patent_data_control.parquet` | 56,799 patent-level records |
| `Data/paper_data_control.parquet` | 353,194 paper-level records |
| `Data/Reg_results/reg_1–4_patents.csv` | Patent regression tables |
| `Data/Reg_results/reg_1–4_papers.csv` | Paper regression tables |
| `Data/T_test_*.xlsx` | Statistical result workbooks |

The Parquet tables include paper/patent identifiers, `is_orange`, year,
reference/team counts, first/last-author attributes, team diversity, and impact
measures. Patent impact fields include `cit_pct`, `xi_real`, `num_claims`, and
`cd`; paper fields include `citpct`, `CD`, `is_oa`, and `fund`. Geographic distance
is stored as `distance`; entropy fields describe institutional, country,
field, career-age, and gender diversity.

## Workflow

| Notebook | Analysis |
| --- | --- |
| `Fig_1_patent.ipynb` | Patent descriptive distributions and regression figures |
| `Fig_2_paper.ipynb` | Paper descriptive distributions and regression figures |
| `Fig_3_map_patent.ipynb` | Inventor geography and patent collaboration maps |
| `Fig_4_map_paper.ipynb` | Scientific institutions and paper collaboration maps |
| `R reg.ipynb` | Patent/paper fixed-effects regression tables |

The default `data_dir` is `Data`; the default `regression_dir` is
`Data/Reg_results`. Map workflows use the study's Orange Book, PatentsView,
and SciSciNet-derived tables. Cartopy uses its Natural Earth data cache for
geographic rendering.

Run the regression notebook with R/IRkernel and R packages `arrow`, `fixest`,
and `dplyr`. `FDA_REGRESSION_DIR` selects the prepared regression-table directory
(default `data/regression`). `FDA_REGRESSION_OUTPUT_DIR` selects the destination
(default `outputs/regression`). The notebook checks the fields used by each
model before fitting. To plot the resulting regression tables, point
`regression_dir` at that destination.

## Installation and configuration

Use Python 3.10 or 3.11 with Matplotlib 3.9 or newer within major version 3.
Create and activate a virtual environment with the command for your operating
system, then install the packages:

```bash
python -m venv .venv
python -m pip install -r requirements.txt
```

Copy `config.example.json` to `config.json`. Set `data_dir` to the study-data
directory and `output_dir` to the figure destination. Repositories with regression
figures also use `regression_dir` for regression tables. Relative paths resolve
from the repository root; absolute paths are accepted. `RESEARCH_CONFIG` selects
another configuration file.

Start `jupyter lab` inside the repository and open the desired notebook. Each
Python notebook includes its own initialization and data loading. The output
directories are created automatically. R entry points use the environment
variables described in their workflow sections.

## Source validation

```bash
python scripts/check_sources.py
```

This command validates Python syntax, notebook JSON, configuration JSON, and
empty notebook execution state. The GitHub Actions workflow performs the same
static checks, including R parsing when R is available. R entry points use an
R installation and their listed packages.

## Citation and license

See `CITATION.cff` for repository metadata and cite the associated research.
The MIT license covers code and documentation. Data, publications, and
third-party materials retain their respective source rights.
