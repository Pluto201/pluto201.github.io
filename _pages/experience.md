---
permalink: /experience/
title: "Experience"
author_profile: true
---

## Industry

### R&D Engineer, state-owned enterprise, Beijing
*July 2024 – present*

I work on the company's data platform, data engineering and internal AI applications. The work has moved from reporting automation, to data platform engineering, to AI applications that reduce manual data work.

- **Reporting automation.** Automated recurring reports to reduce manual data processing.
- **Lakehouse migration.** Took part in migrating the data warehouse from Kettle/DataX/MySQL to a Flink, Apache Paimon and StarRocks lakehouse orchestrated by DolphinScheduler. I was responsible for technical research and proposals, platform deployment and operation, and the data pipelines from the ODS layer to the ADS layer. The total daily warehouse update time fell from over 4 hours to about 2 hours, and the scheduled-task failure rate fell from about 10% to about 7% (one-month observation after go-live). [Project details]({{ '/projects/lakehouse-migration/' | relative_url }})
- **Light-ChatBI data agent.** Built an internal natural-language data analysis assistant on StarRocks, with a semantic layer (first a custom YAML layer, later Cube Core), SQL audit, table-level permissions and a task queue. [Project details]({{ '/projects/light-chatbi-data-agent/' | relative_url }})
- **Data governance.** Worked on rule-based data quality checks and on column-level data lineage based on SQL abstract-syntax-tree parsing and graph modelling.
- **Machine learning practice.** Ran forecasting-model experiments as part of internal data applications.

## Education

### Master's degree in Computer Science and Technology
*Wuhan University of Science and Technology, China · September 2021 – June 2024*

- Research area: computational intelligence, specifically evolutionary computation and constrained multi-objective optimization.
- First-author article in *Information Sciences* (2024). [Details]({{ '/publication/2024-saecmo/' | relative_url }})
- First-Class Academic Scholarship, 2021–2022 academic year.

### Bachelor's degree in Mechanical Engineering
*Wuhan University of Science and Technology, China · September 2017 – June 2021*

## Skills

- **Programming:** Python, SQL, Java, MATLAB
- **Data platforms:** Apache Flink (including Flink CDC), Apache Paimon, StarRocks, DolphinScheduler, Hadoop (HDFS, YARN), Hive
- **Data governance:** data quality checks, data lineage, metric definition management
- **AI data applications:** data agents, text-to-SQL, semantic layers, SQL validation
- **Optimization (research):** multi-objective evolutionary algorithms, epsilon-based constraint handling, cooperative multi-population search, benchmark-based algorithm comparison
