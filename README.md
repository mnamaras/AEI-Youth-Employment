# AEI-Youth-Employment

I was curious about analyzing youth employment before and after the release of ChatGPT, and used public data from IPUMS, the Anthropic Economic Index, and the O*NET database to answer a few key questions.
This was motivated by a large number of my peers being concerned about the skills they are learning, and if they were applicable in work settings as AI becomes more integrated in the workplace. 

A written report is in progress.

## What this project asks
1. What do employed 22-25 year old U.S. college graduates work in, and how exposed are their occupations to AI?
2. How much of that exposure is automation-style vs. augmentation-style Claude usage?
3. How did young graduates' occupational choices change before and after ChatGPT (late 2022)?
4. Have outcomes diverged for high-exposure occupations since late 2022?

## Main findings
- Average occupation exposure is 0.43 for ages 22-25 and 0.45 for ages 30-55.
- About half of exposure is automation-style Claude usage and half is augmentation-style.
- No statistically detectable shift in young graduates' share of employment in
  high- vs. low-exposure occupations after 2022 (difference-in-differences and event study).

See `main.pdf` for the full output and 'Rough report.pdf' for a written analysis.

## Limitations
- Exposure and AEI describe occupations, not seniority within them.
- AEI covers about 10% of O*NET tasks and measures Claude usage, not the share of a job made of AI tasks.
- The sample is employed graduates only, so hiring and unemployment effects are not captured.
- Yearly CPS samples are small, so confidence intervals are wide.

## How to run it
1. Install R packages: ipumsr, dplyr, tidyr, stringr, readxl, ggplot2, sandwich, lmtest.
2. Download the data listed below into a `data/` folder.
3. Open `AEI-Youth-Employment.Rproj`, then knit `main.Rmd`.

## Data
| Dataset | Source | Used for | In this repo? |
|---------|--------|----------|---------------|
| IPUMS CPS microdata | https://cps.ipums.org | Who works where, survey weights | No (IPUMS terms). Extract settings below |
| LLM exposure scores (`occ_level.csv`) | https://github.com/openai/gpts-are-gpts | Occupation exposure (dv_rating_beta) | Yes |
| Anthropic Economic Index | https://huggingface.co/datasets/Anthropic/EconomicIndex | Automation vs. augmentation share | No (too large). File used: aei_claude_ai_2026-06-26.csv |
| O*NET Task Ratings | https://www.onetcenter.org/database.html | Task-weighted robustness check | No, download separately |
| BLS 2010-2018 SOC crosswalk | https://www.bls.gov/soc/ | Linking occupation codes | Yes |
| Census 2002-2011 occupation crosswalk | https://www.census.gov | Linking SOC to Census codes | Yes |

### IPUMS extract
Create a free IPUMS account and build an extract with:
- Samples: See cps_00003.xml and cps_00004.xml
- Variables: YEAR, AGE, EDUC, EMPSTAT, OCC, OCC2010, WTFINL, ASECWT
- `cps_00003.xml` (monthly, ages 22-25 and 30-55) and `cps_00004.xml` (yearly March ASEC, 2016-2026) describe the extracts used.

## Files
- `main.Rmd`: all analysis code (Q1-Q4)
- `main.pdf`: rendered output
- `*.png`: key figures

## Citations
- IPUMS CPS: cite as IPUMS asks (see cps.ipums.org for the current citation).
- Eloundou et al., "GPTs are GPTs."
- Anthropic Economic Index.
- O*NET database.
- Claude (Sonnet 5.5) was used to clean up, organize, and debug R code
