# Markowitz Portfolio Optimizer

A Python-based portfolio optimization system built on **Modern Portfolio Theory (MPT)** that identifies optimal asset allocations by balancing expected returns against investment risk.

The project combines historical stock market data, LSTM-based price predictions and quantitative portfolio optimization to evaluate investment opportunities and construct portfolios under different risk constraints.

## Overview

The **Markowitz Portfolio Optimizer** implements Harry Markowitz's Modern Portfolio Theory to help identify efficient portfolio allocations.

It uses historical and predicted stock performance data to estimate expected returns and asset covariance, enabling the construction of portfolios that:

- Maximize expected returns for a given level of risk.
- Minimize portfolio risk for a specified return target.
- Identify the Minimum Variance Portfolio.
- Identify the Maximum Sharpe Ratio Portfolio.
- Optimize asset allocation according to user-defined risk capacity.

The system also incorporates an LSTM-based prediction pipeline to forecast stock prices and generate the data used for predictive portfolio analysis.

## Features

- **Return Estimation:** Calculate expected asset returns using historical and predicted performance data.
- **Covariance Analysis:** Compute covariance matrices to evaluate relationships between asset returns.
- **Efficient Frontier:** Identify optimal portfolios across different risk-return combinations.
- **Minimum Variance Optimization:** Determine the portfolio with the lowest achievable variance.
- **Maximum Sharpe Ratio:** Identify portfolio allocations that maximize risk-adjusted returns.
- **Risk-Constrained Optimization:** Generate portfolio allocations based on user-defined annual volatility targets.
- **LSTM-Based Prediction:** Forecast stock prices using historical market data and TensorFlow.
- **Data Visualization:** Plot the efficient frontier, optimal portfolios and actual-versus-predicted stock performance.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Portfolio Optimization | PyPortfolioOpt |
| Numerical Computing | NumPy |
| Data Processing | Pandas |
| Visualization | Matplotlib |
| Machine Learning | TensorFlow (LSTM) |
| Market Data | yfinance |
| LLM Integration | LangChain, Groq |

## Project Structure

```text
Markowitz-Portfolio-Optimizer/
│
├── main.py
│   └── Main execution pipeline and portfolio optimization
│
├── plot.py
│   └── Portfolio analysis and visualization
│
├── predict_performance.py
│   └── Stock price prediction using LSTM
│
├── utility.py
│   └── Shared utility and response-handling functions
│
├── requirements.txt
│   └── Project dependencies
│
├── response.json
│   └── Conversation and tool-call response storage
│
├── Predicted_performance/
│   ├── AAPL_2024_predictions.csv
│   ├── GOOG_2024_predictions.csv
│   └── ...
│
├── .env
│   └── Environment variables and API credentials
│
└── LICENSE
```

## System Workflow

The project follows two major stages: stock performance prediction and portfolio optimization.

### 1. Stock Data Retrieval and Prediction

Implemented in `predict_performance.py`.

1. Fetch historical stock market data using `yfinance`.
2. Prepare historical price data for model training.
3. Train an LSTM neural network using TensorFlow on data up to 2023.
4. Generate stock price predictions for 2024.
5. Compare predicted prices against actual market prices.
6. Save the resulting data as CSV files in `Predicted_performance/`.

Each prediction CSV is expected to contain:

| Column | Description |
|---|---|
| Date | Trading date |
| Actual | Actual stock performance |
| Predicted | Model-predicted performance |

### 2. Data Loading and Return Estimation

Implemented in `main.py` and `plot.py`.

The `load_returns` function reads the prediction CSV files and combines their data into separate DataFrames for actual and predicted performance.

These DataFrames are indexed by date and used to calculate expected returns and covariance matrices.

### 3. Portfolio Optimization

Implemented using the `PyPortfolioOpt` library.

The `EfficientFrontier` class is used to determine optimal portfolio allocations based on the estimated returns and covariance matrix.

The optimization process identifies:

- Minimum Variance Portfolio.
- Maximum Sharpe Ratio Portfolio.
- Efficient Frontier portfolios.

The resulting portfolio weights represent the proportion of capital allocated to each asset.

### 4. Risk-Constrained Optimization

Implemented in `main.py`.

The `optimize_for_risk_capacity` function performs portfolio optimization under a user-defined annual volatility target.

The `prompt_risk_capacity` function handles user input and normalizes the specified risk capacity before passing it to the optimization process.

This allows users to explore portfolio allocations aligned with their selected risk constraints.

### 5. Visualization and Analysis

Implemented in `plot.py` and `predict_performance.py`.

Matplotlib is used to visualize:

- Efficient Frontier.
- Optimal portfolio allocations.
- Risk-return relationships.
- Actual versus predicted stock prices.

These visualizations help interpret the optimization results and evaluate model predictions.

## Key Concepts

### Modern Portfolio Theory (MPT)

Modern Portfolio Theory focuses on constructing portfolios by considering both expected returns and portfolio risk rather than evaluating individual assets independently.

### Efficient Frontier

The Efficient Frontier represents portfolios offering the highest expected return for each given level of risk, or equivalently, the lowest risk for a given expected return.

### Minimum Variance Portfolio

The portfolio allocation that minimizes overall portfolio variance based on the covariance between assets.

### Maximum Sharpe Ratio Portfolio

The portfolio that maximizes the Sharpe Ratio, measuring excess return relative to portfolio volatility.

### Risk-Constrained Optimization

An optimization approach that incorporates a target portfolio volatility to determine an allocation that seeks to maximize expected returns within the specified risk constraint.

## Installation and Setup

### Prerequisites

- Python 3.9 or later.
- pip package manager.
- Groq API key.

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Markowitz-Portfolio-Optimizer
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file in the project root directory and add your Groq API key:

```env
GROQ_API_KEY=your_groq_api_key
```

### 4. Prepare Prediction Data

Ensure that the required stock prediction CSV files are available in the `Predicted_performance/` directory.

Each CSV should contain the expected `Date`, `Actual`, and `Predicted` columns.

### 5. Run the Application

```bash
python main.py
```

The main execution script loads the available performance data, performs portfolio optimization using the Sharpe Ratio and subsequently prompts the user to specify their risk capacity for risk-constrained optimization.

## Dependencies

The project uses the following major libraries:

- **PyPortfolioOpt:** Portfolio optimization, expected return estimation and covariance analysis.
- **NumPy:** Numerical computations.
- **Pandas:** Financial time-series data processing.
- **Matplotlib:** Portfolio and prediction visualizations.
- **TensorFlow:** LSTM-based stock price prediction.
- **yfinance:** Historical stock market data retrieval.
- **LangChain and Groq:** Language model integration.

For the complete dependency list, refer to `requirements.txt`.

## License

This project is distributed under the license specified in the `LICENSE` file.
