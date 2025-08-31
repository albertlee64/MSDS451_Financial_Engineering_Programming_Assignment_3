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



