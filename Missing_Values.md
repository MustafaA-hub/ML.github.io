# MISSING VALUES
When wanting to deal with missing values, there are three common approches:

1) **Droppping Columns With Missing Values**: Have to be vary of this option. Unless most values in the dropped columns are missing, the model loses access to a lot of (potentially useful!) information with this approach.
![download](https://github.com/user-attachments/assets/04ef376b-4d8f-47ef-9cb3-51e820d8ac9c)
````Python
# Missing Values: Droppping Columns With Missing Values
# Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns
                     if X_train[col].isnull().any()]

# Drop columns in training and validation data
reduced_X_train = X_train.drop(cols_with_missing, axis=1)
reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)
````

2) **Imputation**: Imputation fills in the missing values with some number. For instance, we can fill in the mean value along each column. Standard approach that yusually works well.
![download](https://github.com/user-attachments/assets/78fc8c1b-5833-4f29-8ef8-3985f497a1ef)
````Python
# Missing Values: Imputation
from sklearn.impute import SimpleImputer

my_imputer = SimpleImputer()
imputed_X_train = pd.DataFrame(my_imputer.fit_transform(X_train))
imputed_X_valid = pd.DataFrame(my_imputer.transform(X_valid))

# Imputation removed column names; put them back
imputed_X_train.columns = X_train.columns
imputed_X_valid.columns = X_valid.columns
````

3) **Extension To Imputation**: In this approach, we impute the missing values, as before. And, additionally, for each column with missing entries in the original dataset, we add a new column that shows the location of the imputed entries. This helps keep track of imputed entries.
![download](https://github.com/user-attachments/assets/da3343e5-26e1-48b1-adc7-23fcecc994f6)
````Python
# Missing Values: Extenstion To Imputation
from sklearn.impute import SimpleImputer
# Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns
                     if X_train[col].isnull().any()]

# Make copy to avoid changing original data (when imputing)
X_train_plus = X_train.copy()
X_valid_plus = X_valid.copy()

# Make new columns indicating what will be imputed
for col in cols_with_missing:
    X_train_plus[col + '_was_missing'] = X_train_plus[col].isnull()
    X_valid_plus[col + '_was_missing'] = X_valid_plus[col].isnull()

# Imputation
my_imputer = SimpleImputer()
imputed_X_train_plus = pd.DataFrame(my_imputer.fit_transform(X_train_plus))
imputed_X_valid_plus = pd.DataFrame(my_imputer.transform(X_valid_plus))

# Imputation removed column names; put them back
imputed_X_train_plus.columns = X_train_plus.columns
imputed_X_valid_plus.columns = X_valid_plus.columns
````

Examples below assume that we already have X_train, X_valid, y_train, y_valid. It is useful to first use the missing_value_info function above to know how many columns have missing values.
