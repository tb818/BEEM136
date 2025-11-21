PACKAGE AND LANGUAGE VERSIONS
NOTE WHERE ALL DATASETS CAME FROM

Legal Aid – Dataset User Guide
Raw Data
x raw datasets are used. Sources appended. They are saved in:

LEGAL AID, work completed:
1.	legal-aid-statistics-civil-completions-provider-area-data-to-mar-2024.csv 
CENSUS DATA, to capture local authority descriptives for regressions:
2.	raw_census_2011_ages.csv 
3.	raw_census_2011_economic_activity.csv 
4.	raw_census_2011_ethnicity.csv 
5.	raw_census_2011_housing_tenure.csv 
6.	raw_census_2011_populations.csv 
GEOGRAPHIC MAPPING, for LA codes to names, and regions:
7.	Local_Authority_District_(2022)_to_Local_Authority_District_(2023)_Lookup_for_EW.csv 
MAPPING AND INFLATION DATA:
8.	census_la_converter.csv
9.	inflation_data.csv
SHAPEFILES, for plotting maps:
10.	Local_Authority_Districts_December_2023_Boundaries_UK_BFC_9042356933902664268 

There is one .ipynb file, in three sections: Section A cleans the raw data into full_panel.csv. Section B uses full_panel.csv to generate visual depictions. Section C uses full_panel.csv to perform statistical analysis.
The file should be run in its entirety initially/for replication. Following the creation of full_panel.csv and loading of required packages, Sections B and C may be run independently.

########## SECTION A ##########
Dataset cleaner
This cleans the legal aid and census data from 2011, saving the cleaned dataset as full_panel.csv.

The cleaned panel shows totals for:
LOCAL AUTHORITY x QUARTER

########## SECTION B ##########
Graphics Generator
This generates summary statistics and graphics using full_panel.csv, saved in:

These are:
1.	
2.	
3.	