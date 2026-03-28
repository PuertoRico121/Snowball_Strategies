
# Snowball Coupon Monte Carlo Simulation

## Overview

This project implements a Monte Carlo simulation framework for pricing and analyzing a structured **Snowball Coupon product**.

The objective is to:

- Simulate underlying asset price paths
- Model knock-in and knock-out conditions
- Evaluate coupon payments and principal protection
- Estimate product fair value under stochastic dynamics
- Analyze payoff distribution and risk characteristics

The framework follows a quantitative derivatives pricing approach under risk-neutral dynamics.

---

## Product Structure

A Snowball product typically includes:

- Periodic coupon payments (conditional)
- Knock-out barrier (early redemption)
- Knock-in barrier (capital loss trigger)
- Maturity payoff based on final asset level

### Key Features

- If the asset price breaches the knock-out barrier:
  - Product terminates early
  - Investor receives coupon + principal

- If the asset breaches the knock-in barrier:
  - Downside exposure is activated
  - Final payoff depends on terminal price

- If neither barrier is triggered:
  - Investor receives coupon and principal at maturity

---

## Model Assumptions

The underlying asset follows a Geometric Brownian Motion (GBM):

\[
dS_t = \mu S_t dt + \sigma S_t dW_t
\]

Under risk-neutral pricing:

\[
\mu = r
\]

Where:

- \( S_t \) = Asset price
- \( r \) = Risk-free rate
- \( \sigma \) = Volatility
- \( W_t \) = Brownian motion

Discrete-time simulation is used for Monte Carlo path generation.

---

## Monte Carlo Simulation Framework

### Step 1: Path Generation

- Simulate large number of price paths
- Daily or monthly time steps
- Apply stochastic diffusion process

### Step 2: Barrier Monitoring

For each path:

- Check knock-out condition at observation dates
- Check knock-in condition continuously or discretely
- Record trigger time (if any)

### Step 3: Payoff Calculation

Depending on path outcome:

- Early knock-out → discounted coupon payoff
- Knock-in without recovery → equity-linked loss
- No trigger → full coupon + principal

### Step 4: Discounting

Expected payoff discounted at risk-free rate:

\[
Price = e^{-rT} \cdot \mathbb{E}[Payoff]
\]

---

## Risk Analysis

The simulation framework allows analysis of:

- Probability of knock-out
- Probability of knock-in
- Expected holding period
- Payoff distribution
- Downside tail risk
- Sensitivity to volatility

---

## Model Extensions

The structure can be extended to include:

- Stochastic volatility
- Jump-diffusion models
- Local volatility surface
- Correlated multi-asset snowballs
- Greek estimation via pathwise or bump-and-revalue methods

---

## Applications

This framework is useful for:

- Structured product pricing
- Risk management
- Scenario analysis
- Volatility sensitivity study
- Structured note design optimization

---

## Disclaimer

This implementation is for educational and research purposes only.  
It does not constitute investment advice or product recommendation.
