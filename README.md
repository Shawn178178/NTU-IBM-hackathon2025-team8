# Multi-Objective Optimization Using QAOA

**NTU-IBM Quantum System Qiskit Hackathon Taiwan 2025**

**Team 8:**
Bo-Yu Lien, Jeongbin-Jo, Eliška Krátká, Hsiao-Nan Lu, Shang-Ling Hung

The project consists of three Jupyter notebooks that utilize the Quantum Approximate Optimization Algorithm (QAOA) and a multi-objective optimization (QMOO) technique to solve two different optimization problems: Max-Cut and the Multi-Objective Vehicle Routing Problem (MOVRP).

---
### `implementation.ipynb`
This notebook contains the code for running experiments on real hardware.


### `qmoo_with_HV.ipynb`

This notebook addresses the **Max-Cut problem** by building and optimizing a QMOO circuit based on the QAOA framework, using a hypervolume-based cost function.

#### Key Contents:
- **Graph Construction**: The notebook uses the `rustworkx` library to create a 10-node graph. The graph is constructed based on two sets of weights (`graph_weight1`, `graph_weight2`).
- **Hamiltonian Modeling**: The graph is converted into a cost Hamiltonian for the Max-Cut problem. A weighted Hamiltonian is used, derived from a linear combination of two Hamiltonians (`hamil1` and `hamil2`).
- **Quantum Circuit**: A QAOA-based QMOO circuit is created using `qiskit.circuit.library.QAOAAnsatz` with two layers (`reps=2`). The circuit includes mixer (RX gates) and cost Hamiltonian operators (`PauliEvolutionGate`).
- **Optimization**: The `COBYLA` optimizer from `scipy.optimize.minimize` is employed to optimize the circuit's parameters. The optimization aims to maximize the hypervolume of the solution set.
- **Evaluation**: The hypervolume is used as the cost function to evaluate the quality of the Pareto optimal set of solutions in the multi-objective problem. A reference point of `(1, 1)` is used.
- **Result Visualization**: The final output includes a scatter plot showing all solutions and the Pareto front, which represents the set of solutions that are not dominated by any other solution.

---

### `based_qubo.ipynb`

This notebook presents a method for modeling and solving the **Multi-Objective Vehicle Routing Problem (MOVRP)** using a Quantum Multi-Objective Optimization approach. The problem is formulated in the **QUBO (Quadratic Unconstrained Binary Optimization)** format.

#### Key Contents:
- **MOVRP Modeling**: The notebook models a MOVRP with 5 customers and 2 vehicles. It defines two objective functions: efficiency and service quality, and their corresponding costs (`costs_eff`, `costs_ser`).
- **QUBO Matrix Generation**: QUBO matrices (`Q_eff`, `Q_ser`) are generated for each objective. Penalty terms are included to enforce the constraint that each customer must be assigned to exactly one vehicle.
- **Hamiltonian Conversion**: The QUBO matrices are converted into Ising Hamiltonians in the Pauli operator list format, which is a necessary step for quantum computation.
- **QMOO Circuit**: A QAOA-style QMOO circuit is created using the two Hamiltonians (`H_eff`, `H_ser`) as phase operators.
- **Solution Decoding and Visualization**: The notebook provides functions to decode bitstrings from the quantum circuit's measurement results into customer-vehicle assignments. It then visualizes a single optimized solution and a random solution on a graph, showing the depot and customer locations with assigned vehicle routes. This visualization helps to intuitively understand the trade-offs between the two objectives (e.g., total distance vs. delivery delay).

#### References:

[1] A. Kotil et al., “Quantum Approximate Multi-Objective Optimization,” arXiv:2503.22797v1 (2025).
[2] A. Kotil et al., “Variational Quantum Multi-Objective Optimization,” arXiv:2312.14151 (2023).
[3] R. Shaydulinet al., “Parameter Transfer for Quantum Approximate Optimization of Weighted MaxCut,” arXiv:2201.11785v2 (2023).
