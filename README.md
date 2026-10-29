# Financial Volatility & Logarithmic Return Analyzer 📈

A quantitative Python analysis tool designed to fetch historical market prices, compute daily logarithmic return distributions, and analyze 30-day rolling annualized volatility dynamics across major financial assets (`S&P 500`, `AAPL`, `MSFT`).

---

## 📌 Theoretical & Quantitative Foundations

### 1. Logarithmic Returns ($\ln$)
Rather than using simple percentage returns, this project models price changes using daily continuously compounded (logarithmic) returns:

$$r_t = \ln\left(\frac{P_t}{P_{t-1}}\right) = \ln(P_t) - \ln(P_{t-1})$$

* **Time Additivity:** Log returns sum directly over time periods: $r_{\text{total}} = \sum r_t$.
* **Symmetry & Stationarity:** Eliminates scale asymmetry between positive and negative price moves, aligning closer to a Gaussian distribution required by machine learning models.
* **Computational Efficiency:** Vectorized log subtraction reduces floating-point errors across large time series.

### 2. Volatility & Annualization
* **Daily Volatility ($\sigma_{\text{daily}}$):** Calculated as the standard deviation of daily log returns:

$$\sigma_{\text{daily}} = \sqrt{\frac{1}{N-1} \sum_{t=1}^{N} (r_t - \bar{r})^2}$$

* **Annualized Volatility ($\sigma_{\text{annual}}$):** Scaled using the standard market convention of **252 trading days** per calendar year:

$$\sigma_{\text{annual}} = \sigma_{\text{daily}} \times \sqrt{252}$$

### 3. 30-Day Rolling Windows & Base-100 Normalization
* **Rolling Volatility:** Captures dynamic risk clustering over time instead of relying on a static historical average.
* **Base-100 Indexing:** Rescales initial prices to $100$ ($P_{\text{norm}} = \frac{P_t}{P_0} \times 100$) to enable direct visual comparison of growth rates across assets of varying price scales.

---

## 🛠️ Tech Stack & Dependencies

* **Language:** Python 3.10+
* **Data Ingestion:** `yfinance` (Yahoo Finance API with `auto_adjust=True`)
* **Data Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`

---

## 📊 Key Takeaways & Visual Insights

1. **Risk-Return Trade-off:** Tech equities (`AAPL`, `MSFT`) exhibit higher annualized volatility relative to the benchmark market index (`^GSPC`).
2. **Volatility Clustering:** Spikes in 30-day rolling volatility strongly correlate with localized market drawdowns and macroeconomic shock events.

---

## 🚀 How to Run

1. Open `financial_volatility_analyzer.ipynb` in **Google Colab** or Jupyter Notebook.
2. Run all cells sequentially to download market data, calculate metrics, and generate the charts.
