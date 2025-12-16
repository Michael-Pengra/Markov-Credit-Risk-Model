# Markov Chain Credit Risk Model (Excel)

## Overview
This project models credit risk migration and calculates Expected Loss (EL) using a Discrete-Time Markov Chain. Built entirely in Excel, the model simulates how a borrower's credit rating (AAA through CCC) evolves over time, utilizing historical transition probabilities from S&P Global (1981-2023).

This is the second model in my quantitative finance portfolio, following a Geometric Brownian Motion (GBM) simulation.

## Key Features
* **Dynamic Inputs:** Users can configure Loan Amount, Loss Given Default (LGD), and initial Credit Rating.
* **36-Year Probability Forecast:** Uses matrix exponentiation to project transition matrices up to 36 years into the future.
* **Long-Run Evolution:** Tracks the specific probability vector of a borrower across 787 years until the probability of default reaches ~99.99% (Absorbing State).
* **Interactive Dashboard:** Visualizes Capital at Risk and Cumulative Default Probability curves based on a user-defined time horizon.

## Mathematical Framework
The core of the model relies on **Markov Chains**, where the future state depends only on the current state.

### 1. The Transition Matrix ($P$)
The model uses an $8 \times 8$ transition matrix representing ratings: `AAA, AA, A, BBB, BB, B, CCC, Default`.
* **Absorbing State:** The "Default" state is absorbing, meaning once a borrower enters this state, the probability of staying there is 100%.

### 2. Probability forecasting
To find the probability matrix for year $n$, the model calculates the power of the matrix:
$$P_n = P^n$$
In Excel, this is achieved using the `MMULT` function iteratively.

### 3. State Vector Evolution
To determine the specific rating distribution for a single borrower starting at a specific rating (e.g., BBB) at time $t+1$, the model performs vector-matrix multiplication:
$$\pi_{t+1} = \pi_t \times P$$
Where $\pi_t$ is the row vector of probabilities at time $t$.

### 4. Risk Metrics
The model calculates the **Expected Loss (EL)** for a given horizon:
$$EL = EAD \times LGD \times PD_t$$
* **EAD:** Exposure at Default (Loan Amount)
* **LGD:** Loss Given Default (%)
* **PD:** Probability of Default (derived from the transition vector)

## File Structure

### 1. Inputs
Contains the user drivers and the raw S&P Global Transition Matrix.
* **Inputs:** Loan Amount, LGD, Initial Rating.
* **Matrix:** 8x8 probability grid.

### 2. Probability Forecast
Calculates the raw probability matrices for Years 1 through 36.
* **Formula:** `MMULT` allows for the calculation of $P^t$ to determine long-term transition probabilities.

### 3. Steady State / Time Evolution
Tracks the specific probability vector for the borrower starting at $t=0$ through $t=787$.
* **Logic:** Starts with a vector (e.g., `[0, 0, 1, 0...]` for 'A' rating) and multiplies by the matrix iteratively to show how the borrower "migrates" toward default over centuries.

### 4. Risk Metrics
Aggregates data for the Dashboard.
* Calculates point-in-time Expected Loss.
* Structures data for the "Capital at Risk" and "Cumulative Default Probability" charts.

### 5. Dashboard
The front-end visualization layer.
* **Controls:** Allows the user to change the Time Horizon.
* **Visuals:** Displays Capital at Risk histograms and Cumulative Default Probability curves comparing different rating tiers (AAA vs BBB vs CCC).

## Usage
1. Open the Excel file.
2. Navigate to the **Inputs** sheet to set the Loan Amount and Initial Credit Rating.
3. Go to the **Dashboard** to view the risk profile and adjust the Time Horizon to see how risk capital requirements change over time.# Markov-Credit-Risk-Model
