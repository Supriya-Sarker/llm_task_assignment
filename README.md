# LLM Task Assignment with Minimum-Cost Network Flow

Course project, Network Optimization (University of Arkansas, Fall 2026).

## Problem
Assign a batch of independent tasks to heterogeneous LLM agents within one processing window. Each task goes to exactly one eligible agent, and each agent has a task-count capacity (for example, an API quota). The goal is to minimize total expected cost, which combines price and the expected cost of wrong answers.

## Model
- **Network:** source -> tasks -> agents -> sink, solved as a **min-cost flow** problem with **Google OR-Tools**.
- **Arc cost:** `c_ij = p_ij + lambda * (1 - a_ij)`, where `p_ij` is the estimated price of agent *j* on task *i*, `a_ij` is its estimated accuracy from a calibration set, and `lambda` is the dollar penalty per wrong answer.
- **Constraints:** every task is assigned once, only to eligible agents, and agent capacities are respected.
- **Baselines:** greedy assignment (random order and most-restricted-first).

## Data
Built on **RouterBench** (Hu et al., 2024): real prompts from standard benchmarks with recorded correctness and cost for 11 LLMs. Accuracy and price estimates come from a calibration split, and assignments are evaluated on a held-out split with real outcomes.

## Experiments
Varying batch size, capacity tightness, eligibility thresholds, task mix, and `lambda`, plus sensitivity to errors in the accuracy estimates. Metrics are total cost, realized errors, accuracy, feasibility, and runtime, compared against the greedy baselines.

## Status
In progress. Code, data extracts, and results will be added here as each step is completed.

## Tech
Python, Google OR-Tools, pandas, NumPy, Matplotlib, pytest
