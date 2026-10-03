# U.S. Mortality Curve Modeling with Numerical Methods

## Overview

This project applies numerical methods to U.S. age-specific mortality data to investigate how mathematical techniques can be used to represent and approximate mortality curves.

The analysis compares **cubic spline interpolation** with a **degree-5 least-squares polynomial approximation**. The models are evaluated using held-out age observations and a cross-year experiment in which mortality data from 2020 is used to approximate mortality rates observed in 2024.

The project was developed to apply concepts from numerical methods in an actuarial context, particularly mortality modeling and risk analysis.

## Dataset

The mortality data comes from the **Human Mortality Database (HMD)** and contains U.S. period mortality rates by age and year.

The analysis uses the HMD U.S. `Mx_1x1` dataset.

- Source: Human Mortality Database
- Country: United States
- Measure: Age-specific period mortality rates
- Years available: 1933–2024
- Ages available: 0–109 and 110+

The raw HMD data file is not included in this repository. Users should obtain the dataset directly from the Human Mortality Database and place the file at:

data/age-specific-death-rates.txt

## Objectives
Explore the shape of U.S. mortality rates across age.
Apply a logarithmic transformation to mortality rates.
Use cubic spline interpolation to represent the mortality curve.
Use least-squares polynomial approximation as an alternative numerical method.
Compare the methods using prediction error.
Evaluate how a mortality curve from 2020 approximates mortality observed in 2024.
Interpret the results in an actuarial context.

## Methodology
1. Data Preparation
The HMD mortality dataset was loaded into Python using Pandas. The analysis focuses primarily on the 2024 mortality curve and excludes the 110+ open-ended age category because it does not represent a single exact age.

2. Technologies
Python
Pandas
NumPy
Matplotlib
SciPy
Jupyter Notebook
Visualizations
2024 Log Mortality Curve

3. Exploratory Analysis
The 2024 mortality rates were examined across age. A logarithmic scale was used to make mortality rates across the full age range easier to visualize because mortality varies substantially between childhood and old age.

4. Log Transformation
Mortality rates were transformed using their natural logarithm. This allows the analysis to examine the shape of mortality more effectively across a wide range of mortality levels.

5. Cubic Spline Interpolation
A cubic spline was fitted to the log mortality rates. Cubic spline interpolation creates a smooth piecewise polynomial curve that passes through the observed data points and can be used to estimate mortality rates at ages between observed observations.

6. Least-Squares Polynomial Approximation
A degree-5 polynomial was fitted to the log mortality rates using least squares. Unlike the interpolating spline, the polynomial does not need to pass through every observation. Instead, it provides a mathematical approximation of the overall relationship between age and log mortality.

7. Numerical Method Comparison
To compare the methods on observations that were not used during fitting, the data was divided using an even/odd age holdout scheme:
Even ages were used for training.
Odd ages were used for testing.
The models were evaluated using:
Root Mean Squared Error (RMSE)
Mean Absolute Error (MAE)

8. Cross-Year Prediction
A second experiment fitted the numerical methods to the 2020 mortality curve and evaluated how well the resulting curves approximated the observed 2024 mortality curve. This experiment demonstrates the difference between approximating the shape of a mortality curve and modeling changes in mortality over time.

9. Results
Even/Odd Age Holdout
The models were fitted using even ages and evaluated using odd ages. The Cubic spline and degree-5 polynomial had a test RMSE of 0.1010 and 0.3126 and a Test MAE of 0.0336 and 0.2418, respectively. For this dataset and evaluation procedure, the cubic spline produced lower prediction error than the degree-5 polynomial. The spline generally tracked the held-out mortality observations more closely, while the polynomial showed larger deviations, particularly at younger ages. 
Cross-Year Approximation: 2020 to 2024
The numerical methods were also fitted using 2020 mortality data and evaluated against 2024 observations.  Cubic spline and degree-5 polynomial had a test RMSE of 0.1990 and 0.3911 and a Test MAE of 0.1826 and 0.2691, respectively.  The cubic spline again produced lower error for this experiment. However, this should be interpreted as cross-year approximation rather than a complete mortality forecasting model. The model uses age as the primary input and does not explicitly model the time trend between 2020 and 2024.

10. Limitations
Single population: The analysis uses mortality data for the United States. Results may differ for other countries or populations.
Single-year mortality curves: Much of the analysis focuses on the 2024 mortality curve. A single-year curve does not represent a long-term mortality projection.
Cross-year approximation: The 2020 → 2024 experiment evaluates how well information from 2020 approximates mortality in 2024. It does not constitute a complete mortality forecasting model.
Interpolation versus forecasting: Cubic spline interpolation is particularly suited to estimating values between observed ages. Applying a spline fitted to one year to another year is a different task.
Polynomial degree: The least-squares comparison uses a degree-5 polynomial. Other polynomial degrees or approximation methods could produce different results.
Infant mortality: Mortality changes rapidly between infancy and early childhood, making the youngest ages more difficult to approximate.
Mortality measure: The dataset contains age-specific mortality rates rather than individual-level probabilities of death. The rates should therefore not be interpreted directly as the probability that an individual will die at a particular age.
Limited model complexity: A practical actuarial mortality projection would generally incorporate additional factors such as calendar-year trends, cohort effects, and potentially separate mortality assumptions for different populations.

## Actuarial Interpretation
Mortality modeling is an important component of actuarial analysis because mortality assumptions can be used to estimate the likelihood and timing of future deaths within a population.
This project demonstrates several numerical techniques that are relevant to actuarial work:
Mortality curves: Age-specific mortality rates provide a way to characterize how mortality changes across a population's lifetime.
Interpolation: Cubic spline interpolation can estimate mortality rates at ages between observed data points while allowing the curve to adapt to local changes in mortality.
Least-squares approximation: Polynomial least-squares approximation provides a single mathematical function that summarizes the overall relationship between age and mortality.
Model comparison: RMSE and MAE were used to compare how closely the numerical methods approximated observations that were not used during fitting.
Mortality trends: Comparing the 2020 and 2024 mortality curves demonstrates that mortality depends not only on age but can also change over time.


