---
permalink: /about/
title: "About"
author_profile: true
---

## Background

I studied mechanical engineering as an undergraduate and then completed a master's degree in Computer Science and Technology at Wuhan University of Science and Technology (2021–2024). My master's research was in computational intelligence, specifically evolutionary algorithms for **constrained multi-objective optimization**. The main outcome is a first-author article in *Information Sciences* that proposes a dual-population evolutionary algorithm with a self-adaptive epsilon constraint-handling method (see [Publications]({{ '/publications/' | relative_url }})).

After graduating in 2024, I joined a state-owned enterprise in Beijing as an R&D engineer. I have worked there for about two years and three months.

## Data platform and AI application work

My industry work has moved through three stages:

1. **Reporting automation.** Early work focused on automating recurring reports and reducing manual data processing.
2. **Data platform engineering.** I took part in migrating the company's data warehouse from a Kettle/DataX/MySQL setup to a lakehouse built on Apache Flink, Apache Paimon and StarRocks, with DolphinScheduler for dependency-driven orchestration. My work covered technical research and proposals, deployment and operation of the platform components, and the data-development pipeline from the raw (ODS) layer to the application (ADS) layer. A team lead set the technical direction and approved the design. ([Project page]({{ '/projects/lakehouse-migration/' | relative_url }}))
3. **Internal AI applications.** I built Light-ChatBI, an internal natural-language data analysis assistant. Its central design choice is to let a privately deployed language model interpret the question and select metrics, while SQL is generated deterministically from a semantic layer. ([Project page]({{ '/projects/light-chatbi-data-agent/' | relative_url }}))

Alongside these projects I have worked on data quality checks, column-level data lineage and forecasting-model experiments.

## Research background and future interests

I separate what I have done from what I would like to do:

- **Completed research:** design of a constraint-handling strategy and a cooperative dual-population search for constrained multi-objective evolutionary optimization, evaluated against state-of-the-art algorithms on benchmark suites and real-world problems.
- **Current interests:** how data-driven and AI methods can support optimization algorithms, and how optimization can be applied to problems that arise in data systems.
- **Not yet started:** I have not yet chosen a PhD topic. Directions I am considering include operations research, optimization, evolutionary computation and data-driven optimization. I have not carried out research in reinforcement learning, mathematical programming or stochastic optimization.

See [Research]({{ '/research/' | relative_url }}) for more detail.
