# TAAPS
## Transforming Australia's Ability to Prevent Suicide (TAAPS) Project:
The TAAPS Project is a comprehensive, multi-phase research project funded by the Australian National Health and Medical Research Council (NHMRC). Using linked administrative health care data from the Centre for Victorian Data Linkage (CVDL) and the Australian Institute of Health and Welfare (AIHW), the TAAPS project aims to answer two key research questions:

1. What are the patterns of health services use in the year prior to, during, and following an episode of self-harm resulting in presentation to the emergency department?
2. Using dynamic systems simulation, how could the health care system be transformed to reduce self-harm and suicide rates by half within a decade?


### Background:
Globally, one person dies by suicide every 30 seconds (Meda et al., 2025). Suicide is the leading cause of premature death for Australians aged 18–44 years (Australian Bureau of Statistics, 2024), and remains a top cause of mortality in similar age groups worldwide (World Health Organization, 2025). Suicide is associated with immense economic and human costs. In Australia, suicide costs the economy over AUD$30.5 billion annually (Productivity Commission, 2020), while in the UK, it's estimated at over GBP£9.5 billion (Samaritans, 2024). The majority of these costs stem from healthcare, lost productivity, and the emotional toll on families and communities. One in five of us will loose a family member or friend to suicide during our lifetime (Andriessen et al., 2017).

Non-fatal self-harm — which includes self-injury or poisoning regardless of motivation and/or degree of suicidal intent — is a key risk factor for suicide. For every suicide, many more individuals present to emergency departments following an episode of non-fatal self-harm, but only a fraction receive either a comprehensive mental health assessement (Witt et al., 2024), and even fewer still recieve any form of mental health follow-up care (Witt et al., 2023). 

Despite decades of investment in mental health care, the proportion of individuals receiving timely, effective treatment following self-harm has not improved. Addressing this critical gap requires a system-wide understanding of health service pathways — and how these relate to future risks of self-harm repetition and/or suicide death.

### Data Sources:
The TAAPS Project utilises data linkage to combine information from a wide array of services, including:

* [Victorian Alcohol and Drug Collection (VADC)](https://www.health.vic.gov.au/funding-and-reporting-aod-services/victorian-alcohol-and-drug-collection-vadc), formally the Alcohol and Drug Information System (ADIS)
* [Clinical Public Mental Health Services (CMI/ODS)](https://www.health.vic.gov.au/research-and-reporting/cmiods)
* [Community Health Minimum Data Set (CHMDS)](https://www.health.vic.gov.au/primary-and-community-health/community-health-minimum-data-set-chmds)
* [Cause of Death Unit Record File (COD URF)](https://metadata.phrn.org.au/dataset/COD-URF-vic)
* [Medicare Benefits Schedule (MBS)](https://www.aihw.gov.au/about-our-data/our-data-collections/medicare-benefits-schedule-mbs)
* [Mental Health Community Support Services (MHCSS)](https://www.health.vic.gov.au/mental-health-services/mental-health-community-support-services)
* [National Death Index (NDI)](https://www.aihw.gov.au/about-our-data/our-data-collections/national-death-index) and [Victorian Death Index (VDI)](https://metadata.phrn.org.au/dataset/deaths-vic)
* [National Hospital Morbidity Dataset (NHMD)](https://www.aihw.gov.au/about-our-data/our-data-collections/national-hospitals-data-collection) and [Victorian Admitted Episode Database (VAED)](https://www.health.vic.gov.au/data-reporting/victorian-admitted-episodes-dataset)
* [National Non-Admitted Patient Database – Emergency Care (NNAPD-EC)](https://www.aihw.gov.au/about-our-data/our-data-collections/national-hospitals-data-collection#:~:text=The%20National%20Non-Admitted%20Patient%20Emergency%20Department%20Care%20Database,care%20in%20emergency%20departments%20in%20selected%20public%20hospitals.) and [Victorian Integrated Non-Admitted Health (VINAH)](https://www.health.vic.gov.au/data-reporting/victorian-integrated-non-admitted-health-vinah-dataset)
* [Pharmaceutical Benefits Scheme (PBS)](https://www.aihw.gov.au/about-our-data/our-data-collections/pharmaceutical-benefits-scheme)
* [Self-Harm Monitoring System for Victoria](https://pmc.ncbi.nlm.nih.gov/articles/PMC7765445/)
* [Victorian Emergency Minimum Dataset (VEMD)](https://www.health.vic.gov.au/data-reporting/victorian-emergency-minimum-dataset-vemd)

Linkage was conducted via the Australian Institute of Health and Welfare (AIHW) using the National Linkage Map, with clerical review to ensure high-quality matching.

A fuller [description of these data sources] as well as the [entity relationship diagram (ERD)](https://github.com/K-G-Witt/TAAPS/blob/main/TAAPS_EntityRelationshipDiagram.pdf) between the data sources used in this project is provided within this repo.

### Packages:
#### Patterns of health services use in the year prior to, during, and following an episode of self-harm.
Pattern mining of health care contacts in the year prior to, during, and up to one year following an episode of non-fatal self-harm resulting in presentation to the emergency department was undertaken in R for Windows. In addition to base R, the following packages were used:

* [cmprsk](https://www.rdocumentation.org/packages/cmprsk/versions/2.2-11)
* [data.table](https://www.rdocumentation.org/packages/data.table/versions/1.14.8)
* [dplyr](https://www.rdocumentation.org/packages/dplyr/versions/1.0.10)
* [haven](https://www.rdocumentation.org/packages/haven/versions/2.5.3)
* [lubridate](https://www.rdocumentation.org/packages/lubridate/versions/1.9.2)
* [nmet](https://www.rdocumentation.org/packages/nnet/versions/7.3-20/topics/nnet)
* [readr](https://www.rdocumentation.org/packages/readr/versions/2.1.4)
* [survival](https://www.rdocumentation.org/packages/survival/versions/3.5-7)
* [tidyr](https://www.rdocumentation.org/packages/tidyr/versions/1.3.0)
* [TraMineR](https://traminer.unige.ch/)

### Analyses:
#### Patterns of health services use in the year prior to, during, and following an episode of self-harm.
1. Individual linked administrative data frames were loaded into the environment and cleaned (see TAAPS_DataCleaningScript.rmd).
2. Individual data frames were merged into a master data frame by matching on personal identity numbers supplied by AIHW (see TAAPS_DataMergingScript.rmd).
3. For each person, healthcare contacts were ordered chronologically, labelled, and pattern mining was conducted (see TAAPS_PatternMiningScript.rmd).
4. Multinomial logisitc regression was conducted to identify if any demographic, clinical, and/or presentation characteristics were associated with identified health care patterns (see TAAPS_PatternMiningScript.rmd).
5. Surivial analysis modelling was conducted to identify if identified health care patterns were differentially associated with risks of death (see TAAPS_SurvivalScript.rmd).
6. Finally, competing risks modelling using the Fine-Grey model was conduucted to identify if identified health care patterns were differentially associated with risks of death by suicide as compared to all other causes of death (see TAAPS_PatternMiningScript.rmd).

### References:
Andriessen K., et al. (2017). Prevalence of exposure to suicide: A meta-analysis of population-based studies. _J Psychiatr Res_, 88: 113-20. DOI: [10.1016/j.jpsychires.2017.01.017.](https://www.sciencedirect.com/science/article/abs/pii/S0022395616304836?via%3Dihub)

Australian Bureau of Statistics. (2024). _Causes of Death, Australia_. Canberra, Australian Capital Territory: Author. [Link](https://www.abs.gov.au/statistics/health/causes-death/causes-death-australia/latest-release).
 
Meda N., et al. (2025). How many people die by suicide each year? Not 727,000: A systematic review and meta-analysis of suicide underreporting across 71 countries over 122 years. _Front Psychiatry_, 16: 1609580. DOI: [10.3389/fpsyt.2025.1609580.](https://www.frontiersin.org/journals/psychiatry/articles/10.3389/fpsyt.2025.1609580/full) 

Productivity Commission. (2020). _Mental Health: Productivity Commission Inquiry Report_. Canberra, Australian Capital Territory: Commonwealth of Australia. [Link](https://www.pc.gov.au/inquiries-and-research/mental-health-review/#final-report)

Samaritans. (2024). _The Economic Cost of Suicide in the UK_. London, UK: Author. [Link](https://www.samaritans.org/about-samaritans/research-policy/the-economic-cost-of-suicide/).

Witt K., et al. (2023). Global prevalence of psychiatric in- and out-patient treatment following hospital-presenting self-harm: a systematic review and meta-analysis. _eClin Med_, 65: 102295. DOI: [10.1016/j.eclinm.2023.102295.](https://www.thelancet.com/journals/eclinm/article/PIIS2589-5370(23)00472-8/fulltext)

Witt K., et al. (2024). Global prevalence of psychosocial assessment following hospital-treated self-harm: systematic review and meta-analysis. _Br J Psychiatry Open_, 10(1): e29. DOI: [10.1192/bjo.2023.625.](https://www.cambridge.org/core/journals/bjpsych-open/article/global-prevalence-of-psychosocial-assessment-following-hospitaltreated-selfharm-systematic-review-and-metaanalysis/898B8307745ABDC3837EBC8781FB9167)

World Health Organization. (2025). _Suicide Worldwide in 2021: Global Health Estimates_. Geneva, Switzerland: Author. [Link](https://www.who.int/publications/i/item/9789240110069).


### Additional Credits:
Flothow A., et al. (2023). Analytical methods for identifying sequences of utilization in health data: a scoping review. _BMC Med Res Methodol_, 23: 212. DOI: [10.1186/s12874-023-02019-y](https://doi.org/10.1186/s12874-023-02019-y).
