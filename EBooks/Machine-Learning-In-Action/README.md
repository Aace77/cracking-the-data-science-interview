# Machine Learning in Action

This is the source code to go with "Machine Learning in Action"
by Peter Harrington published by Manning Inc.
The official page for this book can be found here: http://manning.com/pharrington/

All the code examples were working on Python 2.6, there shouldn't be any problems with the 2.7.  NumPy will be needed for most examples.  

## Part 1 - Classification

### Chapter 1 - Machine Learning Basics

7 Steps to develop a Machine Learning application:

1. *Collect data*. You could collect the samples by scraping a website and extracting data, or you could get information from an RSS feed or an API. You could have a device collect wind speed measurements and send them to you, or blood glucose levels, or anything you can measure. The number of options is endless. To save some time and effort, you could use publicly available data.

2. *Prepare the input data*. Once you have this data, you need to make sure it's in a useable format. The format in this book is Python list. The benefit of having this standard format is that you can mix and match algorithms and data sources. You may need to do some algorithm-specific formatting here. Some algorithms need features in a special format, some algorithms can deal with target variables and features as strings, and some need them to be integers.

3. *Analyze the input data.* This is looking at the data from the previous task. This could be as simple as looking at the data you’ve parsed in a text editor to make sure steps 1 and 2 are actually working and you don’t have a bunch of empty values. You can also look at the data to see if you can recognize any patterns or if there’s anything obvious, such as a few data points that are vastly different from the rest of the set. Plotting data in one, two, or three dimensions can also help. But most of the time you’ll have more than three features, and you can’t easily plot the data across all features at one time. You could, however, use some advanced methods to distill multiple dimensions down to two or three so you can visualize the data.

4. If you’re working with a production system and you know what the data should look like, or you trust its source, you can skip this step. This step takes human involvement, and for an automated system you don’t want human involvement. The value of this step is that it makes you understand you don’t have garbage coming in.

5. *Train the algorithm.* This is where the machine learning takes place. This step and the next step are where the “core” algorithms lie, depending on the algorithm. You feed the algorithm good clean data from the first two steps and extract knowledge or information. This knowledge you often store in a format that’s readily useable by a machine for the next two steps. In the case of unsupervised learning, there’s no training step because you don’t have a target value. Everything is used in the next step.

6. *Test the algorithm.* This is where the information learned in the previous step is put to use. When you’re evaluating an algorithm, you’ll test it to see how well it does. In the case of supervised learning, you have some known values you can use to evaluate the algorithm. In unsupervised learning, you may have to use some other metrics to evaluate the success. In either case, if you’re not satisfied, you can go back to step 4, change some things, and try testing again. Often the collection or preparation of the data may have been the problem, and you’ll have to go back to step 1.

7. *Use it.* Here you make a real program to do some task, and once again you see if all the previous steps worked as you expected. You might encounter some new data and have to revisit steps 1–5.

### Chapter 2 - Classifying with k-Nearest Neighbors

**Pros:** High accuracy, insensitive to outliers, no assumptions about data.

**Cons:** Computationally expensive, requires a lot of memory.

**Works with:** Numeric values, nominal values.

General Approach to kNN:
1. Collect: Any method.
2. Prepare: Numeric values are needed for a distance calculation. A structured data format is best.
3. Analyze: Any method.
4. Train: Does not apply to the kNN algorithm.
5. Test: Calculate the error rate.
6. Use: This application needs to get some input data and output structured numeric values. Next, the application runs the kNN algorithm on this input data and determines which class the input data should belong to. The application then takes some action on the calculated class.

**Summary**

The k-Nearest Neighbors algorithm is a simple and effective way to classify data. kNN is an example of instance-based learning, where you need to have instances of data close at hand to perform the machine learning algorithm. The algorithm has to carry around the full dataset; for large datasets, this implies a large amount of storage. In addition, you need to calculate the distance measurement for every piece of data in the database, and this can be cumbersome.

An additional drawback is that kNN doesn’t give you any idea of the underlying structure of the data; you have no idea what an “average” or “exemplar” instance from each class looks like.

### Chapter 3 - Splitting datasets one feature at a time: Decision Trees

**Pros:** Computationally cheap to use, easy for humans to understand learned results, missing values OK, can deal with irrelevant features.

**Cons:** Prone to overfitting.

**Works with:** Numeric values, nominal values.

General Approach to Decision Trees:
1. Collect: Any method.
2. Prepare: This tree-building algorithm works only on nominal values, so any continuous values will need to be quantized.
3. Analyze: Any method. You should visually inspect the tree after it is built.
4. Train: Construct a tree data structure.
5. Test: Calculate the error rate with the learned tree.
6. Use: This can be used in any supervised learning task. Often, trees are used to better understand the data.

**Summary**

A decision tree classifier is just like a work-flow diagram with the terminating blocks representing classification decisions. Starting with a dataset, you can measure the inconsistency of a set or the entropy to find a way to split the set until all the data belongs to the same class. The ID3 algorithm can split nominal-valued datasets. Recursion is used in tree-building algorithms to turn a dataset into a decision tree. The tree is easily represented in a Python dictionary rather than a special data structure.

Cleverly applying Matplotlib’s annotations, you can turn our tree data into an easily understood chart. The Python Pickle module can be used for persisting our tree. The contact lens data showed that decision trees can try too hard and overfit a dataset. This overfitting can be removed by pruning the decision tree, combining adjacent leaf nodes that don’t provide a large amount of information gain.

### Chapter 4 - Classifying with probability theory: Naive Bayes

**Pros:** Works with a small amount of data, handles multiple classes.

**Cons:** Sensitive to how the input data is prepared.

**Works with:** Nominal values.

General Approach to naïve Bayes:
1. Collect: Any method.
2. Prepare: Numeric or Boolean values are needed.
3. Analyze: With many features, plotting features isn’t helpful. Looking at histograms is a better idea.
4. Train: Calculate the conditional probabilities of the independent features.
5. Test: Calculate the error rate.
6. Use: One common application of naïve Bayes is document classification. You can use naïve Bayes in any classification setting. It doesn’t have to be text.

**Summary**

Using probabilities can sometimes be more effective than using hard rules for classification. Bayesian probability and Bayes’ rule gives us a way to estimate unknown probabilities from known values.

You can reduce the need for a lot of data by assuming conditional independence among the features in your data. The assumption we make is that the probability of one word doesn’t depend on any other words in the document. We know this assumption is a little simple. That’s why it’s known as naïve Bayes. Despite its incorrect assumptions, naïve Bayes is effective at classification.

There are a number of practical considerations when implementing naïve Bayes in a modern programming language. Underflow is one problem that can be addressed by using the logarithm of probabilities in your calculations. The bag-of-words model is an improvement on the set-of-words model when approaching document classification. There are a number of other improvements, such as removing stop words, and you can spend a long time optimizing a tokenizer.

### Chapter 5 - Logistic Regression

**Pros:** Computationally inexpensive, easy to implement, knowledge representation easy to interpret

**Cons:** Prone to underfitting, may have low accuracy

**Works with:** Numeric values, nominal values

General Approach to Logistic Regression:
1. Collect: Any method.
2. Prepare: Numeric values are needed for a distance calculation. A structured data format is best.
3. Analyze: Any method.
4. Train: We’ll spend most of the time training, where we try to find optimal coefficients to classify our data.
5. Test: Classification is quick and easy once the training step is done.
6. Use: This application needs to get some input data and output structured numeric values. Next, the application applies the simple regression calculation on this input data and determines which class the input data should belong to. The application then takes some action on the calculated class.

**Summary**

Logistic regression is finding best-fit parameters to a nonlinear function called the sigmoid. Methods of optimization can be used to find the best-fit parameters. Among the optimization algorithms, one of the most common algorithms is gradient ascent. Gradient ascent can be simplified with stochastic gradient ascent.

Stochastic gradient ascent can do as well as gradient ascent using far fewer computing resources. In addition, stochastic gradient ascent is an online algorithm; it can update what it has learned as new data comes in rather than reloading all of the data as in batch processing.

### Chapter 6 - Support Vector Machines

**Pros:** Low generalization error, computationally inexpensive, easy to interpret results.

**Cons:** Sensitive to tuning parameters and kernel choice; natively only handles binary classification.

**Works with:** Numeric values, nominal values.

General Approach to SVMs:
1. Collect: Any method.
2. Prepare: Numeric values are needed.
3. Analyze: It helps to visualize the separating hyperplane.
4. Train: The majority of the time will be spent here. Two parameters can be adjusted during this phase.
5. Test: Very simple calculation.
6. Use: You can use an SVM in almost any classification problem. One thing to note is that SVMs are binary classifiers. You’ll need to write a little more code to use an SVM on a problem with more than two classes.

**Summary**

Support vector machines are a type of classifier. They’re called machines because they generate a binary decision; they’re decision machines. Support vectors have good generalization error: they do a good job of learning and generalizing on what they’ve learned. These benefits have made support vector machines popular, and they’re considered by some to be the best stock algorithm in unsupervised learning.

Support vector machines try to maximize margin by solving a quadratic optimization problem. In the past, complex, slow quadratic solvers were used to train support vector machines. John Platt introduced the SMO algorithm, which allowed fast training of SVMs by optimizing only two alphas at one time.

Kernel methods, or the kernel trick, map data (sometimes nonlinear data) from a low-dimensional space to a high-dimensional space. In a higher dimension, you can solve a linear problem that’s nonlinear in lower-dimensional space. Kernel methods can be used in other algorithms than just SVM. The radial-bias function is a popular kernel that measures the distance between two vectors.

Support vector machines are a binary classifier and additional methods can be extended to classification of classes greater than two. The performance of an SVM is also sensitive to optimization parameters and parameters of the kernel used.

### Chapter 7 - Improving classification with the Ada-Boost Meta-Algorithm

**Pros:** Low generalization error, easy to code, works with most classifiers, no parameters to adjust.

**Cons:** Sensitive to outliers.

**Works with:** Numeric values, nominal values.

General Approach to AdaBoost
1. Collect: Any method.
2. Prepare: It depends on which type of weak learner you’re going to use. In this chapter, we’ll use decision stumps, which can take any type of data. You could use any classifier, so any of the classifiers from chapters 2–6 would work. Simple classifiers work better for a weak learner.
3. Analyze: Any method.
4. Train: The majority of the time will be spent here. The classifier will train the weak learner multiple times over the same dataset.
5. Test: Calculate the error rate.
6. Use: Like support vector machines, AdaBoost predicts one of two classes. If you want to use it for classification involving more than two classes, then you’ll need to apply some of the same methods as for support vector machines.

**Summary**

Ensemble methods are a way of combining the predictions of multiple classifiers to get a better answer than simply using one classifier. There are ensemble methods that use different types of classifiers, but we chose to look at methods using only one type of classifier.

Combining multiple classifiers exploits the shortcomings of single classifiers, such as overfitting. Combining multiple classifiers can help, as long as the classifiers are significantly different from each other. This difference can be in the algorithm or in the data applied to that algorithm.

The two types of ensemble methods we discussed are bagging and boosting. In bagging, datasets the same size as the original dataset are built by randomly sampling examples for the dataset with replacement. Boosting takes the idea of bagging a step further by applying a different classifier sequentially to a dataset. An additional ensemble method that has shown to be successful is random forests. Random forests aren’t as popular as AdaBoost, so they aren’t discussed in this book.

We discussed the most popular variant of boosting, called AdaBoost. AdaBoost uses a weak learner as the base classifier with the input data weighted by a weight vector. In the first iteration the data is equally weighted. But in subsequent iterations the data is weighted more strongly if it was incorrectly classified previously. This adapting to the errors is the strength of AdaBoost.

We built functions to create a classifier using AdaBoost and the weak learner, decision stumps. The AdaBoost functions can be applied to any classifier, as long as the classifier can deal with weighted data. The AdaBoost algorithm is powerful, and it quickly handled datasets that were difficult using other classifiers.

The classification imbalance problem is training a classifier with data that doesn’t have an equal number of positive and negative examples. The problem also exists when the costs for misclassification are different from positive and negative examples. We looked at ROC curves as a way to evaluate different classifiers. We introduced precision and recall as metrics to measure the performance classifiers when classification of one class is more important than classification of the other class.

We introduced oversampling and undersampling as ways to adjust the positive and negative examples in a dataset. Another, perhaps better, technique was introduced for dealing with classifiers with unbalanced objectives. This method takes the costs of mis-classification into account when training a classifier.

## Part 2 - Forecasting numeric values with Regression

### Chapter 8 - Predicting numeric values: Regression

**Pros:** Easy to interpret results, computationally inexpensive.

**Cons:** Poorly models nonlinear data.

**Works with:** Numeric values, nominal values.

General Approach to Regression:
1. Collect: Any method.
2. Prepare: We’ll need numeric values for regression. Nominal values should be mapped to binary values.
3. Analyze: It’s helpful to visualized 2D plots. Also, we can visualize the regression weights if we apply shrinkage methods.
4. Train: Find the regression weights.
5. Test: We can measure the R^2, or correlation of the predicted value and data, to measure the success of our models.
5. Use: With regression, we can forecast a numeric value for a number of inputs. This is an improvement over classification because we’re predicting a continuous value rather than a discrete category.

**Summary**

Regression is the process of predicting a target value similar to classification. The difference between regression and classification is that the variable forecasted in regression is continuous, whereas it’s discrete in classification. Regression is one of the most useful tools in statistics. Minimizing the sum-of-squares error is used to find the best weights for the input features in a regression equation. Regression can be done on any set of data provided that for an input matrix X, you can compute the inverse of X^T * X. Just because you can compute a regression equation for a set of data doesn’t mean that the results are very good. One test of how “good” or significant the results are is the correlation between the predicted values yHat and the original data y.

When you have more features than data points, you can’t compute the inverse of X^T * X. If you have more data points than features, you still may not be able to compute X^T * X if the features are highly correlated. Ridge regression is a regression method that allows you to compute regression coefficients despite being unable to compute the inverse of X^T * X.

Ridge regression is an example of a shrinkage method. Shrinkage methods impose a constraint on the size of the regression coefficients. Another shrinkage method that’s powerful is the lasso. The lasso is difficult to compute, but stagewise linear regression is easy to compute and gives results close to those of the lasso.

Shrinkage methods can also be viewed as adding bias to a model and reducing the variance. The bias/variance tradeoff is a powerful concept in understanding how altering a model impacts the success of a model.   

### Chapter 9 - Tree-based Regression

**Pros:** Fits complex, nonlinear data.

**Cons:** Difficult to interpret results.

**Works with:** Numeric values, nominal values.

General Approach to Tree-based Regression:
1. Collect: Any method.
2. Prepare: Numeric values are needed. If you have nominal values, it’s a good idea to map them into binary values.
3. Analyze: We’ll visualize the data in two-dimensional plots and generate trees as dictionaries.
4. Train: The majority of the time will be spent building trees with models at the leaf nodes.
5. Test: We’ll use the R^2 value with test data to determine the quality of our models.
6. Use: We’ll use our trees to make forecasts. We can do almost anything with these results.

**Summary**

Oftentimes your data contains complex interactions that lead to nonlinear relationships between the input data and the target variables. One method to model these complex relationships is to use a tree to break up the predicted value into piecewise constant segments or piecewise linear segments. A tree structure modeling the data with piecewise constant segments is known as a regression tree. When the models are linear regression equations, the tree is known as a model tree.

The CART algorithm builds binary trees and can handle discrete as well as continuous split values. Model trees and regression trees can be built with the CART algorithm as long as you use the right error measurements. When building a tree, there’s a tendency for the tree-building algorithm to build the tree too closely to the data, resulting in an overfit model. An overfit tree is often more complex that it needs to be. To make the tree less complex, a process of pruning is applied to the tree. Two methods of pruning are prepruning, which prunes the tree as it’s being built, and postpruning, which prunes the tree after it’s built. Prepruning is more effective but requires user-defined parameters.

## Part 3 - Unsupervised Learning

### Chapter 10 - Grouping unlabeled items using k-Means Clustering

**Pros:** Easy to implement.

**Cons:** Can converge at local minima; slow on very large datasets.

**Works with:** Numeric values.

General Approach to k-Means Clustering:
1. Collect: Any method.
2. Prepare: Numeric values are needed for a distance calculation, and nominal values can be mapped into binary values for distance calculations.
3. Analyze: Any method.
4. Train: Doesn’t apply to unsupervised learning.
5. Test: Apply the clustering algorithm and inspect the results. Quantitative error measurements such as sum of squared error (introduced later) can be used.
6. Use: Anything you wish. Often, the clusters centers can be treated as representative data of the whole cluster to make decisions.

**Summary**

Clustering is a technique used in unsupervised learning. With unsupervised learning you don’t know what you’re looking for, that is, there are no target variables. Clustering groups data points together, with similar data points in one cluster and dissimilar points in a different group. A number of different measurements can be used to measure similarity.

One widely used clustering algorithm is k-means, where k is a user-specified number of clusters to create. The k-means clustering algorithm starts with k-random cluster centers known as centroids. Next, the algorithm computes the distance from every point to the cluster centers. Each point is assigned to the closest cluster center. The cluster centers are then recalculated based on the new points in the cluster. This process is repeated until the cluster centers no longer move. This simple algorithm is quite effective but is sensitive to the initial cluster placement. To provide better clustering, a second algorithm called bisecting k-means can be used. Bisecting k-means starts with all the points in one cluster and then splits the clusters using k-means with a k of 2. In the next iteration, the cluster with the largest error is chosen to be split. This process is repeated until k clusters have been created. Bisecting k-means creates better clusters than k-means.

### Chapter 11 - Association analysis with the Apriori algorithm

**Pros:** Easy to code up.

**Cons:** May be slow on large datasets.

**Works with:** Numeric values, nominal values.

General Approach to the Apriori algorithm:
1. Collect: Any method.
2. Prepare: Any data type will work as we’re storing sets.
3. Analyze: Any method.
4. Train: Use the Apriori algorithm to find frequent itemsets.
5. Test: Doesn’t apply.
6. Use: This will be used to find frequent itemsets and association rules between items.

**Summary**

Association analysis is a set of tools used to find interesting relationships in a large set of data. There are two ways you can quantify the interesting relationships. The first way is a frequent itemset, which shows items that commonly appear in the data together. The second way of measuring interesting relationships is association rules. Association rules imply an if..then relationship between items.

Finding different combinations of items can be a time-consuming task and prohibitively expensive in terms of computing power. More intelligent approaches are needed to find frequent itemsets in a reasonable amount of time. One such approach is the Apriori algorithm, which uses the Apriori principle to reduce the number of sets that are checked against the database. The Apriori principle states that if an item is infrequent, then supersets containing that item will also be infrequent. The Apriori algorithm starts from single itemsets and creates larger sets by combining sets that meet the minimum support measure. Support is used to measure how often a set appears in the original data.

Once frequent itemsets have been found, you can use the frequent itemsets to generate association rules. The significance of an association rule is measured by confidence. Confidence tells you how many times this rule applies to the frequent itemsets.

Association analysis can be performed on many different items. Some common examples are items in a store and pages visited on a website. Association analysis has also been used to look at the voting history of elected officials and judges.

### Chapter 12 - Efficiently finding frequent itemsets with FP-growth

## Part 4 - Additional Tools

### Chapter 13 - Using Principal Component Analysis to simplify data

### Chapter 14 - Simplifying data with the Singular Value Decomposition

### Chapter 15 - Big Data and MapReduce