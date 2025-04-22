# CROSS VALIDATION
When Validating data, we normally use the last 20% of a our training model as validation. But that does not give a reliable estimate of how accurate our model is because, there are only few possibilites that are being covered in the validation data and the model might perform differntly if we select the a different section of the training data for validation. This is where cross validation comes in, where we run our modeling process on different subsets of the data to get multiple measures of model quality.

For example, we could begin by dividing the data into 5 pieces aka 5 "folds". In each expriment we treat the highlighted fold as avalidation data and train the model on the remaining data. This process is repeated 5 times.

![download](https://github.com/user-attachments/assets/69ce0b48-0d70-4816-8427-8610969e855a)

Cross validation gives a more accurate depection of the model but can take longer to run especially on large datasets. As a general rule of thumb, if your model takes a couple minutes or less to run, it's probably worth switching to cross-validation. Alternatively, you can run cross-validation and see if the scores for each experiment seem close. If each experiment yields the same results, a single validation set is probably sufficient. Added benfit of Cross-Validation is that we don't have to keep track of training and validation data seperatley.

It is best to use pipline when doing cross-validation. Example below assumes we have X and y

````Python
# Cross Validation Code
from sklearn.ensemble import RandomForestRegressor
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.model_selection import cross_val_score

my_pipeline = Pipeline(steps=[('preprocessor', SimpleImputer()),
                              ('model', RandomForestRegressor(n_estimators=50,
                                                              random_state=0))
                             ])

# Multiply by -1 since sklearn calculates *negative* MAE
# cv = number of folds
scores = -1 * cross_val_score(my_pipeline, X, y,
                              cv=5,
                              scoring='neg_mean_absolute_error'

print("Average MAE score (across experiments):")
print(scores.mean())
````
