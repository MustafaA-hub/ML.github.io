# Useful Functions

**Calculate MAE**

The lower the MAE, the better

````Python
from sklearn.metrics import mean_absolute_error

def calculate_mae( model_type, X_train, X_valid, y_train, y_valid):
    model = create_model(model_type)
    model.fit(X_train, y_train)
    preds = model.predict(X_valid)
    return mean_absolute_error(y_valid, preds)
````
----
**Missing Value Info**

Information on the dataset (missing values, no. of rows and col)

````Python
def missing_value_info(Dataset):
    # Shape of training data (num_rows, num_columns)
    print(f"Rows: {Dataset.shape[0]}, Columns: {Dataset.shape[1]}")
    
    # Number of missing values in each column of training data
    missing_val_count_by_column = Dataset.isnull().sum()
    total_values = Dataset.shape[0]  # Total number of rows
    
    print("Columns with missing values:")
    for col, count in missing_val_count_by_column[missing_val_count_by_column > 0].items():
        percentage = (count / total_values) * 100
        print(f"  {col}: {count} ({percentage:.2f}%)")
````
