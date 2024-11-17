# European Option Pricing Simulation

This project implements a Monte Carlo simulation to price European-style options expiring in \( T = 0.75 \) years. The simulation assumes the stock price changes daily, with 250 trading days in a year, and generates 10,000 price paths to compute the option price.

---

## **Problem Description**

The stock price \( S_t \) follows the risk-neutral dynamics:

\[ dS_t = (r - q) S_t dt + \sigma S_t dz_t, \]

where:
- \( S_0 = 100 \): Initial stock price
- \( r = 0.05 \): Continuously compounded risk-free rate (5%)
- \( q = 0.02 \): Dividend yield (2%)
- \( \sigma = 0.40 \): Volatility (40%)
- \( T = 0.75 \): Option maturity in years
- \( \Delta t = 1/250 = 0.004 \): Time step (1 trading day)
- \( z_t \): Standard Brownian motion

The dynamics of the log-price \( x = \ln(S) \) are given by:

\[ x_{t+\Delta t} = x_t + \left(r - q - \frac{\sigma^2}{2}\right) \Delta t + \sigma \sqrt{\Delta t} \epsilon, \]

where \( \epsilon \sim N(0, 1) \). 

The price of the option is:

\[ P = \frac{1}{10,000} \sum_{k=1}^{10,000} X_k e^{-rT}, \]

where \( X_k \) is the payoff for the \( k \)-th simulation.

---

## **Steps**
1. **Simulate Price Paths**:
   - Simulate 10,000 paths for the stock price from \( t = 0 \) to \( t = T \), using \( \Delta t = 0.004 \).

2. **Compute Payoffs**:
   - For each path, calculate the option payoff \( X(k) \) at maturity.

3. **Calculate Option Price**:
   - Average the payoffs across all paths and discount them at the risk-free rate \( r \).

---

## **Inputs**
- Stock price today: \( S_0 = 100 \)
- Risk-free rate: \( r = 5\% \)
- Dividend yield: \( q = 2\% \)
- Volatility: \( \sigma = 40\% \)
- Time step: \( \Delta t = 0.004 \)
- Number of paths: 10,000

---

## **Outputs**
- Simulated stock price paths.
- Estimated option price.

---

This README explains the simulation setup and details how the option price is calculated using Monte Carlo methods.
