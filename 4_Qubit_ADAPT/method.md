# Qubit-ADAPT-VQE: An Adaptive Algorithm for Constructing Hardware-Efficient Ansätze on a Quantum Processor

[PRX QUANTUM 2, 020310 (2021)](https://journals.aps.org/prxquantum/abstract/10.1103/PRXQuantum.2.020310)

## Introduction

1. Compare the the Fermionic ADAPT, whose operator pool is defined by the fermionic excitation operators, the operator pool of the Qubit ADAPT is defined by the qubit pauli operators.
2. The Pauli operator pool's number can be at least $2n - 2$, where n is the number of the qubit used in the algorithm. These $2n - 2$ operators are complete, which can transform any state of the qubit to $|0...0\rangle$.
3. Two constructed qubit operator pool:
   1. 

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