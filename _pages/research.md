---
permalink: /research/
title: "Research"
author_profile: true
---

This page separates three things: research I have **completed**, topics I am **currently interested in**, and **future directions** I have not yet worked on.

## Completed research

### Constrained multi-objective evolutionary optimization (Master's research, 2021–2024)

Many real-world optimization problems have several conflicting objectives and must also satisfy constraints. These are constrained multi-objective optimization problems (CMOPs). In this setting, an algorithm that focuses too much on feasibility can get stuck in parts of the feasible region, while one that focuses too much on convergence can miss the constrained Pareto front.

In my master's research I proposed **SaE-CMO**, a cooperative dual-population evolutionary algorithm:

- **Two cooperating populations.** A main population and an auxiliary population exploit promising solutions from both feasible and infeasible regions.
- **Self-adaptive epsilon constraint handling.** Each population applies a different comparison criterion to select survivors from a shared mating pool.
- **Preserving diversity.** The auxiliary population keeps solutions that are well constrained but poorly converged. This retains information about both the constrained and the unconstrained Pareto fronts.
- **Evaluation.** SaE-CMO was compared with state-of-the-art constrained multi-objective algorithms on three benchmark test suites and four real-world CMOPs, and it performed better than the compared algorithms in the reported experiments.
- **Implementation.** MATLAB on the PlatEMO platform. The code is public at [github.com/LingZ0/SaECMO](https://github.com/LingZ0/SaECMO).

Publication: [*Information Sciences*, vol. 655, 119906, 2024]({{ '/publication/2024-saecmo/' | relative_url }}).

**Topics covered:** evolutionary computation · constrained multi-objective optimization · constraint-handling techniques · cooperative multi-population search · empirical benchmarking of optimization algorithms.

## Current interests

These are topics I am reading about and would like to study more deeply. They are **not** completed work.

- **Optimization algorithms more broadly**, beyond population-based heuristics, including the operations research view of modelling and solving constrained problems.
- **Data-driven optimization**, where models learned from data inform or accelerate the optimization process.
- **AI for optimization**, for example using learning-based components inside optimization algorithms.

My industry experience with large data pipelines and with constraining language-model outputs through a semantic layer gives me practical motivation for these questions. It is engineering experience, not optimization research.

## Future directions (not yet started)

I have not yet chosen a specific PhD topic. Areas I am considering include:

- Operations research and optimization
- Evolutionary computation
- Data-driven optimization
- The intersection of AI and optimization

I will refine these directions as I read more of the literature and talk with potential supervisors.
