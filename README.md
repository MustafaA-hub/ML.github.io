# ML.github.io

# Missing Values: Droppping Columns With Missing Values
# Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns
                     if X_train[col].isnull().any()]

# Drop columns in training and validation data
reduced_X_train = X_train.drop(cols_with_missing, axis=1)
reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)image.png
Examples below assume that we already have X_train, X_valid, y_train, y_valid. It is useful to first use the missing_value_info function above to know how many columns have missing values.
