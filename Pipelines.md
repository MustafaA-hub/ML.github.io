# PIPELINES
A pipeline bundles preprocessing and modeling steps into one single step.

1) **Preprocessing**: Preprocessing it self might have a lot of steps and so it is a good idea to bundle those steps too using 'ColumnTransformer' class. For example when preprocessing, numerical data (e.g. imputing) is processed differently from categorical data (e.g. imputing + one-hot coding).

2) **Create a Model**: Model can be any type (e.g. Desicion Tree, Random Forest Regressor)

3) **Create Pipeline**: We use the 'Pipeline' class to define a pipeline that bundles the preprocessing and modeling steps. After creating the pipline when we run the .fit() command on it, it will preprocess and model the training data. Next when we run the .predict() command on this pipleine, it will automatically preprocess the validation data.

Examples below assume that we already have X_train, X_valid, y_train, y_valid.
````Python
# Pipeline Code

from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder
from sklearn.ensemble import RandomForestRegressor

# Preprocessing for numerical data
numerical_transformer = SimpleImputer(strategy='constant')

# Preprocessing for categorical data (2 actions bundled together)
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

# Bundle preprocessing for numerical and categorical data
preprocessor = ColumnTransformer(
    transformers=[
        ('num', numerical_transformer, numerical_cols),
        ('cat', categorical_transformer, categorical_cols)
    ])

# Create a model
model = RandomForestRegressor(n_estimators=100, random_state=0)


# Bundle preprocessing and modeling code in a pipeline
my_pipeline = Pipeline(steps=[('preprocessor', preprocessor),
                              ('model', model)
                             ])

# Preprocessing of training data, fit model 
my_pipeline.fit(X_train, y_train)

# Preprocessing of validation data, get predictions
preds = my_pipeline.predict(X_valid)
````
