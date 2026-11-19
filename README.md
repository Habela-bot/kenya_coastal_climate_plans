# kenya_coastal_climate_plans
Assessing gender and youth commitments in climate action plans in Kenya coastal counties.
Capstone project for the YSE Environmental Data Science Certificate.
# Project Description
Coastal communities in Kenya depend heavily on climate-sensitive livelihoods such as fishing, tourism and natural resources, and women and youth play key roles in them. Each county sets out its climate priorities in a County Climate Change Action Plan, which guides how the county spends climate finance, including funds under the national Financing Locally Led Climate Action (FLLoCA) program. This project assesses whether the plans of Kenya’s coastal counties describe women and youth only as vulnerable groups, or go beyond that to make concrete commitments to include them as participants and leaders, and where the plans could become more inclusive. 
Research Questions
1.	**How often do county climate plans mention women, gender, and youth?**
2.	**How are women and youth described: as vulnerable groups, beneficiaries, or active participants and leaders?**
3.	**When plans mention women and youth, do they include specific details such as actions, targets, timelines, budgets, or responsible offices?**
4.	**How do these patterns differ across counties?**

Scope: six coastal counties (Mombasa, Kilifi, Kwale, Lamu, Tana River and Taita-Taveta), mainly their County Climate Change Action Plans for 2023–2027.

## Data
  	
File	Description	Source
## Data

| File | Description | Source |
|------|-------------|--------|
| `raw_data/kenya_census_2019_age_sex_county.csv` | Population by single year of age, five-year age group, sex, county and sub-county, for all 47 counties | Kenya National Bureau of Statistics, 2019 Kenya Population and Housing Census, Volume III, Table 2.3; accessed through the rKenyaCensus R package (table `V3_T2.3`), saved as CSV in November 2026 |
| `clean_data/census_2019_coastal_counties_clean.csv` | One row per coastal county: male, female and total population, the percentage of women (`women_percentage`), the number of youth aged 18–34 (`youth`) and the percentage of youth (`youth_percentage`) | Made by `scripts/1_data_clean.ipynb` |
| County Climate Change Action Plans, 2023–2027 *(To be uploaded)* | PDF plans for each county, to be turned into a table of text passages and keyword counts | County governments, through the Council of Governors Maarifa Centre |
## Repository structure

```
kenya_coastal_climate_plans/
├── README.md                    ← project description (this file)
├── raw_data/                    ← original data, never edited
│   └── kenya_census_2019_age_sex_county.csv
├── clean_data/                  ← output of 1_data_clean.ipynb
│   └── census_2019_coastal_counties_clean.csv
├── figures/                     ← plots and tables (coming in later scripts)
└── scripts/                     ← notebooks, numbered in the order they run
    ├── 0_project_setup.ipynb
    └── 1_data_clean.ipynb
```
# How to run the code
All scripts are Google Colab notebooks written in R. Run them in number order:

1. **scripts/0_project_setup.ipynb creates the project folder and subfolders in Google Drive.**
2. **scripts/1_data_clean.ipynb reads the raw census file, keeps the six coastal counties, and writes clean_data/census_2019_coastal_counties_clean.csv.**
3.**scripts/2_analysis.ipynb (coming soon) will make summary tables and charts of women and youth by county.**

Each notebook mounts Google Drive with one Python cell (drive.mount()), then switches to the R runtime.
## Data cleaning steps (1_data_clean.ipynb)
1.**Kept the six coastal counties with filter() and %in%. The raw file covers all 47 counties.**

2.**Kept whole-county rows only (SubCounty == "ALL"). The file also has a row for each sub-county, and the ALL row is their sum, so keeping both would count every person twice.**

3.**Took each county's population by sex from the Age == "Total" row, kept the columns I need with select(), and added the percentage of women with mutate().**

4.**Counted youth aged 18–34, the definition in Kenya's constitution. I used filter(), group_by() and summarise() on the single-age rows 18 to 34 only, because the Age column also contains five-year age groups and totals that would count people more than once.**

5.**Joined the two tables with left_join() by county, and added the percentage of youth with mutate().**

6.**Saved the result to clean_data/ with write_csv().**

## Known data issues:
1. **County names are in capitals in the raw file, and Taita-Taveta is written TAITA/ TAVETA (a slash and a space). Filters must use this exact spelling.**
2. **The Total column is male plus female. The small number of intersex people counted in the census is not in this table.**
3. **Mombasa has a Climate Action Plan for 2023–2050, so its plan is a different type from the other five.**
## Status and next steps
- [x] Set up the project folder and GitHub repository

- [x] Clean the census data for the six coastal counties

- [ ] Summary tables and a bar chart of women and youth by county

- [ ] upload the six county climate action plans and check that their text can be extracted
## AI Disclosure
I used chat to help me edit parts of the README, for example ticking the boxes, making my text bold and how to insert a table.

write README
