# Portfolio Optimization Using Reinforcement Learning  
### A Dynamic Trading Approach Inspired by Garleanu–Pedersen

## Overview

This project explores **portfolio optimization as a dynamic control problem** under transaction costs, mean reversion, and evolving return expectations.

Rather than directly tracking a static Markowitz optimal portfolio, the approach is inspired by the framework introduced in:

> Garleanu, N., & Pedersen, L. H.  
> *Dynamic Trading with Predictable Returns and Transaction Costs*

In this setting, the optimal portfolio evolves over time, and rational agents **trade toward** a moving target rather than instantly rebalance to it.  
This project implements that idea using **Advantage Actor-Critic (A2C)** reinforcement learning as a numerical approximation to the optimal trading policy.

---

## Motivation

Classical Markowitz portfolio optimization assumes:
- Frictionless markets
- Instantaneous rebalancing
- Static optimal weights

In practice:
- Transaction costs penalize aggressive trading
- Assets exhibit different mean reversion speeds
- Optimal positions evolve dynamically as forecasts change

The Garleanu–Pedersen framework formalizes this by treating portfolio choice as a **dynamic optimization problem**, where the optimal policy trades off:
- Expected return
- Risk
- Trading costs
- Adjustment speed toward a target portfolio

Reinforcement learning provides a natural way to learn such policies when:
- Closed-form solutions are unavailable
- Market dynamics are stochastic
- Constraints are nonlinear

---

## Problem Formulation

### State Space

The agent observes:
- Current portfolio weights
- Target (Markowitz-style) portfolio weights
- Asset returns or predictive signals
- Market state variables (e.g., volatility proxies)

### Action Space

- Continuous portfolio adjustments (position changes)
- Trades incur transaction costs proportional to turnover

### Reward Function

The reward is designed to reflect the Garleanu–Pedersen objective:
- Positive reward for expected returns
- Penalty for portfolio variance
- Penalty for transaction costs
- Optional penalty for excessive deviation from target weights

This formulation encourages **smooth, gradual rebalancing** rather than myopic optimization.

---

## Reinforcement Learning Approach

An **Advantage Actor-Critic (A2C)** algorithm is used to learn the trading policy:

- **Actor**: learns a stochastic policy for portfolio adjustments
- **Critic**: estimates the value function to reduce variance in policy updates

A2C is chosen because:
- It supports continuous action spaces
- It is stable for control problems
- It aligns naturally with dynamic optimization formulations

The RL agent does not attempt to replicate the Markowitz portfolio directly.  
Instead, it learns **how fast and how aggressively** to trade toward it under costs and uncertainty.

---

## Experimental Setup

- Synthetic or historical asset return data
- Rolling estimation of Markowitz target portfolios
- Fixed or stochastic transaction cost models
- Episodic training with multiple market trajectories

Performance is evaluated qualitatively in terms of:
- Turnover reduction
- Stability of portfolio paths
- Tracking behavior relative to the target portfolio

This work does **not** claim alpha generation or market outperformance.

---

## Results and Observations

Key qualitative observations include:

- The learned policy trades gradually toward the target portfolio
- Higher transaction costs induce slower adjustment speeds
- The agent naturally avoids excessive turnover
- Portfolio paths resemble theoretical dynamics predicted by Garleanu–Pedersen

These behaviors emerge without explicitly coding the optimal control solution, demonstrating that RL can recover economically meaningful structure.

---

## Limitations

- The environment is stylized and simplified
- Results are sensitive to reward shaping
- No claims are made about real-world profitability
- The approach is computationally intensive relative to closed-form solutions

This project is intended as an **exploratory numerical implementation**, not a trading strategy.

---

## Future Work

Possible extensions include:
- Multi-timescale mean reversion modeling
- Risk factor–based state representations
- Comparison against analytic Garleanu–Pedersen solutions
- Extension to multi-asset, constrained portfolios
- Off-policy methods or model-based RL approaches

---

## References

- Garleanu, N., & Pedersen, L. H.  
  *Dynamic Trading with Predictable Returns and Transaction Costs*  
  https://docs.lhpedersen.com/DynamicTrading.pdf

- Sutton, R. S., & Barto, A. G.  
  *Reinforcement Learning: An Introduction*

---

## Disclaimer

This project is for educational and research purposes only and does not constitute investment advice.
