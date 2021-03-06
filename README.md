# Risk-based Threshold Regressor
Simplified Binary Threshold Classification 
on Smart Transportation Accidents, 
investigating whether Huber or Cauchy performs better than MSE/MAE
-------

### NOTE: Actual Data could not be released as it is an NDA Licensed dataset


__Specifications__
1. Build model using optimal candidate parameter - tau, in single feature dataset ( y = theta_0 )
2. Minimise cost using M-estimators/Loss functions: Mean Absolute Err., Mean Square Err., Huber Loss, Cauchy Loss
3. Select function with lowest Empirical Risk, intending to minimise both Type I and II errors, and naturally highest prediction score.
4. Remove bad RUC values based on cost derivative       ## To computationally intensive for my machine, but algorithm is implemented.


__Methods__
* Input RUC is focused on a specific slinding window and kappa value, and only negative RUC values are chosen as RUC > 0 & RUC < 0 are two independent event spaces.
* Loss functions hard-coded to help understand its purpose.
* tau_range (for collecting cost & risk across RUC values) and beta_range (hyperparameter for M-estimators) defined w.r.t the size of input sample space, step-size given is an arbitrary value relative to input sample space.
* 4 sample tau_range were created to analyse how model performs, min-Max RUC / min-Max RUC where accidents happened / min RUC to Max ruc where accidents happened / min RUC where accidents happend to Max RUC.

__Results__
* RUC smaller than threshold is classified as accident (1), above threshold is non-accident (0)
* tau param 1 & 2 were presented due to drastic difference in parameter range.
#### Visualised through Confusion Matrix,
In tau_param1, MSE performed the best, with prediction score of 50.36%
Tau Param 1 | True | False
--- | --- | ---
Positive | 5 | 4011
Negative | 4072 | 8

MSE | Threshold
--- | ---
0.003158 | -0.03947

visualised w/ ggplot2
![alt text](https://github.com/WMUStudent21/PAFv1/blob/main/param1-viz.png "MSE Threshold on Data")

In tau_param2, MAE performed the best, with prediction score of 50.42%
Tau Param 2 | True | False
--- | --- | ---
Positive | 5 | 4006
Negative | 4077 | 8

MAE | Threshold
--- | ---
0.0347 | -0.03944

visualised w/ ggplot2
![alt text](https://github.com/WMUStudent21/PAFv1/blob/main/param2-viz.png "MAE Threshold on Data")

__Conclusion__
* Huber and Cauchy did not perform better than MSE/MAE
* Prediction score could not increase without True Positives and False Positives suffering, data collected was too skewed.
* As threshold approaches 0, accuracy will increase.


__Limitations & Improvements__
* Data was not balanced enough between yes/no, which affected training.
1. We can attempt to mend that by learning only on RUC where accidents did happen, or optimising with Gradient Descent would improve results.

