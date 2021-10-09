# Israel-Excess-Mortality
R code for estimating excess mortality in Israel due to the COVID-19 pandemic.

This repository contains the R-markdown file used to estimate excess mortality in Israel
from the COVID-19 pandemic. 

This repository does NOT provide the data used in the analysis.  Some (but not all) of the 
data are publicly available. Data from 2000-2019 were used to estimate the baseline model
and it was then applied to data from 2020 and 2021 (target period).

The analysis uses daily mortality data, by age group, from the Israel Central Bureau of
Statistics (CBS), population size data from the CBS, daily weather data from the Israel 
Meteorological Service (from the Bet Dagan station) and the weekly ILI index (by age
group) computed by the Israel Center for Disease Control.

Modeling is by quasi-Poisson regression for 6 different age groups.  Annual population data
are smoothed to give daily numbers and these numbers (on a log scale) serve as offsets in
the model for mortality rate, and as a multiplier in predicting mortality for the target
period.  Each model includes a cyclic B-spline to account for annual trends, season-specific 
weather variables (averages of past 10 days with distinct coefficients for each of the four
seasons), the ILI index for the relevant age group and a day-of-week effect (there is lower
mortality on the weekends than during the work week).  Examination of residuals showed good
fits for all groups.

Predictions are computed as the estimated rates times the population size.  Prediction intervals
are computed taking the quasi-Poisson variation as the sole source of variation.  Examination of
the results showed that uncertainty in estimating the rates was almost negligible compared to
the quasi-Poisson variation.  Prediction intervals treat the "to be observed" mortality as
having a Normal distribution with variance taken from the quasi-Poisson model.  
