---
title: "A Dual-Population Algorithm Based on Self-Adaptive Epsilon Method for Constrained Multi-Objective Optimization"
collection: publications
category: manuscripts
permalink: /publication/2024-saecmo/
excerpt: 'Proposes SaE-CMO, a cooperative dual-population evolutionary algorithm with a self-adaptive epsilon constraint-handling method for constrained multi-objective optimization problems (CMOPs).'
date: 2024-01-01
venue: 'Information Sciences'
paperurl: 'https://doi.org/10.1016/j.ins.2023.119906'
citation: '<b>S. Song</b>, K. Zhang, L. Zhang, and N. Wu, "A dual-population algorithm based on self-adaptive epsilon method for constrained multi-objective optimization," <i>Information Sciences</i>, vol. 655, Art. no. 119906, Jan. 2024.'
---

- **Authors:** Shiquan Song (first author), Kai Zhang, Ling Zhang, Ni Wu
- **Venue:** *Information Sciences*, vol. 655, article 119906, January 2024
- **DOI:** [10.1016/j.ins.2023.119906](https://doi.org/10.1016/j.ins.2023.119906)
- **Code:** MATLAB implementation on the PlatEMO platform, [github.com/LingZ0/SaECMO](https://github.com/LingZ0/SaECMO)
- **BibTeX:** [song2024saecmo.bib]({{ '/files/song2024saecmo.bib' | relative_url }})

## Summary

In constrained multi-objective optimization problems (CMOPs), a search that over-emphasizes either convergence or feasibility can fail to approximate the constrained Pareto front well.

The paper proposes **SaE-CMO**, a cooperative dual-population evolutionary algorithm:

- A **main population** and an **auxiliary population** exploit promising solutions from both feasible and infeasible regions.
- A **self-adaptive epsilon method** handles constraints. Each population applies a different comparison criterion when selecting survivors from the shared mating pool.
- The auxiliary population keeps solutions that are well constrained but poorly converged. This preserves information about both the constrained and the unconstrained Pareto fronts and helps the main population maintain diversity.

SaE-CMO was compared with state-of-the-art constrained multi-objective evolutionary algorithms on three benchmark test suites and four real-world CMOPs, and it performed better than the compared algorithms in the reported experiments.

## My contribution

I am the first author of this article. I implemented the algorithm in MATLAB on the PlatEMO platform; the code is publicly available in the repository above.
