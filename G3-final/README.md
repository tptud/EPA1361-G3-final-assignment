# Flood Risk Management Model

# Group 3


This repository contains a Flood Risk Management Model implemented using the EMA Workbench.
The model analyzes different scenarios and policies for managing flood risks in a given area. 
It takes into account factors such as dike heights, room for the river, and policy interventions.

## Prerequisites

To reproduce the analysis, you need to have the following software and packages installed:

- Python (version 3.11.3)
- EMA Workbench (version 2.4.1)
- Pandas (version 2.0.2)
- NumPy (version 1.24.3)
- Matplotlib (version 3.7.1)
- Seaborn (version 0.12.2)

## Repository Structure


- The `data/` directory contains the input files required by the dike model.
- The `model/` directory contains the dike model 
- The `notebooks/` directory contains Jupyter notebooks used for the analysis. These notebooks provide step-by-step instructions on running the analysis and generating the results.
- The `Output/` directory contains the analysis results and visualizations obtained using the EMA Workbench.

## Installation

Clone the repository: `our url `

## Exploration 
This .ipynb notebook contains the exploration phase of the model.

### Usage


2. Choose the problem formulation
3. Define policies for accordingly, use different scenarios, add a base case:

   ```python
   def base_case():
       return {l.name: 0 for l in dike_model.levers}

   policies = [
       Policy("base case", **base_case()),
       Policy("only heighting", **dict(base_case(), **{'A.1_DikeIncrease 0': 10, 'A.2_DikeIncrease 0': 10, 'A.3_DikeIncrease 0': 10, 'A.4_DikeIncrease 0': 10, 'A.5_DikeIncrease 0': 10})),
       Policy("only RfR", **dict(base_case(), **{'0_RfR 0': 1, '1_RfR 0': 1, '2_RfR 0': 1, '3_RfR 0': 1, '4_RfR 0': 1})),
       Policy("Final policy debate", **dict(base_case(), **{'0_RfR 0': 1, 'A.1_DikeIncrease 0': 3, 'A.2_DikeIncrease 0': 3, 'A.3_DikeIncrease 0': 10, '0_RfR 0': 1, 'A.4_DikeIncrease 0': 3, 'A.5_DikeIncrease 0': 10}))
   ]
   ```


4.  it visualizes the results using various plots and analysis techniques. Examples include:

   * Pairplot visualization: `from visualization_functions import pairplot_maker`

   * Boxplot and histogram visualization: `from visualization_functions import boxplot_histogram_maker`

   * PRIM analysis: `from ema_workbench.analysis import prim`

### Mordor and Moro

Define convergence metrics, number of function evaluations, and epsilon values:
```python
convergence_metrics = [EpsilonProgress()]
nfe = 100000
epsilon = [0.5,] * len(model.outcomes)
```
Then save the results and analyse whether it converges

```python
df, convergence = total
df.to_csv('MORDOR_small.csv')
fig, ax = plt.subplots()
ax.plot(convergence.nfe, convergence.epsilon_progress)
ax.set_ylabel('$\epsilon$-progress')
ax.set_xlabel('number of function evaluations')
plt.show()
```




