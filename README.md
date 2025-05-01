# Predicting Hubble Residuals Using Host Galaxy Properties

**Author**: Mykola Chernyashevskyy  
**Affiliation**: University of Pittsburgh, Department of Physics and Astronomy  
**Email**: myc21@pitt.edu

---

## 🔭 Introduction

Type Ia supernovae (SNe Ia) are crucial cosmological tools used to measure the universe’s expansion. However, after standardization, some residual scatter remains in their luminosity—called **Hubble residuals**.

Studies (e.g., Scolnic et al. 2018) show a "mass step": SNe Ia in more massive galaxies appear systematically brighter. This implies that **host galaxy properties** may predict or explain residual scatter.

This project uses **machine learning** (kNN, XGBoost, Random Forest) to investigate correlations between eight host galaxy properties and Hubble residuals.

---

## 🗂️ Data

- **Supernovae**: Dark Energy Survey (DES) using DECam on the Blanco 4m telescope (CTIO).
- **Host Galaxies**: Dark Energy Spectroscopic Instrument (DESI) DR1 via Mayall 4m telescope (KPNO).
- **Matching Criteria**:  
  - Within 5 half-light radii  
  - Redshift difference < 0.05  
- **Final Sample**: 67 matched SN–host galaxy pairs  
- **Cosmology**: Flat ΛCDM, H₀ = 70 km/s/Mpc, Ωₘ = 0.315

![Mollweide Projection](mollweide.png)

---

## 🧪 Methods

### 📈 Spearman Correlation
Spearman’s rank correlation coefficient (ρ) measures the monotonic relationship between two sets of data. It’s robust to outliers and captures non-linear trends.

### 🤖 Machine Learning Models

- **kNN**: Predicts using the average values from k nearest neighbors.
- **Random Forest**: An ensemble of decision trees trained on bootstrapped data.
- **XGBoost**: Gradient boosting that sequentially builds trees to minimize loss.

### 🔁 k-Fold Cross Validation
k-Fold Cross-Validation evaluates a model's performance by splitting data into k subsets, training on k-1 subsets, and testing on the remaining subset.

---

## 📊 Results

**Top Correlated Features (Spearman ρ):**

| Feature     | ρ       | p-value  |
|-------------|---------|----------|
| DN4000      | -0.2317 | 0.0592   |
| SFR         | +0.2029 | 0.0997   |
| COLOR G–R   | -0.2804 | 0.0215   |

**Used Features for ML**: DN4000, SFR, COLOR G–R

**Performance Summary**:

| Model         | NMAD     | Outlier Rate |
|---------------|----------|--------------|
| kNN           | 0.1012   | 2.99%        |
| Random Forest | 0.1187   | 4.48%        |
| XGBoost       | 0.1043   | 4.48%        |

Outlier cutoff = ±0.3 mag (Scolnic et al. 2018)

![Residuals vs Features](lowess_DN4000.png) ![Residuals vs Features](lowess_SFR_V2.png) ![Residuals vs Features](lowess_g-r.png)

![Model Predictions](kNN.png) ![Model Predictions](Random_f.png) ![Model Predictions](XGBOOST.png)

---

## 🧠 Conclusion

- **Low outlier rates** suggest promising predictive power.
- **Random Forest** showed no improvement over raw residuals.
- **Estimated contribution of host properties** to residuals:  
  sigma_galaxy ≈ 0.06 mag
- Host galaxy features like DN4000, SFR, and COLOR G–R account for a modest (~0.06 mag) variation in Hubble residuals.

---

## 📚 References

- Scolnic et al. (2018)
- Lunnan et al. (2016)
- Gupta et al. (2018)
- Sanchez et al. (2024)
- DESI Collaboration (DR1)
- Laerd Statistics (Spearman explanation)
- Medium (kNN article, 2020)
- Koehrsen (Random Forest, 2018)
- Sonawane (XGBoost, 2019)
- Brownlee (k-Fold CV, 2018)
