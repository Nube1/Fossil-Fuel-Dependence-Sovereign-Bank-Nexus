# Fossil-Fuel-Dependence-Sovereign-Bank-Nexus
Fossil fuel dependence converts climate transition risk into a correlated sovereign–bank balance-sheet shock, breaking diversification assumptions and amplifying systemic risk.

# Triple-Knot Contagion Model (TKCM)

## Overview

The **Triple-Knot Contagion Model (TKCM)** is a Python-based simulation framework designed to quantify and visualize systemic risk within a sovereign-bank-corporate nexus. It models the feedback loops between three critical sectors:

1.  **Sovereign Debt** ($\delta_L$)
2.  **Corporate FX Exposure** ($\delta_{FX}$)
3.  **Banking Sector Capitalization** ($\delta_K$)

Unlike standard linear risk models, this tool implements a **non-linear stress multiplier** ($M(\kappa)$) to demonstrate how shocks amplify during regimes of high financial fragility.

## Theoretical Framework

The core of the simulation is the **Triple-Knot Index ($\kappa$)**, which acts as an attractor for systemic collapse.

### 1. The Kappa Equation
The systemic risk index is calculated as:

$$ \kappa = \frac{\lambda_s \cdot \gamma_s \cdot \alpha_s}{\delta_L \cdot \delta_{FX} \cdot \delta_K} $$

Where:
*   $\lambda_s$: Market Illiquidity Parameter
*   $\gamma_s$: FX Sensitivity
*   $\alpha_s$: Banking Sector Correlation
*   $\delta$: Respective buffers for Liquidity, FX reserves, and Capital.

### 2. Systemic Regimes
The model classifies the economy into four regimes based on $\kappa$:
*   **Stable:** $\kappa \le 0.3$
*   **Fragile:** $0.3 < \kappa \le 0.6$
*   **Critical:** $0.6 < \kappa < 1.0$
*   **Collapsing:** $\kappa \ge 1.0$

### 3. The Stress Multiplier
To simulate contagion, the model applies a hyperbolic multiplier to loss estimates:

$$ M(\kappa) = \frac{1}{1 - \kappa} $$

As $\kappa \to 1$, $M(\kappa) \to \infty$, simulating a singularity or total systemic freeze.

## Features

*   **Monte Carlo Simulation:** Compares "Standard" (decoupled) risk models against the "Coupled Nexus" model using 5,000 simulations with correlated shocks via Cholesky decomposition.
*   **Scenario Analysis:** Simulates specific economic scenarios (e.g., "Baseline" vs. "Disorderly").
*   **Policy Evaluation:** Analyzes the effectiveness of interventions (FX Intervention, LOLR, Capital Controls) against their implementation lag and side effects.
*   **Visualization:** Generates publication-ready plots for sensitivity analysis, non-linear amplification, and policy trade-offs.

## Prerequisites

The project requires **Python 3.8+** and the following libraries:

*   `numpy`
*   `pandas`
*   `matplotlib`
*   `seaborn`
*   `scipy`

## Installation

1.  Clone the repository or save the script.
2.  Install the dependencies:

```bash
pip install numpy pandas matplotlib seaborn scipy
```

## Usage

Run the main script to execute the simulation and generate reports:

```bash
python main.py
```

### Outputs

1.  **Console Report:** A summary of Mean Outcomes (PD, LGD, CET1) and Policy Effectiveness.
2.  **figure1_attractor.pdf:**
    *   *(a)* The Non-linear Multiplier function showing the critical zone.
    *   *(b)* A heatmap showing sensitivity of $\kappa$ to Illiquidity ($\lambda$) and FX Sensitivity ($\gamma$).
3.  **figure2_policy.pdf:**
    *   *(a)* Bar chart of loss reduction by policy type.
    *   *(b)* Scatter plot showing trade-offs between Implementation Lag and Side Effects.

## Code Structure

*   **`SystemicRegime` (Enum):** Defines the stability thresholds.
*   **`TripleKnotContagionModel` (Class):**
    *   `calculate_kappa`: Computes the systemic index.
    *   `stress_multiplier`: Computes the amplification factor.
    *   `simulate_nexus_impact`: Runs Monte Carlo simulations comparing standard vs. coupled models.
    *   `policy_analysis`: Evaluates different regulatory interventions.
*   **`TripleKnotVisualizer` (Class):** Static methods for generating matplotlib figures.
*   **`main`:** Execution entry point.

## Example Output

When running the script, you will see output similar to this:

```text
============================================================
TRIPLE-KNOT CONTAGION MODEL RESULTS
============================================================

Scenario Summary (Mean Outcomes):
                             Coupled Mean  Standard Mean
Scenario   Metric                                       
Baseline   CET1 Ratio (%)       12.85431       13.45120
           Corporate LGD (%)    42.10050       40.05120
           Sovereign PD (%)      1.65200        1.51200
Disorderly CET1 Ratio (%)        8.12040       11.85010
           Corporate LGD (%)    85.20010       45.12050
           Sovereign PD (%)      5.12050        2.05010

Policy Effectiveness:
               Policy  Loss Reduction (%)     Lag    Side
0     FX Intervention           22.500000   Short  Medium
1        LOLR Support           14.200000   Short     Low
2    Capital Controls           65.100000  Medium    High
3     Macroprudential           31.500000  Medium     Low
```

## License

This project is open-source and available for educational and research purposes.
