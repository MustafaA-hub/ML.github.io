# MISSING VALUES
When wanting to deal with missing values, there are three common approches:

1) **Droppping Columns With Missing Values**: Have to be vary of this option. Unless most values in the dropped columns are missing, the model loses access to a lot of (potentially useful!) information with this approach.
![download](https://github.com/user-attachments/assets/04ef376b-4d8f-47ef-9cb3-51e820d8ac9c)

2) **Imputation**: mputation fills in the missing values with some number. For instance, we can fill in the mean value along each column. Standard approach that yusually works well.
![download](https://github.com/user-attachments/assets/78fc8c1b-5833-4f29-8ef8-3985f497a1ef)

3) **Extension To Imputation**: In this approach, we impute the missing values, as before. And, additionally, for each column with missing entries in the original dataset, we add a new column that shows the location of the imputed entries. This helps keep track of imputed entries.
![download](https://github.com/user-attachments/assets/da3343e5-26e1-48b1-adc7-23fcecc994f6)

Examples below assume that we already have X_train, X_valid, y_train, y_valid. It is useful to first use the missing_value_info function above to know how many columns have missing values.
