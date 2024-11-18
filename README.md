# Methodology

The model of Black and Scholes (1973) implies that it is possible to price European-style derivatives by simulating the stock price under the risk-neutral measure and discounting expected payoffs at the risk-free rate.

Black, Fischer, and Myron Scholes. 1973. "The Pricing of Options and Corporate Liabilities." *Journal of Political Economy* 81 (3): 637–54.

Consider a stock with price $S$ that pays a dividend yield $q$ and whose risk-neutral dynamics are given by

$$
\frac{dS}{S} = (r - q) dt + \sigma dz
$$

where $r$ denotes the continuously compounded risk-free rate and $z$ is a Brownian motion. If we denote $x = \ln(S)$, Ito’s lemma implies that

$$
dx = \left(\mu - \frac{1}{2} \sigma^2 \right) dt + \sigma dz
$$

We can express the previous expression in discrete time as

$$
\Delta x_t = \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \Delta z_t = \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \Delta t \epsilon_t + \Delta t
$$

which implies

$$
x_1 \Delta t = x_0 \Delta t + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \Delta t \epsilon_1
$$

$$
x_2 \Delta t = x_1 \Delta t + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \Delta t \epsilon_2
$$

$$
x_3 \Delta t = x_2 \Delta t + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \Delta t \epsilon_3
$$

...

$$
x_n \Delta t = x_{n-1} \Delta t + \left( \mu - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \Delta t \epsilon_n
$$

In this project, you will be pricing European-style options expiring in $T = 0.75$ years by assuming that the stock price changes every trading day. If we assume that there are 250 trading days in a year, this implies that $\Delta t = \frac{1}{250} = 0.004$ years. Therefore, for each path or history of the stock price, you will pick 250 independent $N(0,1)$ random numbers in order to compute the simulated path.

You will simulate 10,000 different paths or histories of the stock. The price of each option will be computed as the average payoff at maturity discounted at the risk-free rate. Note that for some options, the payoff might depend on the whole history of the stock price. If $X = f(\{ S \}_{t=0}^{T})$ denotes the potentially path-dependent payoff of the option, its price is given by

$$
P = \mathbb{E}(X) e^{-rT}
$$

Therefore:

- Simulate the price history from $t = 0$ until $t = T$ using a $\Delta t = 0.004$.
- Compute the payoff $X(k)$ of the option in simulation $k$.
- Do this 10,000 times.

Once you have all 10,000 simulations, the price of the option will be given by

$$
P = \left( \frac{1}{10,000} \sum_{k=1}^{10,000} X(k) \right) e^{-rT}
$$

We will assume in the following that the stock price today is $S_0 = 100$, $r = 5\%$, $q = 2\%$, and $\sigma = 40\%$.


## Methodology File: `Methodology.py`

The `Methodology.py` file contains the core functions to simulate stock prices and calculate option prices.

### Functions in `Methodology.py`

1. **`stock_price(s_0=100, dt=0.004, r=0.05, q=0.02, vol=0.4, period=250)`**
   - Simulates the stock price over a period (typically 250 trading days).
   - **Parameters**:
     - `s_0`: Initial stock price (default is 100)
     - `dt`: Time step (default is 0.004, corresponding to 1 day in a 250-day year)
     - `r`: Risk-free rate (default is 5%)
     - `q`: Dividend yield (default is 2%)
     - `vol`: Volatility (default is 40%)
     - `period`: Number of trading days (default is 250)
   - **Returns**: A numpy array of stock prices over the specified period.

2. **`simulation(iterations=10000, period=250)`**
   - Simulates multiple stock price paths for a given number of iterations.
   - **Parameters**:
     - `iterations`: Number of simulated paths (default is 10,000)
     - `period`: Number of trading days for each path (default is 250)
   - **Returns**: A 2D numpy array of simulated stock prices with shape `(iterations, period)`.

3. **`option_price(option_payoff, rate=0.05, T=0.75)`**
   - Computes the price of an option based on the average payoff of all simulations, discounted at the risk-free rate.
   - **Parameters**:
     - `option_payoff`: Array of option payoffs from simulations
     - `rate`: Risk-free rate (default is 5%)
     - `T`: Time to maturity (default is 0.75 years)
   - **Returns**: The price of the option.

4. **`plotting(payoffs, name)`**
   - Plots the payoff histogram of the option with the average payoff displayed on the plot.
   - **Parameters**:
     - `payoffs`: Array of option payoffs from simulations
     - `name`: Name of the option (e.g., "Lookback Call Option")
   - **Returns**: Displays a histogram plot of the payoffs.

5. **`lookBackCallPrice(sim=simulation())`**
   - Simulates the price of a Lookback Call Option by calculating payoffs based on the minimum stock price during the option’s life.
   - **Parameters**:
     - `sim`: A simulation of stock prices (default is 10,000 iterations)
   - **Returns**: Prints the price of the Lookback Call Option and shows the payoff histogram.

6. **`lookBackPutPrice(sim=simulation())`**
   - Simulates the price of a Lookback Put Option by calculating payoffs based on the maximum stock price during the option’s life.
   - **Parameters**:
     - `sim`: A simulation of stock prices (default is 10,000 iterations)
   - **Returns**: Prints the price of the Lookback Put Option and shows the payoff histogram.

## Jupyter Notebook: `OptionsPricing.ipynb`

The Jupyter Notebook uses the functions in `Methodology.py` to simulate stock price paths, calculate option payoffs, and compute the option price.

1. **Simulating Stock Prices**:
   - The `simulation` function is called to generate 10,000 simulated stock price paths, based on the specified parameters (e.g., `S0 = 100`, `r = 5%`, `q = 2%`, `sigma = 40%`).

2**Pricing the Option**:
   - The _`Price` functions are then used to compute the payoffs and then the price of the option by averaging the payoffs across all simulations and discounting the result at the risk-free rate.

## Requirements

This project requires the following Python packages:

- `numpy`
- `matplotlib`


