# MSDS451 Financial Engineering Programming Assignment 3
Multi-Level Prediction Trader

This repository implements an end-to-end functional prototype algorithmic trading system based on simple predictive signals (mean reversion and momentum). The framework demonstrates how to transform signals into discrete trading actions (BUY/SELL/HOLD), backtest strategies under realistic conditions, and evaluate both predictive accuracy and hit rate.

The project with a focus on the trading pipeline and risk evaluation rather than predictive model sophistication. The paper highlights the history of algorithmic trading and how we got to where we are today where more and more banks / investment firms are leveraging AI within their algorithmic trading models now. The paper includes the data preparation, model, results, and future improvements.

## Data Preparation and Pipeline

The Python notebook developed uses automated, algorithmic trading based on multi-level prediction and future returns. The cutoffs in the multi-level prediction are based on the trading actions listed in the assignment:

<img width="468" height="223" alt="image" src="https://github.com/user-attachments/assets/01dcf817-7b50-4616-8934-5982a74c24e2" />

Buy: Take a long position, purchase a call option
Hold: Keep current positions, do nothing
Sell: Take a short position, purchase a put option

The data preparation of the notebook begins by constructing a reproducible data pipeline to support systematic trading analysis. A config dataclass is introduced to consolidate the defined parameters such as ticker symbol, lookback horizon, strategy type (mean reversion or momentum), and risk profile (as shown above). The asset price history is retrieved through yfinance, and exploratory data analysis (EDA) is conducted to understand the statistical properties of the asset. The asset chosen initially was Apple or AAPL. The initial strategy used was a mean-reversion trading strategy. Mean-reversion signal measures the tendency of short-term losses to reverse, while the momentum signal captures the persistence of cumulative returns. Since I wanted flexibility in the model to be able to easier change the ticker symbol, risk profile, or strategy, I developed an in-notebook python widget that uses is based on ipywidgets. The second asset chosen for this assignment was Microsoft or MSFT. I was also hoping that this model can be potentially used for my own personal investment decisions as well.

AAPL EDA:

<img width="850" height="371" alt="image" src="https://github.com/user-attachments/assets/8758c9b8-ff66-42ee-a163-84c0fa07fde8" />

<img width="858" height="507" alt="image" src="https://github.com/user-attachments/assets/d69bdf72-a68f-4e2d-8eb5-6261f4f79d2f" />

<img width="711" height="318" alt="image" src="https://github.com/user-attachments/assets/3dab9462-c9d8-4f90-b3ea-67fe87e3e125" />


MSFT EDA:

<img width="842" height="371" alt="image" src="https://github.com/user-attachments/assets/048923ad-65b8-4905-b710-e52a345def7e" />

<img width="858" height="507" alt="image" src="https://github.com/user-attachments/assets/6e7ff200-703d-457d-9269-7e438e4ee77e" />

<img width="711" height="318" alt="image" src="https://github.com/user-attachments/assets/d81ad065-bef1-4353-8d16-8164e21160a9" />


## Programming

The programming component of the notebook includes the trading logic, performance evaluation, and diagnostics. The core engine is backtest_singnals, which simulates the daily equity curve by combining positions with realized returns, and deducting slippage. This backtester produces both a detailed trade-level record and an equity time series, which are then summarized into standard metrics including compound annual growth rate (CAGR), annualized volatility, Sharpe ratio, maximum drawdown, and Calmar ratio. The model also outputs the latest trading recommendation and decision evidence, reinforcing the link between predictive signals and actionable strategy outputs.

Using AAPL, the model is outputting the following latest recommendation:

{'date': '2025-08-29', 'ticker': 'AAPL', 'score': 0.5932, 'action': 'HOLD', 'position': 0.0, 'price': 232.13999938964844}

CAGR: None
AnnVol:  0.2677
Sharpe: -0.0399
MaxDD: -0.7850

<img width="468" height="302" alt="image" src="https://github.com/user-attachments/assets/1c0edbca-f643-428d-9785-0ee563c6484c" />

The signal strength is driven by the “score” and it’s currently 0.5932 which sits between the BUY and SELL cutoffs for the chosen risk profile or a HOLD.

For MSFT, the model is outputting the following latest recommendation: 

{'date': '2025-08-29', 'ticker': 'MSFT', 'score': 0.6231, 'action': 'BUY', 'position': 1.0, 'price': 506.69000244140625}

CAGR: None
AnnVol:  0.1737
Sharpe: -0.0149
MaxDD: -0.7528

<img width="468" height="302" alt="image" src="https://github.com/user-attachments/assets/b29fe3c2-03e6-4009-a29e-939ab71d03f0" />

Using the score signal again, MSFT is indicating as a BUY based on the model. The strategy delivered similarly weak outcomes when applied to both Apple (AAPL) and Microsoft (MSFT), though with slightly different risk profiles. For AAPL, the model produced no compounding growth, an annualized volatility of 26.8%, a negative Sharpe ratio (−0.04), and an extreme maximum drawdown of −78.5%. For MSFT, results were marginally less volatile but no more profitable: annualized volatility of 17.4%, a near-zero Sharpe ratio (−0.02), and a maximum drawdown of −75.3%. Trade logs for MSFT from August 2025 illustrate the mechanism of underperformance which resulted in scores drifting into the BUY territory.

