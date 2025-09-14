# Quantum Optimization for the Knapsack Problem (Q³ Qompute 2025) 



This repository contains the experiment and results for solving the **37-item Knapsack Problem** using a Variational Quantum Eigensolver (VQE) for **Q³ Qompute 2025**. The solution formulates the problem as a QUBO, implements a **CVaR-VQE** objective, and uses a lightweight **NFT (Nakanishi-Fujii-Todo)** coordinate optimizer [1, 2] to find the solution.

------

## Team

Team Name: qm_for_good

Member's Name: Qingtian Miao

------

## ✨ Highlights



- **Problem**: 37-Item 0/1 Knapsack Problem formulated as a QUBO (Quadratic Unconstrained Binary Optimization) model.
- **Ansatz & Backend**: A custom `TwoLocal` variational circuit with bilinear entanglement, executed on Qiskit's `AerSimulator`.
- **Objective Function**: **Conditional Value-at-Risk (CVaR)** with α=0.1, focusing the optimizer on the average of the best 10% of measurement outcomes.
- **Optimizer**: A custom, dependency-light **NFT** coordinate descent optimizer, which uses three function probes to determine parameter updates.
- **Verification**: The final quantum solution is checked for feasibility (i.e., total weight ≤ capacity) and compared against the optimal classical solution found by CPLEX.

------



## 🗂️ Repository Files



- `Knapsack_37_item_solution.ipynb`: The main Jupyter Notebook containing the end-to-end workflow.
- `README.md`: This file.
- [📄 Project Presentation Deck](Project_Presentation_deck.pdf)

------



## 🚀 How to Run the Experiment





### 1. Environment Setup



It is recommended to use a virtual environment with Python 3.10+.

Bash

```
# Example using Conda
conda create -n q3qompute python=3.10 -y
conda activate q3qompute
```



### 2. Install Dependencies



The required Python libraries are listed in the first code cell of the notebook.

Bash

```
pip install qiskit qiskit-aer docplex numpy scipy numba matplotlib jupyter
```



### 3. Execute the Notebook



Open and run all cells in `Knapsack_37_item_solution.ipynb`.

------



## ⚙️ Experiment Workflow



The notebook is structured into four main parts:

1. **Part I: Problem Definition**: A 37-item knapsack instance is created with random values and weights. The problem is modeled using `docplex`, and a classical solution is found with CPLEX for benchmarking.
2. **Part II: QUBO Formulation**: The constrained optimization model is converted into a QUBO by combining the objective function with a squared hinge-loss penalty for constraint violations.
3. **Part III: Quantum Circuit Design**: A `TwoLocal` variational ansatz is constructed with `RY` rotation gates and `RXX` entangling gates in a bilinear pattern. The circuit is then transpiled for the `AerSimulator` backend.
4. **Part IV: VQE Execution & Optimization**: The custom NFT optimizer is used to minimize the CVaR objective function over 4 epochs. Global trackers are used to store the single best bitstring found during the entire run.

------



## 📊 Expected Output



Upon completion, the notebook will output:

- **Classical Solution**: The optimal items, total value, and total weight found by the CPLEX solver.
- **VQE Optimization Log**: A real-time log of each evaluation, showing the CVaR cost and the best objective value found so far.
- **Optimizer Results**: A summary including the total runtime, final CVaR value, and the number of function evaluations.
- **VQE Solution Analysis**: A verification of the best bitstring found, confirming its total value, total weight, and feasibility.
- **Final Comparison**: A side-by-side comparison of the classical and quantum solution bitstrings.



## 📚 References



1. K. M. Nakanishi, K. Fujii, and S. Todo, “Sequential minimal optimization for quantum-classical hybrid algorithms,” Phys. Rev. Research, vol. 2, p. 043158, 2020. (arXiv:1903.12166).

2. WISER Optimization VG (code repository), https://github.com/bimehta/WISER_Optimization_VG (accessed Sep. 13, 2025).



