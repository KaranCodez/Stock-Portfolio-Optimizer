Markowitz Portfolio Optimizer
________________________________

A tool for optimizing investment portfolios using Markowitz's modern portfolio theory.

This project provides a Python implementation of the Markowitz Portfolio Optimization model, also known as Modern Portfolio Theory (MPT). It allows users to find the optimal asset allocation for their portfolio to maximize expected return for a given level of risk, or minimize risk for a given level of expected return. It is designed for individual investors, financial analysts, and students interested in quantitative finance.

### Features

*   Calculate expected returns and covariance matrix for a set of assets.
*   Identify the efficient frontier for a given set of assets.
*   Determine the portfolio with the minimum variance.
*   Determine the portfolio with the maximum Sharpe Ratio.
*   Visualize the efficient frontier and optimal portfolios.
This project provides functionality to analyze historical and predicted stock performance data to construct optimal investment portfolios. It helps users make informed decisions by identifying portfolios that maximize returns for a given level of risk or minimize risk for a target return, based on both actual historical data and model predictions.

Tech Stack
___________

Python
LangChain
Groq
NumPy
Pandas
Matplotlib
TensorFlow
yfinance


Install dependencies:
pip install -r requirements.txt
Set up environment variables: Create a .env file in the root directory and add your Groq API key:
GROQ_API_KEY="your_groq_api_key"
Run the optimizer:
python main.py
The script will load predicted performance data, calculate optimal portfolios based on the Sharpe ratio, and then prompt the user for their risk capacity to perform risk-constrained optimization.

Project Structure
.
├── .env
├── LICENSE
├── main.py
├── plot.py
├── predict_performance.py
├── requirements.txt
├── response.json
├── utility.py
└── Predicted_performance/
 ├── AAPL_2024_predictions.csv
 └── GOOG_2024_predictions.csv
 └── ...
Key Concepts
Data Loading (main.py, plot.py): The load_returns function reads CSV files from the Predicted_performance directory. Each CSV is expected to contain 'Date', 'Actual', and 'Predicted' columns for a specific stock symbol. These are merged into two DataFrames: one for actual returns and one for predicted returns, indexed by date.
Portfolio Optimization (main.py, plot.py): The PyPortfolioOpt library is used to calculate expected returns and covariance matrices from the loaded return data. The EfficientFrontier class is then employed to find optimal portfolios, such as the maximum Sharpe ratio portfolio and portfolios optimized for a specific risk capacity (target volatility).
Risk-Constrained Optimization (main.py): The optimize_for_risk_capacity function allows users to specify a target annual volatility. The optimizer then finds the portfolio weights that aim to achieve this volatility while maximizing expected return. User input for risk capacity is handled and normalized in the prompt_risk_capacity function.
LSTM Stock Prediction (predict_performance.py): This script demonstrates how to fetch historical stock data using yfinance, train a Long Short-Term Memory (LSTM) neural network using TensorFlow on data up to 2023, predict prices for 2024, and save these predictions along with actual prices to CSV files in the Predicted_performance directory. It also generates plots comparing actual and predicted prices.
Utility Functions (utility.py): This module contains helper functions such as remove_think for cleaning text output from language models and append_to_response for logging conversation history and tool calls to a JSON file.
