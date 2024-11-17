# European Option Pricing using Black-Scholes Model

## Methodology

The model of Black and Scholes (1973) implies that it is possible to price European-style derivatives by simulating the stock price under the risk-neutral measure and discounting expected payoffs at the risk-free rate.

**Reference**:  
Black, Fischer, and Myron Scholes. 1973. *The Pricing of Options and Corporate Liabilities.* Journal of Political Economy 81 (3): 637–54.

Consider a stock with price \( S \) that pays a dividend yield \( q \) and whose risk-neutral dynamics are given by:

\[
dS = (r - q) S \, dt + \sigma S \, dz,
\]

where:  
- \( r \): Continuously compounded risk-free rate  
- \( z \): Brownian motion  

Using \( x = \ln(S) \), Ito's lemma implies:

\[
dx = \left( \mu - \frac{1}{2} \sigma^2 \right) dt + \sigma dz.
\]

In discrete time, this can be written as:

\[
\Delta x_t = \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \sqrt{\Delta t} \epsilon_t,
\]

where \( \epsilon_t \sim N(0, 1) \). Expanding further:

- \( x_1 = x_0 + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \sqrt{\Delta t} \epsilon_1 \),  
- \( x_2 = x_1 + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \sqrt{\Delta t} \epsilon_2 \),  
- \( \dots \),  
- \( x_n = x_{n-1} + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \sqrt{\Delta t} \epsilon_n \).  

### Pricing European-Style Options

The price of the option is computed as:

\[
P = E(X) e^{-rT},
\]

where:  
- \( P \): Option price  
- \( E(X) \): Expected payoff  
- \( r \): Risk-free rate  
- \( T \): Time to maturity  

### Simulation Steps

1. Simulate the stock price history from \( t = 0 \) to \( t = T \) using \( \Delta t = 0.004 \).  
2. Compute the payoff \( X(k) \) for each simulation \( k \).  
3. Repeat for 10,000 simulations.  
4. The option price is then:

\[
P = \left( \frac{1}{10,000} \sum_{k=1}^{10,000} X(k) \right) e^{-rT}.
\]

### Assumptions

- Initial stock price: \( S_0 = 100 \)  
- Risk-free rate: \( r = 5\% \)  
- Dividend yield: \( q = 2\% \)  
- Volatility: \( \sigma = 40\% \)  
- Number of trading days in a year: 250  
- Time step: \( \Delta t = \frac{1}{250} = 0.004 \)
