# CATEGORICAL VARIABLES
A categorical variable/column takes only a limited number of values. Plugging these variables into most machine learning models in Python without preprocessing them first will result in an error. There are three approaches to dealing with categorical variables. Examples below assume that we already have X_train, X_valid, y_train, y_valid.

1) **Dropping Categorical Variables**: Easiest way to deal with these vaibales is to drop them however this may result in loss of valuable information
````Python
# Categorical Variables: Dropping Categorical Variables
drop_X_train = X_train.select_dtypes(exclude ='object')
drop_X_valid = X_valid.select_dtypes(exclude ='object')
````

2) **Ordinal encoding**: Ordinal encoding assigns a different integer to each unique value in the variable/column. Variables whoses values follow a clear order/ranking are called ordinal variable. Ordinal encoding works well for tree-based models (like decision trees and random forests).
![download](https://github.com/user-attachments/assets/903a03e7-b311-404b-afda-0b04f3f50815)
When conducting ordinal encoding on a variable, we have to make sure the values of X_vaild are a subset of values of the values in X-train. If there are values in X_valid that are not in X_train, there are many approaches to fixing this issue. For instance, you can write a custom ordinal encoder to deal with new categories. The simplest approach, however, is to drop the problematic categorical columns.
````Python
# Categorical Variables: Ordinal Encoding
from sklearn.preprocessing import OrdinalEncoder

# Categorical columns in the training data
object_cols = [col for col in X_train.columns if X_train[col].dtype == "object"]

# Columns that can be safely ordinal encoded
good_label_cols = [col for col in object_cols if 
                   set(X_valid[col]).issubset(set(X_train[col]))]
        
# Problematic columns that will be dropped from the dataset
bad_label_cols = list(set(object_cols)-set(good_label_cols))

# Drop categorical columns that will not be encoded
label_X_train = X_train.drop(bad_label_cols, axis=1)
label_X_valid = X_valid.drop(bad_label_cols, axis=1)

# Apply ordinal encoder 
ordinal_encoder = OrdinalEncoder()
label_X_train[good_label_cols] = ordinal_encoder.fit_transform(X_train[good_label_cols])
label_X_valid[good_label_cols]= ordinal_encoder.transform(X_valid[good_label_cols])
````

3) **One-Hot Encoding**: One-Hot encoding creates a new columns for each value in a variable. This new column is used to indicate the presense (or absense) of the value in that row of the dataset.
![download](https://github.com/user-attachments/assets/0d4e6a3d-6f5a-4d80-b139-a0dc0acb850c)
We refer to the number of unique entries of a categorical variable as the cardinality of that categorical variable. For large datasets with many rows, one-hot encoding can greatly expand the size of the dataset. For this reason, we typically will only one-hot encode columns with relatively low cardinality. Then, high cardinality columns can either be dropped from the dataset, or we can use ordinal encoding.
````Python
# Categorical Variables: One-Hot Encoding
from sklearn.preprocessing import OneHotEncoder

# Categorical columns in the training data
object_cols = [col for col in X_train.columns if X_train[col].dtype == "object"]

# Columns that will be one-hot encoded. Cardinality < 10
low_cardinality_cols = [col for col in object_cols if X_train[col].nunique() < 10]

# Columns that will be dropped from the dataset
high_cardinality_cols = list(set(object_cols)-set(low_cardinality_cols))

# Apply one-hot encoder to each column with categorical data
OH_encoder = OneHotEncoder(handle_unknown = 'ignore', sparse = False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[low_cardinality_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[low_cardinality_cols]))

# One-hot encoding removed index; put it back
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

# Remove categorical columns (will replace with one-hot encoding)
keep_cols_train = X_train.drop(object_cols, axis=1)
keep_cols_valid = X_valid.drop(object_cols, axis=1)

# Add one-hot encoded columns to numerical features
OH_X_train = pd.concat([keep_cols_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([keep_cols_valid, OH_cols_valid], axis=1)

# Ensure all columns have string type
OH_X_train.columns = OH_X_train.columns.astype(str)
OH_X_valid.columns = OH_X_valid.columns.astype(str)
````
