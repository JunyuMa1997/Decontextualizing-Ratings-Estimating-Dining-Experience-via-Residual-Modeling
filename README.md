# Decontextualizing-Ratings-Estimating-Dining-Experience-via-Residual-Modeling
Restaurant ratings are shaped by more than food and servics. Non-experiential factors like location, accessibility, price, and popularity can confound what the score actually reflects. Nonetheless, some diners would like to separate these factors when evaluating a restaurant. This project isolates the "true dining experience" by modeling expected ratings based on contextual attributes and treating the residuals as a proxy for intrinsic quality.

### Repo guide
In the Data_cleaning.ipynb file, we removed restaurants located outside Philadelphia, removed food trucks, converted Google’s price indicators into categorical variables, filled missing values using the median, and grouped restaurant types into broader categories.

In EDA.ipynb, we show some of our preliminary exploratory data analysis. 

In raw_model.ipynb, we regressed rating solely on a restaurant’s location. Using cross-validation, we computed the optimal 
k
k for the KNN method and made a simple estimate.

In improved_model.ipynb, we introduced additional features such as distance to City Hall, distance to the nearest trolley station, and total weekly open hours. We experimented with bootstrap resampling, but it did not perform well in this setting. We also generated polynomial features (up to degree 2) and square root transformations. Using ordinary cross-validation, we compared Ridge, Lasso, and Random Forest models, selecting the one with the lowest MSE. Random Forest yielded the best performance, and we computed the corresponding residuals.

In final_model.ipynb, we addressed the endogeneity of the price feature, recognizing that price may be influenced by the underlying experience. To resolve this, we used instrumental variable regression, predicting price from exogenous variables such as median neighborhood income and restaurant type. We then used these predicted prices as inputs in a new Random Forest model. We plotted feature importances, recomputed the residuals, and sorted restaurants by residual value—highlighting those with the highest and lowest residuals as candidates for qualitative analysis.
