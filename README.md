# Modeling Sports Attendance in Argentina with Bayesian Hierarchical Models

## Project overview
This project models stadium attendance for football matches in Argentina using Bayesian methods. The goal is to understand how attendance varies by team and by day of the week and to build a model that can predict attendance for future games, even when some scanner data is missing.

The analysis compares simpler models with a Bayesian hierarchical Negative Binomial model that can capture both team-specific behavior and overdispersed count data.

## Data
The dataset contains ticket scanner counts for multiple teams across the days of the week.  
Each row represents one game with columns such as:

- team  
- day of week  
- scanned attendance  

Some games have missing scanner data that we handle through the model.

## Methods

### Exploratory analysis
- Visualized attendance distributions overall and by team and weekday  
- Checked for overdispersion and skew in the counts  
- Looked at patterns in missing data

### Models
All models were implemented in PyMC.

1. **Complete pooling model**  
   - One global mean attendance  
   - Negative Binomial likelihood for overdispersed counts  

2. **Hierarchical model with team and day effects**  
   - Negative Binomial likelihood  
   - Varying intercepts for each team  
   - Day-of-week effects  
   - Shared hyperpriors to partially pool team-level parameters

### Model comparison and diagnostics
- Used posterior predictive checks to see how well each model reproduces the observed distribution of attendance  
- Used PSIS-LOO (Leave One Out) to compare out of sample predictive performance  
- Checked trace plots and effective sample sizes to ensure good MCMC convergence

The hierarchical Negative Binomial model provided better predictive performance and more realistic uncertainty than the simpler alternatives.

## Imputing missing games
Some games were missing scanner data because of technical failures.  
Using the fitted hierarchical model, I generated posterior predictive distributions for these missing games and summarized them with means and credible intervals by team and day.

## Results
Key findings:

- Attendance varies strongly across teams and days of the week  
- A hierarchical Negative Binomial model captures both team-level differences and within-team variability  
- The hierarchical model outperforms simpler models on PSIS-LOO and produces sensible predictions for games with missing data  

## Files
- `sports_attendance_model.ipynb`  
  Full PyMC implementation, exploratory plots, model fitting, diagnostics, and posterior predictive checks.  

- `sports_attendance_report.pdf`  
  Assignment report that explains the modeling choices, diagnostics, and conclusions in more detail.  

- `sports-attendance-data.csv`  
  Raw attendance data used in the analysis.

