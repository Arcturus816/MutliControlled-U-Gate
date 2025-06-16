# MultiControlled U-Gate 

This repo is for work related to my implementation of a multicontrolled U-gate (in Qiskit), which was completed in early June of 2025. Any updates to this will be noted. 

## Problem Statement 
This gate was created to satisfy the following prompt: 

Write a Qiskit function that takes two inputs: a positive integer n and a matrix U $\in{U(2)}$. The function should and output a quantum circuit on $n+1$ qubits, possibly with further ancillas, that implements a multi-controlled U gate, $C^nU$. 

That is: 

$$C^nU|x\rangle_n{|y\rangle_1}=
\begin{equation}
f(x) = \begin{cases}
|x\rangle_nU|y\rangle_1 & \text{if } x = (1,1,...,1) \\
|x\rangle_n|y\rangle_1 & \text{otherwise } 
\end{cases}
\end{equation} $$

Note that we may only use arbitrary 1-qubit gates (U gates) and CX gates, and that no classical bit measurements will be allowed. 

## Outline of Process

This outline is also given wihtin the Jupyter notebook for the project. 

1. We begin by discussing how to contstruct the multi-controlled U gate. This involves:

    A. Creating S, T, T(dag), and H gates from the allowable gates 

    B. Using these to create a function that builds a Toffoli gate with certain inputs 

    C. Finally, using 2(n-1) of these Toffoli gates in the final function that implements the multi-controlled gate

2. We will then work out qiskit code with benchmarking for low values of n. 

3. Fianlly, we provide an analysis of the various complexities and resources used (given out gate count, gate depth, and number of ancillas)

## Creating the Circuit
### Permitted Gates

#### Recall, U gates are definied as follows: 

$U(\theta, \varphi, \lambda)$ = $$\begin{bmatrix}
    \cos \left( \tfrac{\theta}{2} \right) & - e^{i \lambda} \sin \left( \tfrac{\theta}{2} \right) \\
    e^{i \varphi} \sin \left( \tfrac{\theta}{2} \right) & e^{i (\varphi + \lambda)} \cos \left( \tfrac{\theta}{2} \right) 
    \end{bmatrix}$$,

for some $(\theta, \varphi, \lambda) \in \left[ 0, 2 \pi \right)^3$. 

Every 1-qubit gate can be written in this form. 

-----------------------------------------------------

#### CX gates are 2-qubit gates, also known as "Controlled-NOT" gates:

We can view the action on our basis vectors as: 

$$|00>\rightarrow{|00>}$$

$$|01>\rightarrow{|11>}$$

$$|10>\rightarrow{|10>}$$

$$|11>\rightarrow{|01>}$$

### Toffoli Gates 

Are constructed from the permitted gates.

### Multicontrolled U-Gate 

Is built using $2(n-1)$ Toffoli gates and the desired U gate. 



## Sources 
My implementation was informed by the contrusctions in Chapter II, Section 4 of Nielsen and Chuang. 
