# Concrete Strength: Abrams' Law vs Machine Learning

**PH1050 – Foundation of Computational Physics**  
**IIT Madras | Group 5 | Problem 6**

## About the Project

Concrete strength depends on several factors, and one of the most important among them is the water-to-cement ratio.

In this project, we explore how the water-to-cement ratio affects the compressive strength of concrete. We start with a traditional empirical relationship known as **Abrams' Law** and then compare its predictions with different machine learning models.

The main aim is to understand how well a simple physics-based model works and whether machine learning can give better predictions using additional concrete mix parameters.

We use both artificially generated data and the UCI Concrete Compressive Strength dataset for our analysis.

## What We Did

The project is divided into three parts.

### 1. Understanding and Testing Abrams' Law

We first studied Abrams' Law, which describes the relationship between the water-to-cement ratio and concrete strength.

\[
S = \frac{A}{B^{w/c}}
\]

We generated synthetic data using known values of A and B, added some random noise and used curve fitting to check whether we could recover the original parameters.

We also:
- Checked how concrete strength changes with the water-to-cement ratio.
- Studied the behaviour of the equation as w/c approaches zero.
- Calculated the w/c ratio required to achieve a strength of 40 MPa.
- Compared the Bisection Method with SciPy's Brent's Method.

### 2. Applying Abrams' Law to Real Concrete Data

Next, we used the UCI Concrete Compressive Strength dataset to see how well Abrams' Law works with actual experimental data.

We focused on concrete samples with a curing age of 28 days.

Our analysis included:
- Fitting Abrams' Law to the real dataset.
- Studying the accuracy of the fitted curve.
- Looking at the residuals and parameter uncertainties.
- Comparing concrete samples with and without fly ash using Welch's t-test.
- Checking whether the observed difference in strength could be explained by the water-to-cement ratio.

### 3. Comparing Machine Learning Models

Finally, we explored whether machine learning models could predict concrete strength more accurately.

We tested the following models:
- Linear Regression
- K-Nearest Neighbours (kNN)
- Decision Tree Regression

We compared their performance using 5-fold cross-validation and RMSE.

We also investigated how these models perform when predicting the strength of concrete at ages beyond 28 days, even though they were trained only on samples with ages up to 28 days.

## Results and Observations

Here are some of the important findings from our project.

### Abrams' Law on Synthetic Data

The fitted values were:

| Parameter | Fitted Value |
|---|---:|
| A | 74.69 ± 0.90 |
| B | 2.483 ± 0.061 |
| R² | 0.75 |

The fitted parameters were very close to the original values used to generate the data.

For a target strength of 40 MPa, both the Bisection Method and Brent's Method gave a water-to-cement ratio of approximately 0.686036.

### Abrams' Law on Real Data

For 425 concrete samples with a curing age of 28 days, we obtained:

| Parameter | Result |
|---|---:|
| A | 75.03 ± 2.63 MPa |
| B | 2.573 ± 0.131 |
| RMSE | 10.57 MPa |
| R² | 0.48 |

The results show that Abrams' Law captures the general trend, but the water-to-cement ratio alone cannot explain all the variations in concrete strength.

### Fly Ash Analysis

We initially observed that samples containing fly ash had lower average compressive strength than samples without fly ash.

However, after accounting for the water-to-cement ratio using the residuals of Abrams' Law, the difference was no longer statistically significant.

This suggests that the initial difference was largely associated with the water-to-cement ratio.

### Machine Learning Comparison

We compared the models using 5-fold cross-validation.

| Model | RMSE (MPa) |
|---|---:|
| Mean Baseline | 16.70 |
| Linear Regression | 7.02 ± 0.43 |
| kNN | 6.37 ± 0.56 |
| Decision Tree | 6.41 ± 0.49 |

Among the tested models, kNN gave the lowest average RMSE.

This shows that using multiple concrete mix parameters can improve prediction accuracy compared to relying only on the water-to-cement ratio.

### Extrapolation

We also tested the models on concrete samples with curing ages greater than 28 days.

An interesting observation was that the kNN and Decision Tree models produced relatively flat predictions beyond the training range.

Linear Regression with logarithmic age, on the other hand, showed a gradually increasing strength trend.

This highlights one of the limitations of machine learning models when they are used outside the range of data on which they were trained.

## Tools and Technologies Used

The entire project was carried out using Python.

- **NumPy:** Numerical calculations and synthetic data generation.
- **Pandas:** Data handling and processing.
- **SciPy:** Curve fitting, root finding and statistical tests.
- **Scikit-learn:** Machine learning models and cross-validation.
- **Matplotlib:** Graphs and data visualisation.
- **ucimlrepo:** Accessing the UCI dataset.

## Dataset

We used the **Concrete Compressive Strength Dataset** from the UCI Machine Learning Repository.

- Number of observations: 1,030
- Target variable: Concrete compressive strength (MPa)
- Dataset ID: 165

Dataset link: https://archive.ics.uci.edu/dataset/165/concrete+compressive+strength

## How to Run the Project

You can run the project using Google Colab or Jupyter Notebook.

First, install the required libraries:

```bash
pip install numpy pandas scipy scikit-learn matplotlib ucimlrepo
```

Then:

1. Clone or download this repository.
2. Open `PH1050_Final_Project.ipynb` in Google Colab or Jupyter Notebook.
3. Run the notebook cells in order.
4. The dataset will be fetched from the UCI repository during execution.

An active internet connection is required to download the dataset.

## Project Files

```text
Concrete-Strength-Abrams-vs-ML/
│
├── README.md
├── PH1050_Final_Project.ipynb
├── Project_Report.pdf
├── Project_Presentation.pptx
├── Concrete_Readme.txt
└── Concrete_Data.xls
```

## Team Members

**Group 5 – PH1050, IIT Madras**

| Name | Contribution |
|---|---|
| P. V. Dharshini | Physics formulation, synthetic data and curve fitting |
| Neeraj Laphriya | Bisection and Brent's methods |
| Srivatsan Gopalakrishnan | Abrams' Law on real data |
| Gagan Devana | Fly ash statistical analysis |
| Siddharth Sivakumar | Machine learning models and cross-validation |
| Sonu Rajank | Extrapolation analysis and conclusions |
| Anoop Malraj | GitHub repository, README and presentation |

## Conclusion

Through this project, we got to explore how a traditional physical relationship and machine learning approaches can be used to study the same engineering problem.

Abrams' Law gave us a simple way to understand the relationship between the water-to-cement ratio and concrete strength. However, it could not account for all the variations present in real-world data.

Machine learning models performed better in terms of prediction accuracy by considering multiple input parameters. At the same time, their performance during extrapolation showed that better prediction within a dataset does not necessarily mean better predictions beyond it.

Overall, the project helped us understand the strengths and limitations of both physics-based modelling and machine learning when applied to a real engineering problem.

## References

1. Abrams, D. A. (1918). *Design of Concrete Mixtures*.
2. Yeh, I-C. (1998). Modeling of strength of high-performance concrete using artificial neural networks.
3. UCI Machine Learning Repository – Concrete Compressive Strength Dataset.
4. SciPy Documentation.
5. Scikit-learn Documentation.

---

*PH1050 – Foundation of Computational Physics | IIT Madras | November 2026*
