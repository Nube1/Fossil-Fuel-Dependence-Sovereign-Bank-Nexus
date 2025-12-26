# Fossil-Fuel-Dependence-Sovereign-Bank-Nexus
Fossil fuel dependence converts climate transition risk into a correlated sovereign–bank balance-sheet shock, breaking diversification assumptions and amplifying systemic risk.

# Open Economy Nexus & Triple-Knot Contagion Frameworks

## Overview

This repository implements a dual-framework approach to quantifying systemic risk within the **Sovereign-Bank-Corporate Nexus**. It contains two complementary models designed to analyze how financial contagion spreads through feedback loops in open economies:

1.  **The Triple-Knot Contagion Model (TKCM):** A static, non-linear stress-testing tool focused on "regime classification" and policy multipliers.
2.  **The Open Economy Nexus Model (OENM):** A stochastic, structural simulation using coupled differential equations to model time-varying dynamics and "cliff effects."

---

## 1. Triple-Knot Contagion Model (TKCM)

The TKCM focuses on the **amplification of losses** based on the fragility of the financial system. It calculates a systemic index ($\kappa$) that acts as a multiplier for standard credit risk models.

### Theoretical Framework
The core metric is the **Triple-Knot Index ($\kappa$)**, defined as:

$$ \kappa = \frac{\lambda_s \cdot \gamma_s \cdot \alpha_s}{\delta_L \cdot \delta_{FX} \cdot \delta_K} $$

Where the numerator represents sensitivities (Illiquidity $\lambda$, FX $\gamma$, Correlation $\alpha$) and the denominator represents buffers (Liquidity $\delta_L$, Reserves $\delta_{FX}$, Capital $\delta_K$).

### Systemic Regimes & Multiplier
The model defines the economy's state and applies a hyperbolic stress multiplier ($M$):

| Regime | $\kappa$ Range | Multiplier Logic $M(\kappa)$ | Description |
| :--- | :--- | :--- | :--- |
| **Stable** | $\kappa \le 0.3$ | $\approx 1.0$ | Standard linear loss models apply. |
| **Fragile** | $0.3 < \kappa \le 0.6$ | Increasing | Feedback loops begin to amplify shocks. |
| **Critical** | $0.6 < \kappa < 1.0$ | Exponential | Small shocks cause massive losses. |
| **Collapsing** | $\kappa \ge 1.0$ | Singularity | Systemic freeze; multiplier capped for stability. |

$$ M(\kappa) = \frac{1}{1 - \kappa} $$

### Key Outputs
*   **Policy Trade-off Analysis:** Visualizes the effectiveness of interventions (e.g., LOLR, Capital Controls) vs. their implementation lags and side effects.
*   **Regime Heatmaps:** Contours showing how changes in FX sensitivity and illiquidity shift the economy into critical zones.

---

## 2. Open Economy Nexus Model (OENM)

The OENM is a **dynamic structural framework** that uses Stochastic Differential Equations (SDEs) to simulate the evolution of the crisis over time ($t$). It is designed to capture **Sudden Stops** and **Liquidity Freezes**.

### Structural Equations
The model tracks three coupled state variables:

1.  **Sovereign Risk ($P^S_t$):** Driven by mean-reversion to a target that shifts based on external stress.
    $$ dP^S_t = \kappa_S (\theta^S(X_t) - P^S_t)dt + \sigma_S \sqrt{P^S_t} dW^S_t $$
2.  **Corporate Distress ($L^C_t$):** Models the "Freezing" of corporate balance sheets when Sovereign and FX risks combine.
3.  **External Stress ($X_t$):** Uses a **Sigmoid Function** to model non-linear capital flight when sovereign risk hits a critical threshold ($P_{crit}$).

$$ \Psi(P^S) = \frac{X_{max}}{1 + e^{-\alpha(P^S - P_{crit})}} $$

### Visualization Suite
The OENM includes an advanced visualization module:
*   **3D Phase Space:** A trajectory plot showing the economy moving through the $P^S - L^C - X$ volume, color-coded by time.
*   **Bifurcation Diagrams:** Analysis of system stability (via Eigenvalues) as parameters change.
*   **Structural Stability Maps:** Heatmaps identifying globally stable vs. unstable regions based on structural parameters.

---

## Getting Started

### Prerequisites
The framework requires Python 3.8+ and the following scientific computing libraries:

```bash
pip install numpy pandas matplotlib seaborn scipy
```

### Installation
Clone the repository:

```bash
git clone https://github.com/your-username/nexus-contagion-framework.git
cd nexus-contagion-framework
```

## Usage

### Running the Triple-Knot Model (TKCM)
Use this model for static stress testing and policy impact analysis.

```python
from tkcm import TripleKnotContagionModel, TripleKnotVisualizer

# Initialize model
model = TripleKnotContagionModel()

# Run Scenario Analysis (Baseline vs. Disorderly)
model.simulate_nexus_impact(scenario_name="Disorderly", base_pd=2.0, base_lgd=45.0, base_cet1=12.0, kappa=0.68)

# Generate Policy Analysis
policy_df = model.policy_analysis()
```

### Running the Open Economy Nexus (OENM)
Use this model for dynamic simulation of crash mechanics and trajectory analysis.

```python
from nexus_model import OpenEconomyNexus, NexusVisualizer, disorderly_transition_params

# Load Disorderly Transition Parameters
params = disorderly_transition_params()
model = OpenEconomyNexus(params)

# Run Monte Carlo Simulation (500 paths)
mc_paths = model.simulate(n_paths=500)

# Visualize 3D Trajectory and Time Series
vis = NexusVisualizer()
vis.plot_time_series(model, *mc_paths[0], show_quantiles=True, mc_paths=mc_paths)
```

## Comparisons

| Feature | Triple-Knot (TKCM) | Open Economy Nexus (OENM) |
| :--- | :--- | :--- |
| **Math Basis** | Algebraic / Static Multipliers | Stochastic Differential Equations |
| **Time Dimension** | Snapshot (Before/After) | Continuous Time ($t_0 \to T$) |
| **Key Metric** | $\kappa$ (Systemic Fragility Index) | Jacobian Eigenvalues (Stability) |
| **Best For** | Capital Planning, Policy Selection | Crisis Mechanics, Tail Risk Dynamics |
| **Visuals** | Heatmaps, Bar Charts | 3D Phase Plots, Fan Charts |

## License
This project is open-source and available for educational and research purposes.
