# Monte Carlo Simulations 

This application was created to run mock Monte Carlo simulations on the portfolio of 2 hypothetical investors. We are determining their readiness to retire by analyzing their portfolio consisting of Bitcoin, Ethereum, SPY and AGG to determine if retiring in 10 years is realistic. 

---

## Technologies 

This application runs on Python 3.7. We also use the Free Crypto API to obtain Bitcoin and Ethereum prices. In order to obtain said cryptocurrency prices, we run the following code:

```python
btc_response = requests.get(btc_url).json()
print(json.dumps(btc_response, indent=4, sort_keys=True))
```

We then use the Alpaca API and SDK to obtain ticker SPY and AGG price history. First we need to create a .env file with the Alpaca API Key and the Secret Key with the following code: 

```python
alpaca_api_key = os.getenv("ALPACA_API_KEY")
alpaca_secret_key = os.getenv("ALPACA_SECRET_KEY")

alpaca = tradeapi.REST(
    alpaca_api_key,
    alpaca_secret_key,
    api_version="v2"
)
```

Finally, in order to run our Monte Carlo simulations we need to have the pre-written MCForecastTools.py file in our folder library. Then we run the following code:

```python
MC_run = MCSimulation(
    portfolio_data = stock2_df,
    weights= [.6, .4],
    num_simulation=500,
    num_trading_days=252*30
)

# Run the Monte Carlo simulation to forecast 30 years cumulative returns
MC_run.calc_cumulative_return()

# Visualize the probability distribution of the 30-year Monte Carlo simulation by plotting a histogram
hist_plot = MC_run.plot_distribution()
```

---

## Libraries

This analysis used extensive DataFrame manipulation with Pandas, plotting with matplotlib and the Path function from pathlib to refer to files in other directories. Import statements already present in program, refer to them below:

```python
import os
import requests
import json
import pandas as pd
from dotenv import load_dotenv
import alpaca_trade_api as tradeapi
from MCForecastTools import MCSimulation
%matplotlib inline
```

---

## Database

This program couldn't run without the pre-written Monte Carlo simulation tools:

* MCForecastTools.py

---

## Contributors

Thank you for Eric Cardena for teaching Rice's FinTech Boot Camp. He was instrumental in teaching and helping us understand this material. Thank you for Rice for preparing this curriculum and the corresponding data sets that are required to be used. 

**Rishi Prasadha**

**LinkedIn**: https://www.linkedin.com/in/rishi-prasadha-912212133/

**Instagram**: @therishiprasadha

**Twitter**: @RishiPrasadha

---

## Licenses 

MIT