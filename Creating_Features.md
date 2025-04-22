# Creating Features
It's good to keep in mind your model's own strengths and weaknesses when creating features.

Here are some guidelines:Linear models learn sums and differences naturally, but can't learn anything more complex.
Ratios seem to be difficult for most models to learn. Ratio combinations often lead to some easy performance gains.
Linear models and neural nets generally do better with normalized features. Neural nets especially need features scaled to values not too far from 0. Tree-based models (like random forests and XGBoost) can sometimes benefit from normalization, but usually much less so.
Tree models can learn to approximate almost any combination of features, but when a combination is especially important they can still benefit from having it explicitly created, especially when data is limited.
Counts are especially helpful for tree models, since these models don't have a natural way of aggregating information across many features at once.

````Python
df["new_feature"] = df.feature_1/df.feature_2

# If the feature has 0.0 values, use np.log1p (log(1+x)) instead of np.log
df["new_feature"] = df.feature_1.apply(np.log1p)

# counting True/False features
feature_group = ["feature_1", "feature_2", "feature_3", "feature_4"]
df["new_feature"] = df[feature_group].sum(axis=1)

# counting numerical features greater than 0
feature_group = ["feature_1", "feature_2", "feature_3", "feature_4"]
df["new_feature"] = df[feature_group].gt(0).sum(axis=1)

# Create two new features from an existing feature by splitting on " " and expanding the result into separate columns
df[["new_feature_1", "new_feature_2"]] = (df["feature"].str.split(" ", expand=True))

# joining two features
df["new_feature"] = df["feature_1"] + "_" + df["feature_2"]

# Group transform helps to aggregate infromation of on feature and categorize it according to the second feature
# for example if you have income and state and you want the sum/average of the the total income per state
df["AverageIncome"] = (df.groupby("State")["Income"].transform("mean"))
# other functions include max, min, median, var, std, and count
````
