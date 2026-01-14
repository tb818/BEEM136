=================================================================================================================================================================================
README: Replication Package for “Legal Aid Provision in England & Wales”
=================================================================================================================================================================================

Tom Burrows (tb818)
BEEM136 – Research Methods
University of Exeter
January 2026

Project available at: https://github.com/tb818/BEEM136

=================================================================================================================================================================================
OVERVIEW
=================================================================================================================================================================================
This replication package cleans and analyses a local-authority-by-quarter panel dataset of civil legal aid provision across England and Wales from 2010–2019. The materials include all data cleaning operations, dataset construction, summary statistics, map generation, and econometric modelling. All steps are executed using the Jupyter notebook titled:

beem136_tb818_legal_aid_ew.ipynb

Running this notebook from start to finish produces all cleaned datasets, figures, regression tables, and intermediate files referenced in the project.

This README has been produced in line with guidance provided by Vilhuber et al. (2022).

=================================================================================================================================================================================
FILE STRUCTURE AND REPRODUCTION
=================================================================================================================================================================================
Software requirements:
Python 3.10 or higher
Jupyter Notebook (constructed in VS Code)
Git, Git Bash, Git LFS (run: git lfs install)

To obtain the data, run the following in Git Bash (other terminals may require syntax alteration):
# Enter cd
cd YOUR_DIR

# Clone repository. See below for dealing with fatal message.
git clone https://github.com/tb818/BEEM136

# Navigate to folder
cd YOUR_DIR/BEEM136

# Create and activate virtual environment for packages
python -m venv .venv
source .venv/Scripts/activate

# Install specified Python packages. This may take some time.
pip install -r requirements.txt

Then, open beem136_tb818_legal_aid_ew.ipynb as a Jupyter Notebook and amend the project root to the relevant working directory. Subsequent paths are well-defined.
The code can now be executed using the .venv kernel (VS Code/Jupyter may require a restart).

If successful, this should yield the following file structure:

BEEM136/
│
├── .venv/                              # Python virtual environment (NOTE: ignored by .gitignore, requires regeneration on each working directory)
├── cleaned_data/                       # Cleaned dataset
├── graphics/                           # Graphics with subfolders
│   ├── summary_stats/
│   ├── time_series/
│   ├── unique_providers_maps/
│   ├── deserts_maps/
│   └── violins/
├── raw_data/                           # Input files (not supplied in Git repo)
├── regressions/                        # Output .tex regression tables
│
├── .gitignore                          # To ignore .venv/
├── .gitattributes                      # To specify graphics/ and raw_data/ to be stored in Git LFS
├── requirements.txt                    # Package requirements for reproducibility
├── README (this file)
└── beem136_tb818_legal_aid_ew.ipynb    # Jupyter Notebook code

There should be in raw_data/
                        legal-aid-statistics-civil-completions-provider-area-data-to-mar-2024.csv
                        Local_Authority_District_(2022)_to_Local_Authority_District_(2023)_Lookup_for_EW.csv
                        raw_census_2011_populations.csv
                        raw_census_2011_ages.csv
                        raw_census_2011_economic_activity.csv
                        raw_census_2011_housing_tenure.csv
                        raw_census_2011_ethnicity.csv
                        census_la_converter.csv
                        inflation_data.csv
                        rural_urban_categories.csv
                        LAD_DEC_2023_UK_BFC.shp
                        LAD_DEC_2023_UK_BFC.shp
                        LAD_DEC_2023_UK_BFC.cpg
                        LAD_DEC_2023_UK_BFC.dbf
                        LAD_DEC_2023_UK_BFC.prj
                        LAD_DEC_2023_UK_BFC.shx

Due to an acknowledged issue with Git's 'defense in depth', the licensed version of Git from the University of Exeter may print a fatal error message cloning Git repositories using LFS (see https://github.com/git-lfs/git-lfs/issues/5749). Extensive testing has not found this to be an issue. The following steps are therefore unnecessary but included as an optional robustness check to kill the hook and re-checkout:

# Enter cd
cd YOUR_DIR

# Clone repository
git clone https://github.com/tb818/BEEM136

# Killing the hook
cd /c/YOUR_DIR/BEEM136
rm .git/hooks/post-checkout
git restore --source=HEAD :/

=================================================================================================================================================================================
DATA AVAILABILITY AND PROVENANCE
=================================================================================================================================================================================
The replication package relies on publicly available external datasets and additional datasets generated entirely within the provided code.

All external datasets are freely available for download by the replicator. They are also available on Github. If downloaded, they should be placed inside the folder raw_data/, and named as below. All sources listed below are publicly accessible without registration.

### a. Legal Aid Dataset
File name: legal-aid-statistics-civil-completions-provider-area-data-to-mar-2024.csv
Access: UK Ministry of Justice
https://assets.publishing.service.gov.uk/media/667bfbf84ae39c5e45fe4caf/legal-aid-statistics-civil-completions-provider-area-data-to-mar-2024.zip 
Usage: Primary dataset. Used for data on legal aid case evolution and supporting analysis.
Summary: Content on legal aid cases completed, by year-quarter and local authority, from 2008 to 2024.

### b. ONS 2011 Census Data
Files: raw_census_2011_populations.csv; raw_census_2011_ages.csv; raw_census_2011_economic_activity.csv; raw_census_2011_housing_tenure.csv; raw_census_2011_ethnicity.csv
Access: ONS/NOMIS Web Viewer
        populations: https://www.nomisweb.co.uk/census/2011/ks101ew         > Type of area > local authorities: district / unitary (prior to April 2015)
        ages: https://www.nomisweb.co.uk/census/2011/ks102ew                > Type of area > local authorities: district / unitary (prior to April 2015)
        economic_activity: https://www.nomisweb.co.uk/census/2011/ks601uk   > Type of area > local authorities: district / unitary (prior to April 2015)
        housing_tenure: https://www.nomisweb.co.uk/census/2011/ks402ew      > Type of area > local authorities: district / unitary (prior to April 2015)
        ethnicity: https://www.nomisweb.co.uk/census/2011/ks201ew           > Type of area > local authorities: district / unitary (prior to April 2015)
Usage: Socioeconomic covariates merged to each local authority.
Summary: Time-invariant measures across a range of variables in 2011 local authorities, including total population, age distribution, economic status, housing status, and ethnicity.

### c. Rural–Urban Classification
File: rural_urban_categories.csv
Access: ONS
        https://www.ons.gov.uk/file?uri=/methodology/geography/geographicalproducts/ruralurbanclassifications/2021ruralurbanclassification/rucallsupplementarytables.xlsx
        Table 1E
Usage: Classification of each local authority as rural or urban.
Summary: Data on the rurality of every local authority as of 2021.

### d. LA Lookup
File: Local_Authority_District_(2022)_to_Local_Authority_District_(2023)_Lookup_for_EW.csv
Access: ONS Geoportal
        https://geoportal.statistics.gov.uk/search?q=Local_Authority_District_(2022)_to_Local_Authority_District_(2023)_Lookup_for_EW > Download > CSV
Usage: Linking updated local authority codes to local authority names.
Summary: Maps LA23CD (local authority codes) to LAD23NM (local authority names).

### e. Census-LA Converter
File: census_la_converter.csv
Access: Manually constructed from open-source ONS data, mapping old local authority codes (2011 census) to new local authority codes (all other files, including legal aid data).
Usage: Used to ensure consistency with local authorities for analysis.
Summary: Maps local authority codes across boundary changes and mergers.

### f. Inflation Data (CPIH Index)
File: inflation_data.csv
Access: ONS
        https://www.ons.gov.uk/economy/inflationandpriceindices/timeseries/l522/mm23 > Show data as: Table > Frequency: Quarter > Time period: Custom Q1 2010 Q4 2019
Usage: Used to adjust monetary amounts to constant 2015 pounds.
Summary: Index in (0,1) relating spending power in 2015 terms.

### g. Local Authority Boundary Files
Files:  LAD_DEC_2023_UK_BFC.shp
        LAD_DEC_2023_UK_BFC.cpg
        LAD_DEC_2023_UK_BFC.dbf
        LAD_DEC_2023_UK_BFC.prj
        LAD_DEC_2023_UK_BFC.shx
Access: ONS Geoportal
        https://geoportal.statistics.gov.uk/datasets/127c4bda06314409a1fa0df505f510e6_0/ > Download > Shapefile
Usage: Creation of boundary maps for desert and provider distribution figures.
Summary: Data on maps for linking with local authority codes in other datasets.

All other datasets (clean merged panels, regression inputs, generated tex files, plots) are created by the notebook and are fully included in this package. Derived datasets created by the code are included in the folder cleaned_data.

The author certifies that they have legitimate permission to use all datasets included or referenced. All datasets are publicly available. No confidential or restricted-access data are used. Redistribution of all files in this package is permitted. All external datasets used in this project are publicly accessible. None are confidential, restricted, or subject to special licensing conditions.

=================================================================================================================================================================================
OUTPUTS
=================================================================================================================================================================================
### a. Cleaned Panel
File location: cleaned_data/full_panel.csv
Summary: Datasets cleaned and merged into single panel for analysis. 
Expected dimensions: 12720 x 113

### b. Graphics
File locations: graphics
                        /desert_maps
                                        /desert_map_2010-q1.pdf
                                        /desert_map_2013-q2.pdf
                                        /desert_map_2016-q3.pdf
                                        /desert_map_2019-q4.pdf
                                        /deserts_colour_scale.pdf
                                        /ever_desert_rural_urban_legend.pdf
                                        /ever_desert_rural_urban_map.pdf
                        /summary_stats
                                        /ever_desert_summary.tex
                                        /la_cross.tex
                                        /most_frequent_LAs_high.tex
                                        /most_frequent_low_LAs.tex
                                        /quarter_summary.tex
                                        /summary_stats.tex
                                        /summary_stats_central80.tex
                                        /val_vol_providers_dist.pdf
                                        /val_vol_providers_dist_80pc.pdf
                                        /variable_dataframe.tex
                        /time_series
                                        /adj_val_by_qtr.pdf
                                        /deserts_prop_pop.pdf
                                        /unique_firms_by_qtr.pdf
                                        /val_vol_by_qtr.pdf
                                        /val_vol_cases_indexes_by_qtr.pdf
                                        /vol_by_qtr.pdf
                        /unique_providers_maps
                                        /unique_providers_2010-q1.pdf
                                        /unique_providers_2013-q2.pdf
                                        /unique_providers_2016-q3.pdf
                                        /unique_providers_2019-q4.pdf
                                        /unique_providers_colour_scale.pdf
                        /violins
                                        /subset_violin_adjusted_la_total_value_by_quarter.pdf
                                        /subset_violin_la_total_volume_by_quarter.pdf
                                        /subset_violin_la_val_vol_by_quarter.pdf
                                        /subset_violin_unique_providers_by_quarter.pdf
                                        /violin_adjusted_la_total_value_by_quarter.pdf
                                        /violin_la_total_volume_by_quarter.pdf
                                        /violin_la_val_vol_by_quarter.pdf
                                        /violin_unique_providers_by_quarter.pdf
Summary: Maps of legal aid local authority deserts, summary statistic .tex files and figures, time series figures across variables, maps of unique providers per local authority, and violin distributions.
Expected files: 36

### c. Regressions
File locations: regressions
                            /model1_panel.tex
                            /model1_panel_trimmed.tex
                            /model2_logit_desert.tex
                            /model3_DiD_panel.tex
                            /model3_DiD_panel_trimmed.tex
Summary: Regression outputs saved as .tex files.
Expected files: 5

=================================================================================================================================================================================
NOTES
=================================================================================================================================================================================
Tested on:
Windows 11 (no operating system-specific features required)
HP EliteBook 640 14 inch G10 Notebook PC (no specific hardware required)

The analysis uses no stochastic procedures and does not rely on random seeds.

The Notebook beem136_tb818_legal_aid_ew.ipynb is extensively commented for clarity; these will not be repeated here. An indicative order of operations is as follows:

1. Loads all external raw data.
2. Cleans and restructures legal aid provider data.
3. Constructs a balanced panel of local authority by quarter observations.
4. Merges Census, rurality, and inflation data.
5. Saves the cleaned panel as full_panel.csv.
6. Produces summary tables of providers, population, desert frequency, and covariates.
7. Creates violin plots, time-series figures, and desert maps.
8. Runs econometric models including OLS, trimmed OLS, logit models, and difference-in-differences.
9. Saves all output files into the specified directories.

=================================================================================================================================================================================
REFERENCES  
=================================================================================================================================================================================
Data cited in DATA AVAILABILITY AND PROVENANCE seciton.

Lars Vilhuber, Connolly, M., Koren, M., Llull, J., & Morrow, P. (2022). A template README for social science replication packages (v1.1). Social Science Data Editors. https://doi.org/10.5281/zenodo.7293838