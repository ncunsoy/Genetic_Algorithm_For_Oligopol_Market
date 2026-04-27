# Genetic Algorithm for Oligopoly Market

A genetic algorithm (GA) implementation that explores whether firms in a differentiated product oligopoly can learn the Cournot-Nash equilibrium through evolutionary dynamics, based on Arifovic (1994).

## Overview

In a differentiated product oligopoly with n firms, each firm's output decision affects others through a substitutability/complementarity parameter b. The theoretical Cournot-Nash equilibrium defines the optimal output, price, and profit for each firm. This project asks: can firms *learn* this equilibrium without knowing it explicitly — purely through a genetic algorithm?

## How it works

Each firm is represented as a chromosome (binary string of length 10). The GA runs for T = 1000 iterations with a single population of n = 30 chromosomes and applies four genetic operators each round:

- **Recombination** — select chromosomes proportional to fitness (profit)
- **Crossover** — exchange segments between pairs of chromosomes with probability p_cross
- **Mutation** — flip bits with probability p_mut
- **Election** — replace parent with offspring only if offspring performs better

Chromosomes are decoded from binary to continuous output quantities, and fitness is evaluated as each firm's profit given the current population's output decisions.

## Experiments

Three configurations are compared over 1000 iterations, tracking industry output Q_t and population variance σ²_t:

| Configuration | p_cross | p_mut | Finding |
|---|---|---|---|
| Benchmark | 0.300 + offset | 0.00300 + offset | Convergence to Cournot-Nash |
| High crossover | benchmark + 0.200 | benchmark | Faster/slower convergence |
| High mutation | benchmark | benchmark + 0.00200 | Higher variance, disrupted convergence |

## Reference

Arifovic, J. (1994). Genetic algorithm learning and the cobweb model. *Journal of Economic Dynamics and Control*, 18, 3–28.
