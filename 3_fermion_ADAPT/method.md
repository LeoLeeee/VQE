# An adaptive variational algorithm for exact molecular simulations on a quantum computer

[Nature Communications volume 10, Article number: 3007 (2019)](https://www.nature.com/articles/s41467-019-10988-2)

## Introduction

1. Compare the the UCCSD, whose ansatz is defined with given operator and optimized parameters, the ansatz of the ADAPT is predefined by the operators.Instead, the ansatz is growing step by step.
2. In principle, the UCCSD ansatz is, to some extent, the same for all the molecular. The difference is result from the parameter, which is depend on the Hamiltonian. As for ADAPT, the ansatz is different for different molecular. Not only for the parameter, but also for the operator and its order in the excitation unitary.
3. The operators are defined from all the excitation operators to form a operator pool.
4. To grow the ansatz, the gradients of the operators in the operator pool need to be calculated in every step, which results in the overhead of the measurements.
5. To calculate the gradients of the operator, the author provides a iterative method to save simulation time. But it may not applicable to the real quantum device.
6. A better operator pool is formed by the qubit_ADAPT method, and a detailed overhead of the measurements is discussed.

## Algorithm

1. Preparation of the wavefunction by application of parameterized state preparation unitaries;
   1. Define the molecular in the OpenFermion, get necessary parameters such as number of qubits.
   2. Prepare the HF state by JW transformation
   3. Prepare the Unitary by JW transformation
      1. Prepare the operators pool with the excitation operators, $\hat{t}$. These operators could be defined with single and double excitation operators.
   4. Prepare the Hamiltonian by the OpenFermion and do the JW transformation
2. Calculate the gradients of the operator in the operator pool.
   1. Calculate the gradients of the operator, choose the operator with largest gradient.
   2. Construct the ansatz given by the chosen operator given the initial parameters with 0.
3. Determination of the expectation value of every term in the Hamiltonian via an efficient partial tomography;
   1. Applied the Unitary on the HF state orderly.
   2. Simulate the energy expectation
4. Calculation of the total energy and determination of a new set of state preparation parameters in a classical computer.
   1. Optimize the parameter in Unitary.
   2. Return to the step 2 to calculate the gradient of all the operator in the operator pool and stop until the norm of the gradient is bellow the threshold.