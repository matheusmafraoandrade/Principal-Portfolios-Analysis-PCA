# Principal Portfolio Analysis: PCA and Portfolio Optimization

## Overview

This project applies Principal Component Analysis (PCA) to the construction of simplified portfolios based on Brazilian equities.

The main objective is to investigate whether the common variation across a broad set of stocks can be represented by a smaller number of principal portfolios, reducing the dimensionality of the investment universe while preserving relevant information about return dynamics.

Using daily stock returns from the Brazilian equity market, the project extracts principal components, constructs corresponding principal portfolios, and explores portfolio allocation through mean-variance optimization.

The Ibovespa is included as a market benchmark.

## Methodology

The analysis is organized into four main stages.

### 1. Data Collection and Preparation

- Retrieve historical adjusted stock returns for Ibovespa constituents using the `BatchGetSymbols` R package.
- Collect daily log returns for individual stocks.
- Reshape the data into a date-by-asset matrix.
- Retain observations with complete data across the selected stocks.
- Obtain Ibovespa historical returns as a benchmark.

The effective dataset used in the notebook contains 67 stocks and 2,456 daily observations, covering June 2011 to May 2021.

### 2. Principal Component Analysis

PCA is applied to standardized stock returns to identify the main sources of common variation across assets.

The analysis includes:

- Standardization of stock returns.
- Eigenvalue and eigenvector decomposition through PCA.
- Explained variance analysis.
- Component selection using the Kaiser criterion.
- Inspection of component loadings and biplots.

The selected principal components are subsequently used to construct principal portfolios.

### 3. Principal Portfolio Construction

The eigenvectors obtained from PCA are transformed into portfolio weights.

For each selected component, positive and negative loadings are normalized separately, generating long and short exposures.

The resulting principal portfolios are used to calculate portfolio return series, which provide a reduced representation of the original stock universe.

### 4. Portfolio Optimization and Risk Analysis

The principal portfolios are then used as building blocks for portfolio allocation.

The analysis explores:

- Annualized expected returns and volatility.
- Value at Risk (VaR) estimates.
- Random portfolio generation.
- Mean-variance portfolio allocation.
- Sharpe ratio maximization.
- Minimum-volatility optimization.

Numerical optimization is performed using the Sequential Least Squares Programming (SLSQP) algorithm, subject to fully invested and long-only constraints at the principal-portfolio allocation level.

## Repository Structure

```text
Principal-Portfolios-Analysis-PCA/
│
├── ibovespa_ETL.R
├── principal_portfolios_analysis.ipynb
└── README.md
```

- `ibovespa_ETL.R`: Retrieves historical stock returns and prepares the input dataset.
- `principal_portfolios_analysis.ipynb`: Performs data preparation, PCA, principal portfolio construction, risk analysis, and portfolio optimization.

## Technologies

**R**
- BatchGetSymbols
- tidyverse
- ggplot2

**Python**
- NumPy
- pandas
- Matplotlib
- scikit-learn
- pandas-datareader
- SciPy

## Data and Execution

The R script retrieves historical stock data and exports the resulting observations to a CSV file named `cotacoes.csv`.

The Python notebook reads this file as its input and performs the subsequent analysis.

To reproduce the workflow:

1. Run `ibovespa_ETL.R` to retrieve the stock return data.
2. Ensure that `cotacoes.csv` is saved in the project directory.
3. Update the file path in the notebook if necessary.
4. Execute `principal_portfolios_analysis.ipynb`.

The notebook also retrieves Ibovespa benchmark data through `pandas-datareader`.

## Scope and Limitations

This project is an empirical application of PCA-based portfolio construction and classical portfolio optimization.

The analysis focuses on dimensionality reduction and the use of principal portfolios as inputs to portfolio allocation.

The current implementation does not constitute a fully specified index-tracking strategy or a comprehensive out-of-sample investment backtest. Results should therefore be interpreted as an exploratory application of statistical portfolio construction methods.

## Author

Developed as a college seminar in the subject Financial Econometrics.

[GitHub Repository](https://github.com/matheusmafraoandrade/Principal-Portfolios-Analysis-PCA)
