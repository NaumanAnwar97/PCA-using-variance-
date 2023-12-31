# Principal Component Analysis

#### Seoul Bike Sharing Demand

##### Predict demand for shared bikes in Seoul based on various environmental factors

#### About Dataset
##### Data Description:
The dataset contains weather information (Temperature, Humidity, Windspeed, Visibility, Dewpoint, Solar radiation, Snowfall, Rainfall), the number of bikes rented per hour and date information.
available on: https://www.kaggle.com/datasets/joebeachcapital/seoul-bike-sharing

### Choosing the Right Number of Dimensions
Instead of arbitrarily choosing the number of dimensions to reduce down to, it is
simpler to choose the number of dimensions that add up to a sufficiently large portion
of the variance (e.g., 95%). Unless, of course, you are reducing dimensionality for
data visualization—in that case you will want to reduce the dimensionality down to 2
or 3.
The following code performs PCA without reducing dimensionality, then computes
the minimum number of dimensions required to preserve 95% of the training set’s
variance:

```python
pca = PCA()
pca.fit(X_train)
cumsum = np.cumsum(pca.explained_variance_ratio_)
d = np.argmax(cumsum >= 0.95) + 1
```

You could then set n_components=d and run PCA again. But there is a much better
option: instead of specifying the number of principal components you want to preserve,
you can set n_components to be a float between 0.0 and 1.0, indicating the ratio
of variance you wish to preserve:

```python
pca = PCA(n_components=0.95)
X_reduced = pca.fit_transform(X_train)
```

source: Hands-on Machine Learning with Scikit-Learn, Keras, and TensorFlow