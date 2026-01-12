This repository contains the files to reproduce the replication and extension analysis (STATA). 
The workflow is modular: three component datasets are processed separately and then merged into a final master dataset used for all analyses.

## Repository layout
- data/ — component and final datasets (see list below)
- dofiles/ — STATA scripts (cleaning, construction, master analysis)
- docs/ — project report, guide to do-files, checksums, etc.
- README.md — this file

## Data files (component datasets + final)
Expected filenames:
- data/economic_outcomes_final.dta  
  Contains household economic variables (maternal labor supply, business profits, income).
- data/child_outcomes.dta  
  Child-level metrics (childcare enrollment, attendance, IDELA developmental scores).
- data/others.dta  
  Supplementary outcomes (spousal labor supply, household well-being, other secondary metrics).
- data/outcomes_dfinal.dta  
  Final master dataset produced by merging the three component datasets; used for all final analyses.

## Do-files / workflow
The analysis is performed with a set of STATA scripts. Run the master script to reproduce results.

Main scripts (expected/representative names):
- dofiles/outcomes_economic_final_changes.do  
  Cleans and constructs variables for the economic dataset.
- dofiles/child_outcome.do  
  Cleans and prepares child-level variables.
- dofiles/replication_oth_outcomes.do  
  Master analysis script — this script:
  1. Cleans the "Other Outcomes" data.
  2. Merges the three component datasets into `data/outcomes_dfinal.dta`.
  3. Performs final preparation (rescaling/standardization, winsorizing).
  4. Runs the econometric analysis: replication of the original paper and the heterogeneity extension (Childcare × Baseline IDELA).

To run (example, from project root) in Stata:
1. Open Stata and set the working directory to the repository root.
2. In the Stata command window or do-file editor:
   do dofiles/replication_oth_outcomes.do

## Notes & requirements
- Stata (specify version used; e.g., Stata 15/16/17) and any user-written packages required by the do-files. At the top of each do-file, required packages should be listed (e.g., `ssc install ...`).
- Use relative paths in do-files (as above) so scripts run from the project root.
- If datasets are large, consider using Git LFS or provide a release/Zenodo link instead of committing very large binaries.

## Contributions / responsibilities
- Author: anousha-singh-20  
- I was responsible for the `others` (outcome_others) cleaning and the master analysis (merging, final prep, and econometric scripts).
