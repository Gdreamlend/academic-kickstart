---
title: "Kaggle Iris Flower Dataset"
date: 2019-09-09T15:22:40-04:00
draft: true
---

1. Using decidion tree to categorize the dataset
2. Using k-nearest neighbor algorithm to categorize the dataset
3. Which method performs better

## Decision Tree 

[Reference](https://machinelearningmastery.com/machine-learning-in-python-step-by-step/)
Environment

```conda update scikit-learn```

Dimensions of Dataset(行和列): `print(dataset.shape)`

Peek at the Data(返回前多少行): `print(dataset.head(20))`

Statistical Summary(count, mean, min, max): `print(dataset.describe())`

Class Distribution: `print(dataset.groupby('class').size())`

Data Visualization: 

-- Univariate Plots: 

```
# box and whisker plots
dataset.plot(kind='box', subplots=True, layout=(2,2), sharex=False, sharey=False)
plt.show()
```
```
# histograms
dataset.hist()
plt.show()
```

-- Multivariate Plots
```
# scatter plot matrix
scatter_matrix(dataset)
plt.show()
```
Create a Validation Dataset

split the dataset to training dataset and validation dataset.
```
# Split-out validation dataset
array = dataset.values
X = array[:,0:4]
Y = array[:,4]
validation_size = 0.20
seed = 7
X_train, X_validation, Y_train, Y_validation = model_selection.train_test_split(X, Y, test_size=validation_size, random_state=seed)
```

```
# Load libraries
import pandas
from pandas.plotting import scatter_matrix
import matplotlib.pyplot as plt
from sklearn import model_selection
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.neighbors import KNeighborsClassifier
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
from sklearn.naive_bayes import GaussianNB
from sklearn.svm import SVC

# Load dataset
path = "./iris.csv"
names = ['sepal-length', 'sepal-width', 'petal-length', 'petal-width', 'class']
dataset = pandas.read_csv(path, names=names)

# Split-out validation dataset
array = dataset.values
X = array[1:,0:4]
Y = array[1:,4]
validation_size = 0.20
seed = 7
X_train, X_validation, Y_train, Y_validation = model_selection.train_test_split(X, Y, test_size=validation_size, random_state=seed)

# Test options and evaluation metric
seed = 7
scoring = 'accuracy'

# Spot Check Algorithms
models = []
models.append(('LR', LogisticRegression(solver='liblinear', multi_class='ovr')))
models.append(('LDA', LinearDiscriminantAnalysis()))
models.append(('KNN', KNeighborsClassifier()))
models.append(('CART', DecisionTreeClassifier()))
models.append(('NB', GaussianNB()))
models.append(('SVM', SVC(gamma='auto')))
# evaluate each model in turn
results = []
names = []
for name, model in models:
	kfold = model_selection.KFold(n_splits=10, random_state=seed)
	cv_results = model_selection.cross_val_score(model, X_train, Y_train, cv=kfold, scoring=scoring)
	results.append(cv_results)
	names.append(name)
	msg = "%s: %f (%f)" % (name, cv_results.mean(), cv_results.std())
	print(msg)

```
可视化：
```

```
# Load libraries
import pandas
from pandas.plotting import scatter_matrix
from sklearn import model_selection
from sklearn.model_selection import train_test_split
from sklearn import tree
from sklearn.metrics import accuracy_score
from sklearn.tree import DecisionTreeClassifier
import graphviz
from sklearn.tree import export_graphviz

# Load dataset
path = "./iris.csv"
names = ['sepal-length', 'sepal-width', 'petal-length', 'petal-width', 'class']
dataset = pandas.read_csv(path, names=names)

# Split-out validation dataset
array = dataset.values
X = array[1:,0:4]
Y = array[1:,4]
validation_size = 0.20
seed = 7
X_train, X_validation, Y_train, Y_validation = train_test_split(X, Y, test_size=validation_size, random_state=seed)
# building our decision tree classifier and fitting the model
model = tree.DecisionTreeClassifier()
model.fit(X_train, Y_train)

# predicting on the train and the test data and assessing the accuracies
pred_train = model.predict(X_train)
pred_test = model.predict(X_validation)
train_accuracy = accuracy_score(Y_train, pred_train)
test_accuracy = accuracy_score(Y_validation, pred_test)
print('Training accuracy is: {0}'.format(train_accuracy))
print('Testing accuracy is: {0}'.format(test_accuracy))


# calculating the accuracy again with max_depth = 2

# model2 = tree.DecisionTreeClassifier(max_depth = 2)
# model2.fit(X_train, Y_train)

# pred_train = model2.predict(X_train)
# pred_test = model2.predict(X_validation)
# train_accuracy = accuracy_score(Y_train, pred_train)
# test_accuracy = accuracy_score(Y_validation, pred_test)
# print('Training accuracy with max_depth = 2 is: {0}'.format(train_accuracy))
# print('Testing accuracy with max_depth = 2 is: {0}'.format(test_accuracy))

# visualizing our decision tree
# install graphviz using `pip install graphviz` or
# 'conda install graphviz' or `brew install graphviz`
feature_names=['sepal length (cm)', 'sepal width (cm)', 'petal length (cm)', 'petal width (cm)']
dotfile = open("dtree2.dot", 'w')
tree.export_graphviz(model, out_file = dotfile, feature_names = feature_names)
dotfile.close()
#dot_data = export_graphviz(model)
#graphviz.Source(export_graphviz(model,
#                                out_file=None,
#                                feature_names=sorted(feature_names),
#                                class_names=["setosa", "versicolor", "virginica"],
#                                impurity=False))

# dot_data = StringIO()
# export_graphviz(dtree, out_file=dot_data,  
#                filled=True, rounded=True,
#                special_characters=True)
# graph = pydotplus.graph_from_dot_data(dot_data.getvalue())  
# Image(graph.create_png())
```
dot -Tpng input.dot > output.png
```

plot the decision surface of a decision tree using paired features.[Reference](https://scikit-learn.org/0.18/auto_examples/tree/plot_iris.html)

```
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
# Parameters
n_classes = 3
plot_colors = "bry"
plot_step = 0.02
# Load data
iris = load_iris()
for pairidx, pair in enumerate([[0, 1], [0, 2], [0, 3],[1, 2], [1, 3], [2, 3]]):
    # We only take the two corresponding features
    X = iris.data[:, pair]
    y = iris.target
    # Train
    clf = DecisionTreeClassifier().fit(X, y)
    # Plot the decision boundary
    plt.subplot(2, 3, pairidx + 1)
    x_min, x_max = X[:, 0].min() - 1, X[:, 0].max() + 1
    y_min, y_max = X[:, 1].min() - 1, X[:, 1].max() + 1
    xx, yy = np.meshgrid(np.arange(x_min, x_max, plot_step),
                         np.arange(y_min, y_max, plot_step))
    Z = clf.predict(np.c_[xx.ravel(), yy.ravel()])
    Z = Z.reshape(xx.shape)
    cs = plt.contourf(xx, yy, Z, cmap=plt.cm.Paired)
    plt.xlabel(iris.feature_names[pair[0]])
    plt.ylabel(iris.feature_names[pair[1]])
    plt.axis("tight")
    # Plot the training points
    for i, color in zip(range(n_classes), plot_colors):
        idx = np.where(y == i)
        plt.scatter(X[idx, 0], X[idx, 1], c=color, label=iris.target_names[i],
                    cmap=plt.cm.Paired)

    plt.axis("tight")
plt.suptitle("Decision surface of a decision tree using paired features")
plt.legend()
plt.show()

```

