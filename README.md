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
