# Avellaneda–Stoikov Market-Making Model

An educational Python implementation of the Avellaneda–Stoikov framework for
inventory-aware market making. The project simulates a mid-price, calculates
optimal bid and ask quotes, models stochastic order arrivals and tracks the
market maker's inventory and mark-to-market P&L.

## Model intuition

The market maker adjusts its quotes according to its inventory. Its reservation
price is

$$r_t = S_t - q_t\gamma\sigma^2(T-t),$$

where $S_t$ is the mid-price, $q_t$ the inventory, $\gamma$ risk aversion,
$\sigma$ volatility and $T-t$ the remaining horizon. A long inventory lowers
the reservation price and encourages selling; a short inventory raises it and
encourages buying.

The implementation uses the finite-horizon half-spread

$$\delta_t = \frac{\gamma\sigma^2(T-t)}{2}
+ \frac{1}{\gamma}\log\left(1+\frac{\gamma}{k}\right).$$

The execution probability is approximated over each small time interval using
the exponential intensity $\lambda(\delta)=A e^{-k\delta}$.

## What the simulation shows

- Arithmetic Brownian motion for the mid-price
- Inventory-dependent reservation price
- Optimal bid and ask quotes
- Stochastic bid and ask executions
- Inventory and mark-to-market P&L through time

## Run locally

```bash
git clone https://github.com/YOUR-USERNAME/avellaneda-stoikov-market-making.git
cd avellaneda-stoikov-market-making
python -m venv .venv
pip install -r requirements.txt
python avellaneda_stoikov.py
```

## Parameters

| Parameter | Meaning | Default |
|---|---|---:|
| `s0` | Initial mid-price | 100 |
| `sigma` | Price volatility | 2.0 |
| `gamma` | Inventory-risk aversion | 0.1 |
| `horizon` | Trading horizon | 1.0 |
| `a` | Baseline order-arrival intensity | 140 |
| `k` | Intensity decay with quote distance | 1.5 |
| `steps` | Number of simulation steps | 1,000 |

## Limitations and possible extensions

This is a simplified educational model, not a production trading system. It
assumes constant volatility and liquidity parameters, independent fills, no
fees, no latency and an arithmetic Brownian mid-price. The execution rule uses
a discrete-time approximation. Natural extensions include Monte Carlo
performance analysis, inventory limits, parameter sensitivity tests,
transaction costs and calibration with order-book data.

## Reference

Avellaneda, M. and Stoikov, S. (2008), *High-frequency trading in a limit order
book*, Quantitative Finance, 8(3), 217–224.
