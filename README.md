# Quant Atlas

Quant Atlas is a computational framework for the calibration and analysis of stochastic volatility models. The platform provides a high-fidelity pipeline for mapping empirical market data to the Heston-Hull-White parameter space, utilizing a modular architecture designed for research and production-grade derivative pricing.

## Mathematical Framework

The primary objective of the engine is the calibration of the Heston stochastic volatility model, defined by the following system of coupled stochastic differential equations (SDEs):

$$dS_t = \mu S_t dt + \sqrt{v_t} S_t dW_t^1$$
$$dv_t = \kappa(\theta - v_t) dt + \sigma \sqrt{v_t} dW_t^2$$

where $dW_t^1 dW_t^2 = \rho dt$. Quant Atlas facilitates the estimation of the risk-neutral parameter set $\Theta = \{\kappa, \theta, \sigma, \rho, v_0\}$ by minimizing the objective function between market-observed mid-prices and model-implied values.

## System Architecture

The software is partitioned into distinct functional layers to maintain mathematical integrity and computational efficiency:

### 1. Market Data Ingestion
* **Multi-Source Retrieval**: Automated extraction of underlying equity spots, multi-expiry option chains, and sovereign yield curves for risk-free rate modeling.
* **Atlas Caching Layer**: Implementation of a persistent memoization pattern via Python decorators. This ensures idempotency and optimizes the data-acquisition layer for iterative model testing.

### 2. Transformation and Signal Processing
* **Vectorized Data Cleaning**: Transformation of raw market data into dimensionless variables, including moneyness ($M = K/S$) and annualized time-to-maturity ($T$).
* **Liquidity Constraints**: Automated filtration of the volatility surface based on bid-ask spreads, volume signatures, and extreme moneyness bounds (0.8 < M < 1.2) to ensure the stability of the calibration.

### 3. Calibration and Estimation (In Development)
* **Optimization Protocols**: Integration of local and global search algorithms for high-dimensional parameter estimation.
* **Neural Network Surrogates**: Implementation of deep learning models to approximate the inverse mapping from volatility surfaces to stochastic parameters.

## Technical Specifications

* **Environment**: Python 3.10+
* **Core Dependencies**: `numpy`, `pandas`, `scipy`, `yfinance`, `curl_cffi`
* **Data Persistence**: Serialized binary storage (Pickle) for local state management.

