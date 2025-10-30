# Econophysics Project: Gaussian vs. Lévy Analysis of Financial Time Series

This repository contains a Python-based project that empirically analyzes high-frequency financial time series, based on the foundational concepts in "An Introduction to Econophysics" by Mantegna & Stanley.

The project's goal is to **test the statistical model of financial returns** by comparing the **Gaussian hypothesis (Chapter 3)** with the **Lévy Stable hypothesis (Chapter 4)**.

---

## ⚛️ Key Concepts Tested

This analysis is a *descriptive* data science project, not a *predictive* machine learning one. We are trying to *model the underlying stochastic process* of the market.

* **Random Walk (Ch. 3):** Modeling price changes as a sum of random steps ($S_n = \sum x_i$).
* **Central Limit Theorem (Ch. 3):** The hypothesis that if returns have *finite variance*, their sum should converge to a **Gaussian (Normal) distribution**.
* **Leptokurtosis ("Fat Tails"):** The observed feature that real financial returns have more extreme events (crashes, booms) than a Gaussian distribution predicts.
* **Lévy Stable Distributions (Ch. 4):** A class of distributions that have **power-law tails** ($P(x) \sim |x|^{-(1+\alpha)}$) and act as the attractor for sums of variables with *infinite variance* (the Generalized CLT).
* **Scaling Laws:** The core of the analysis. We test how the *shape* of the return distribution $P(S_n)$ changes as we increase the time window $n$.

---

## 📈 Methodology

The project is implemented in the `Econophysics_Analysis.ipynb` Jupyter Notebook and follows these 3 steps:

1.  **Visualize "Fat Tails":** We plot the probability density function (PDF) of 1-minute log-returns and overlay a Gaussian distribution with the same mean and variance. This visually confirms that the Gaussian model is a poor fit for real data.
2.  **Find the Scaling Exponent ($\alpha$):** We test the scaling of the "probability of return to the origin" $P(S_n=0)$. For a stable process, $P(S_n=0) \sim n^{-1/\alpha}$. We plot $\log(P(S_n=0))$ vs. $\log(n)$ and find the slope to empirically solve for $\alpha$. If $\alpha \approx 2$, the process is Gaussian. If $\alpha < 2$, it is non-Gaussian and in the Lévy basin of attraction.
3.  **Perform Data Collapse:** We use our empirical $\alpha$ to scale all the PDFs from different time intervals. If the hypothesis is correct, all the curves will "collapse" onto a single, universal curve, proving the self-similar nature of the process.

---

## ⚠️ A Critical Note on Data

This project **requires high-frequency (intraday) data** (e.g., 1-minute or 5-minute resolution) to properly observe the scaling laws, as shown in the book.

* **I CANNOT PROVIDE THIS DATA.** Large, high-frequency datasets are proprietary or must be purchased.
* You can find some sample datasets on platforms like **Kaggle** or from specialized vendors.
* The notebook is written to read a simple CSV file named `data/high_frequency_data.csv` with a `timestamp` and `price` column. **You must acquire this file yourself.**
* A "demo" section using `yfinance` for *daily* data is included, but it is **not sufficient** for the full scaling analysis (as $n=1$ is already a full day).

---

## 🚀 How to Run

1.  **Clone this repository:**
    ```bash
    git clone [YOUR_REPO_URL]
    cd [YOUR_REPO_NAME]
    ```

2.  **Create a virtual environment (Recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Get Your Data:**
    * Find a high-frequency (1-minute) CSV dataset of a market index (like S&P 500, NIFTY 50, etc.).
    * Create a folder named `data`.
    * Save your file as `data/high_frequency_data.csv`. Ensure it has `timestamp` and `price` columns.

5.  **Run the analysis:**
    * Launch Jupyter Notebook:
        ```bash
        jupyter notebook
        ```
    * Open and run the cells in `Econophysics_Analysis.ipynb`.

---

## 📚 References

* Mantegna, R. N., & Stanley, H. E. (2000). *An Introduction to Econophysics: Correlations and Complexity in Finance*. Cambridge University Press.
