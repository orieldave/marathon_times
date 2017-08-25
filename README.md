# Marathon race time predictor

Exploratory analysis on predicting a runner's marathon race time given incomplete times from shorter races. Inspired by [this FiveThirtyEight article](https://fivethirtyeight.com/features/tell-us-two-things-and-well-tell-you-how-fast-youd-run-a-marathon/) and using the data provided by the corresponding [paper](https://bmcsportsscimedrehabil.biomedcentral.com/articles/10.1186/s13102-016-0052-y) I wanted to see how a quick machine learning based approach would fare.

## Data
The data contains time, distance, difficulty and fitness data for a number of races for 2303 individuals. The race data is incomplete in the sense that person A may have run a 5km, 10mi and a full marathon, whereas person B may only have run a half marathon and a full marathon. There is also data on training (eg. number of miles run per week), on the individuals (eg. age, male/female) and on other relevant factors (eg. experience, footwear). The data also contains predicted marathon times for two existing models.

## Analysis
The two existing models have Mean Absolute Error (MAE) on all the data of 11.37 minutes (using one previous race time) and 10.29 minutes (using two prior race times). Using only the mean of any prior race times and all other features (age, fitness, injury, ...) a simple ridge regression model has MAE (on test data) of 10.67 minutes.

Some notes:
* linear, 2nd and 3rd order polynomials are fairly similar, poly2 slight improvement over linear
* ridge regression has lowest MAE, but similar to lasso / decision tree / random forest
* tree models tended to overfit on train and underperform on test (the dataset is small)
* no noticeable improvement in increasing/decreasing number of features from 50

## Conclusions
* I suspect this is close to what can be achieved without race-specific data (starting pace, day-to-day variance, ...)
* the two types of error (slower than expected / "bonking" and faster than expected) are probably difficult to predict based mainly on times of shorter races

## Next steps
* not enough data for more complex models (random forests overfitting)
* consider more expert feature engineering (eg higher power combinations of mean_pace, dist, etc)?
* consider ways to use multiple race data beyond the mean?
* create model learn/inference script once features are finalised
* create flask webapp
* write up
