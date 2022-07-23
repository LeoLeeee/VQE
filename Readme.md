# Variational quantum eigensolver

## Introduction

1. This project uses OpenFermion and Cirq to implement the VQE algorithm.
2. In each method, a matrix calculation is implemented first to demonstrate the algorithm and acts as an verification. Then, a quantum circuit based on the Cirq is created and demonstrate the VQE algorithm. Note that the energy expectation get from circuit simulation is very time consuming and noisy.
3. Each algorithm contains a method.md, which used to simply summarize the corresponding paper and its algorithm, a jupyter notebook, which is used to demonstrate the algorithm. In the jupyter notebook, some detailed instructions are contained.

## Environment configuration on windows

- Using openfermion_scf on windows is not available. So I use [Docker](https://github.com/quantumlib/OpenFermion/tree/master/docker) to create a image running on Win10. Note I revised the docker file for it can run properly on my computer.
- Instruction on how to install this image is contained in the installation.md
- You can also use the image on Linux as you like.
  
## Simple file structure

- In each jupyter notebook, the file structure:
    1. Import the necessary library
    2. Hamiltonian or molecular definition
    3. Functions used for VQE
       1. Direct matrix implementation
       2. Cirq implementation
    4. VQE functions
       1. scipy optimization
       2. dissociation curve calculation
    5. Simulation of VQE using functions defined above
       1. Direct matrix as verification
       2. Cirq implementation, time consuming.

----------------------------------------------------------------

## Notation

1. I fork and followed the [program](https://github.com/MafaldaRA/VQE), which give much more detailed discussion and implementation of those algorithms. But the jupyter file it contained may not well structure and neglect some basic domain knowledge, which is not friendly for a new starter like me. So I revised its implementation and add more detailed instructions.
2. As a simple implementation of the VQE algorithm, I do not compare the advantage between those algorithm. But you can find it in detail in their original papers.
