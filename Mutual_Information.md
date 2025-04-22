# Mutual Information
The mutual information (MI) between two quantities is a measure of the extent to which knowledge of one quantity reduces uncertainty about the other. If you knew the value of a feature, how much more confident would you be about the target?

MI can help you to understand the relative potential of a feature as a predictor of the target, considered by itself.
It's possible for a feature to be very informative when interacting with other features, but not so informative all alone. MI can't detect interactions between features. It is a univariate metric.

The actual usefulness of a feature depends on the model you use it with. A feature is only useful to the extent that its relationship with the target is one your model can learn. Just because a feature has a high MI score doesn't mean your model will be able to do anything with that information. You may need to transform the feature first to expose the association.

The scikit-learn algorithm for MI treats discrete features differently from continuous features. Consequently, you need to tell it which are which. Float dtype = continous, Int dtype = discrete. Categoricals (object or categorial dtype) can be treated as discrete by giving them a label encoding.

````Python
# MI Utility functions
from sklearn.feature_selection import mutual_info_regression
import matplotlib.pyplot as plt

def make_mi_scores(X, y):
    X = X.copy()
    X = X.fillna(0) 
    for colname in X.select_dtypes(["object", "category"]):
        X[colname], _ = X[colname].factorize()
    mi_scores  = []
    for col in X.columns:
        try:
            score = mutual_info_regression(X[[col]], y, discrete_features=[pd.api.types.is_integer_dtype(X[col].dtype)])
            print(f"{col}: {score[[0]]}")
            mi_scores.append(score[0])
        except Exception as e:
            print(f"❌ Error on column '{col}':", e)
    # All discrete features should now have integer dtypes
    #discrete_features = [pd.api.types.is_integer_dtype(t) for t in X.dtypes]
    #mi_scores = mutual_info_regression(X, y, discrete_features=discrete_features, random_state=0)
    mi_scores = pd.Series(mi_scores, name="MI Scores", index=X.columns)
    mi_scores = mi_scores.sort_values(ascending=False)
    return mi_scores


def plot_mi_scores(scores):
    scores = scores.sort_values(ascending=True)
    width = np.arange(len(scores))
    ticks = list(scores.index)
    plt.barh(width, scores)
    plt.yticks(width, ticks)
    plt.title("Mutual Information Scores")

scores = make_mi_scores(X, y)
plot_mi_scores(scores)
````
