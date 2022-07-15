# A variational eigenvalue solver on a photonic quantum processor

[Nature Communications volume 5, Article number: 4213 (2014)](https://www.nature.com/articles/ncomms5213?ref=https://githubhelp.com)

## Introduction

1. This paper seems to be the first time introduce the VQE method by using a photonic quantum processor.
2. It used a device ansatz without any chemical domain knowledge. The device ansatz benefits it from the easy access of the state preparation by tuning several parameters of photonic thermal phase shifters.
3. It used a Nelder-Mead algorithm to optimize the objective function, i.e., the ground energy of the Hamiltonian. But here I find it is slowly, so I use the COBYLA method.

## Algorithm

1. Define the circuit, which is used to generate the trial state according to a set of the experimental parameters $\left\{\theta_{i}\right\}$. $\left\{\theta_{i}\right\}$ represents the phase controlled by the photonic thermal phase shifters.
    - An arbitrary 2-qubit pure state can be parametrized in the following form
    $$
    \begin{aligned}
    |\psi\rangle=& \cos \left(\frac{\theta_{0}}{2}\right) \cos \left(\frac{\theta_{1}}{2}\right)\left|0_{1} 0_{2}\right\rangle \\
    &+\cos \left(\frac{\theta_{0}}{2}\right) \sin \left(\frac{\theta_{1}}{2}\right) e^{i \omega_{1}}\left|0_{1} 1_{2}\right\rangle \\
    &+\sin \left(\frac{\theta_{0}}{2}\right) e^{i \omega_{0}} \cos \left(\frac{\theta_{2}}{2}\right)\left|1_{1} 0_{2}\right\rangle \\
    &+\sin \left(\frac{\theta_{0}}{2}\right) e^{i \omega_{0}} \sin \left(\frac{\theta_{2}}{2}\right) e^{i \omega_{2}}\left|1_{1} 1_{2}\right\rangle, \\
    & \theta_{i} \in[0, \pi], \omega_{i} \in[0,2 \pi] .
    \end{aligned}
    $$
    - So here it use 6 parameters to form the $\left\{\theta_{i}\right\} = \left\{\theta_{0}, \theta_{1}, \theta_{2}, \omega_{0}, \omega_{1}, \omega_{2}\right\}$.
2. Applied the Hamiltonian on the trial state and calculate the objective function: $f\left(\left\{\theta_{i}^{n}\right\}\right)=\left\langle\psi\left(\left\{\theta_{i}^{n}\right\}\right)|\mathcal{H}| \psi\left(\left\{\theta_{i}^{n}\right\}\right)\right\rangle$, which efficiently maps the set of experimental parameters to the expectation value of the Hamiltonian. $n$ denotes the current iteration of the algorithm.
3. Repeat until optimization is completed:
    i. Using the QPU, compute $\left\langle\sigma_{\alpha}^{i}\right\rangle,\left\langle\sigma_{\alpha}^{i} \sigma_{\beta}^{j}\right\rangle$, $\left\langle\sigma_{\alpha}^{i} \sigma_{\beta}^{j} \sigma_{\gamma}^{k}\right\rangle, \ldots$, on $\left|\psi^{n}\right\rangle$ for all terms of $\mathcal{H} .$
    ii. Classically sum on CPU the values from the QPU with their appropriate weights, $h$, to obtain $f\left(\left\{\theta_{i}^{n}\right\}\right)$
    iii. Feed $f\left(\left\{\theta_{i}^{n}\right\}\right)$ to the classical minimization algorithm (e.g. gradient descent or NelderMead Simplex method), and allow it to determine $\left\{\theta_{i}^{n+1}\right\}$.