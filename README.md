# U.S. Treasury Zero-Coupon Curve Estimation

This repository implements a full pipeline for estimating the **U.S. Treasury zero-coupon yield curve** using bond price data.  
The project was completed as part of an academic assignment (Feb 2025) and combines **bootstrapping techniques** with **parametric curve-fitting models**.

---

## Objectives
- Develop an automated algorithm to compute **continuously compounded discount rates** for each bond payment date (coupons and principal).  
- Implement and compare different methodologies:
  - **Bootstrapping** (market-implied curve from raw prices).
  - **Nelson–Siegel (NS)** model.
  - **Nelson–Siegel–Svensson (NSS)** model.
  - **Chebyshev polynomial approximation (degree 4)**.  
- Present results in **tables** and **graphs** for analysis and interpretation.

---

## Methodology

### 1. Bootstrapping
- Based on **U.S. Treasury bond dirty prices**.  
- Cashflows expressed in **year fractions** using the *Actual/Actual (ISDA)* convention.  
- Discount factors solved sequentially by maturity, with **log-discount factor interpolation** across 797 coupon dates.  
- Advantage: exact match to market prices.  
- Drawback: sensitive to noise, may break monotonicity.

### 2. Nelson–Siegel (NS)
- Four-parameter model capturing level, slope, and curvature.  
- Simple, interpretable, but less flexible at long maturities.

### 3. Nelson–Siegel–Svensson (NSS)
- Six-parameter extension of NS.  
- Adds a second curvature term to capture humps or twists in the curve.  
- More flexible, but higher risk of overfitting.

### 4. Chebyshev Polynomial (degree 4)
- Purely numerical approximation on rescaled maturity domain.  
- Smooth and stable within the sample range.  
- No financial interpretation, may distort extrapolations.

---

## Results

- **Graph**: Comparison of observed yields, bootstrapped zeros, and the three fitted models.  
- **Tables**:  
  - Estimated coefficients of each model.  
  - Zero rates across maturities (bootstrap vs. NS, NSS, Chebyshev).  

Interpretation:  
- Yield curve shows a modest upward slope, stabilizing near 4.7–4.8% at the long end.  
- A slight dip around 2–5 years is captured by the NSS model.  
- **Recommendation**: Use **NSS** for operational purposes (smooth + flexible), while bootstrap serves as direct market check.
