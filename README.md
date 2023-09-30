# ECON615_reg_ovb
import statsmodels.api as sm
import pandas as pd

# Assuming you have a DataFrame 'modeling_df' with covariates and a 'treatment' column

# Step 1: Specify the logistic regression model
X = modeling_df[['covariate1', 'covariate2', 'covariate3']]  # Replace with your covariates
X = sm.add_constant(X)  # Add a constant (intercept) to the model
y = modeling_df['treatment']

# Step 2: Fit the logistic regression model
logit_model = sm.Logit(y, X)
logit_result = logit_model.fit()

# Step 3: Extract propensity scores
propensity_scores = logit_result.predict(X)

# Step 4: Check for common support
treatment_group = propensity_scores[y == 1]
control_group = propensity_scores[y == 0]

# You can check common support using descriptive statistics or visualization
# For example, you can compare histograms or boxplots of propensity scores for both groups
