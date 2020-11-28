# Linear Regression in Python
*note* --> Since this demo was published `scikit-learn` has been updated. The `train_test_split` function is now imported from `sklearn.model_selection`

## scikit learn model
- in reference to finding housing prices in Boston... 
    y = boston housing price(called 'target' data in Python)
    x = all other features(independent variables)
    1. import linear regression from sci-kit learn module
    2. drop price column as you only want parameters as x values
    3. store linear regression object in a variable called lm... lm = LinearRegression()
    lm.fit() -> fits a linear model
    lm.predict() -> Predict Y using the linear model with estimated coefficients
    lm.score() -> Returns the coefficient of determination (R^2). A measure of how well observed outcomes are replicated by the model, as the proportion of total variation of outcomes explained by the model
    lm.coef_ gives estimated coefficients
    lm.intercept_ gives estimated intercept

## Fitting a Linear Model
- use lm.fit(x,boston.price)
- construct data frame that contains features and estiamted coefficients
    - pd.DataFrame(zip(X.columns, lm.coef_), columns = ['features', 'estimatedCoefficients'])

## More on Regression
- regression finds relationships among variables
    - example: observing employees at some company and try to understand how their salaries depend on their **features**
- in regression analysis: consider some phenomenon of interest and have a number of observations where each observation may have 1+ features
- *find a function that maps some features or variables to others well*


[<-- Back](README.md)