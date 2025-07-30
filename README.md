# NOAA Dataset Project

![Python](https://img.shields.io/badge/Python-3.12+-3776AB?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.7+-F7931E?logo=scikit-learn&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-0.14.x-red?logo=statsmodels&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-3.x-green?logo=xgboost&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

This project develops and evaluates predictive models to forecast significant wave height using time-series data from three NOAA oceanic buoys (46041, 46050, 46243). The core challenge of this dataset is a fundamental conflict between two competing predictive signals: a strong **autoregressive signal** and a weaker **meteorological signal**.

The analysis compares a naive persistence baseline against a statistical model (SARIMAX), and machine learning models (RidgeCV, XGBoost) across four forecast horizons (1, 3, 6, and 12 hours).

The key finding is that for this dataset, the SARIMAX model is provides the best results across all horizons. Its success shows that without extensive feature engineering to capture historical trends and dynamics, even state-of-the-art machine learning models like XGBoost can fail to outperform classical statistical methods that are designed to handle the autocorrelation and seasonality present in such time-series data.

## Findings

The primary outcome of the model comparison is summarized in the performance plots below, showing key error metrics (MAPE, MAE, RMSE) and the coefficient of determination (R²) across the four forecast horizons.

![Model Performance Comparison](assets/results.png)  <!-- Replace with the URL to your comparative plot image -->

- **Short-Term (1-hr Horizon):** All models, including the naive baseline, perform well due to the high autocorrelation of wave height. The most recent observation is the best predictor.

- **Mid-to-Long-Term (3-12-hr Horizons):** As the forecast horizon increases, the performance of the machine learning models and the persistence baseline degrades. The SARIMAX model consistently maintains the lowest error and is the only model to provide meaningful predictive power (positive R²) at the 12-hour horizon.

- **Feature Importance:** The underperformance of XGBoost is due to its effectiveness being highly dependent on feature engineering. With a limited relevant feature set, it was unable to capture the complex temporal dynamics that SARIMAX handles intrinsically.

## Project Setup

This project uses `uv` for package management. `uv` is an extremely fast Python package and project manager, written in Rust that can be used as a drop-in replacement for `pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `twine`, `virtualenv`.

### Prerequisites

- Python >=3.12.11

- `uv`

    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

### Installation Steps

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/shama-llama/noaa-dataset-project.git
    cd noaa-noaa-dataset-project
    ```

2. **Create a Virtual Environment and Install Dependencies with `uv`:**

    ```bash
    uv venv
    uv pip install -e .
    ```

3. **Activate the Virtual Environment:**

    ```bash
    source .venv/bin/activate
    ```

4. **Launch Jupyter Notebook:**

    ```bash
    jupyter notebook
    ```

    Navigate to the `notebooks/` directory to run the analysis.

## References

> [1] National Oceanic and Atmospheric Administration, National Data Buoy Center, U.S. Department of Commerce, “Observation Data Descriptions.” *NOAA NDBC*. Accessed: July 10, 2025. [Online]. Available: [https://www.ndbc.noaa.gov/obsdes.shtml](https://www.ndbc.noaa.gov/obsdes.shtml).

> [2] National Oceanic and Atmospheric Administration, National Data Buoy Center, U.S. Department of Commerce, “NDBC Station List.” *NOAA NDBC*. Accessed: July 10, 2025. [Online]. Available: [https://www.ndbc.noaa.gov/to_station.shtml](https://www.ndbc.noaa.gov/to_station.shtml).

> [3] National Oceanic and Atmospheric Administration, National Centers for Environmental Information, U.S. Department of Commerce, “Storm Events Database.” *NOAA NCDC*. Accessed: July 10, 2025. [Online]. Available: [https://www.ncdc.noaa.gov/stormevents/](https://www.ncdc.noaa.gov/stormevents/).

> [4] The COMET Program, University Corporation for Atmospheric Research. "Wave Types and Characteristics," MetEd. Accessed: July 20, 2025. [Online]. Available: [https://learn.meted.ucar.edu/](https://learn.meted.ucar.edu/).

> [5] J. Perktold, S. Seabold, and J. Taylor, "Statsmodels: Statistical Models and Econometric Tools," Statsmodels.org. Accessed: July 20, 2025. [Online]. Available: [https://www.statsmodels.org/stable/](https://www.statsmodels.org/stable/).

> [6] B. Artley, "Time Series Forecasting with ARIMA, SARIMA, and SARIMAX," Towards Data Science, Apr. 26, 2022. Accessed: 20 July 2025. [Online]. Available: [https://towardsdatascience.com/time-series-forecasting-with-arima-sarima-and-sarimax-ee61099e78f6](https://towardsdatascience.com/time-series-forecasting-with-arima-sarima-and-sarimax-ee61099e78f6).

> [7] W. F. Guthrie, “NIST/SEMATECH e-Handbook of Statistical Methods (NIST Handbook 151).” National Institute of Standards and Technology, 2020. doi: [https://doi.org/10.18434/M32189](https://doi.org/10.18434/M32189). Available: [https://www.itl.nist.gov/div898/handbook/](https://www.itl.nist.gov/div898/handbook/).

> [8] R. J. Hyndman and G. Athanasopoulos, *Forecasting: Principles and Practice*, 3rd ed. Melbourne, Australia: OTexts, 2021. Accessed: Jul. 20, 2025. [Online]. Available: [https://otexts.com/fpp3/](https://otexts.com/fpp3/).

> [9] H. Hu, A. J. Van Der Westhuysen, P. Chu, and A. Fujisaki-Manome, “Predicting Lake Erie wave heights and periods using XGBoost and LSTM,” *Ocean Modelling*, vol. 164, p. 101832, Aug. 2021, doi: [10.1016/j.ocemod.2021.101832](https://doi.org/10.1016/j.ocemod.2021.101832).

## License

This project is licensed under the terms of the [MIT](LICENSE) open source license.
