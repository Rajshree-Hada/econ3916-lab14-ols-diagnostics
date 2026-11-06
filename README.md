# econ3916-lab14-ols-diagnostics

# OLS Diagnostics: When the Standard Error Is Lying

## Objective
I tested when classical OLS standard errors can be trusted, and what robust standard errors and residual diagnostics do and do not fix.

## Methodology
- Simulated errors whose spread grows with x, and fitted one regression with classical and HC3 standard errors.
- Ran 400 simulated samples and checked how often each 95% interval covered the true slope, with Monte Carlo standard errors.
- Read four residual plots (well behaved, heteroskedastic, missing curvature, an outlier) beside Breusch-Pagan and Jarque-Bera tests.
- Deleted one influential row out of 600 and compared the slope and its standard error with and without it.
- Fitted a California Housing regression and compared classical and HC3 standard errors.
- Wrote a function, `hc3_se()`, and used it to compare the HC3 standard error on AveRooms with and without the 965 districts at the 5.0 ceiling.
- Built a regression with an omitted confounder that passes every diagnostic.

## Key Findings
- Both methods gave the same slope, 2.0147. The standard errors were 0.0264 (classical) and 0.0290 (HC3).
- Over 400 samples, the classical interval covered the true slope in 91.8% of them (Monte Carlo SE 1.4%) and the robust one in 93.5% (Monte Carlo SE 1.2%). The classical shortfall was well beyond chance, while the robust one was not clearly so.
- Deleting one row out of 600 moved the slope by 0.58 of its own standard error, while the standard error fell 33%. A low-leverage outlier hurt the precision far more than the estimate.
- In California Housing, the HC3 standard error on AveRooms was 5.02 times the classical one.
- The HC3 standard error on AveRooms was 0.0121 with all districts and 0.0082 without the 965 at the ceiling. A smaller standard error is not a reason to drop them. Their true values are unrecorded, and robust standard errors do not fix that censoring.
- A regression of y on x alone, with a confounder left out, passed every diagnostic (Breusch-Pagan p = 0.4856, Jarque-Bera p = 0.0692, max Cook's D = 0.0541). It still gave a slope of 3.604 against a true value of 2.0. Diagnostics test the model's internal assumptions, not whether the model is right about cause.
