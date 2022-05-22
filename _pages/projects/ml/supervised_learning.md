---
layout : single 
title: Supervised Learning 
permalink: /projects/ml/supervised_learning
tagline: "Learning Curve & Hyperparameter Analysis for 2 datasets using Supervised Learning algorithms"
description: "Learning Curve Analysis for 2 datasets using Supervised Learning algorithms. This project analyses 2 classification problems. The idea is not to find correct hyperparameters for the datasets, rather to do the learning curve analysis for each of the datasets and model them using different algorithms like Artificial Neural Nets, Decision Trees, kNN, Boosting"
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/code.jpg
author: Sabyasachi Ghosal
toc: true
toc_label: "Supervised Algorithms"
sidebar:
  nav: others_nav
---
This project analyses 2 classification problems using different Supervised Learning algorithms. The motive is not to find the correct hyper parameters but to understand how each algorithm behaves on the data and how much effect the hyperparameters have on them.

# Datasets
Dataset1 is a bank marketing database from [Kaggle](https://www.kaggle.com/rouseguy/bankbalanced) where the classification goal is to predict if the bank client will subscribe a term deposit depending on features like age, job-profile, loan, housing etc. Though the original dataset from UCI is an unbalanced one, I am using a balanced sample {deposit: no – 53%, yes – 47% } taken from this Kaggle dataset after some pre-processing. The reason for selecting this dataset is to work with categorical variables and understand how the model can learn itself based on the categories. For example, in this graph, the people who are adults (18 > age < 28), mid age ( 29 > age < 40), towards retirement (41 > age < 60), old ( age > 60) are defined as age categories 1,2,3,4 and if they are interested for making a deposit. It is seen that the mid aged and those toward retirement have less money for investment than young adults or the old. This categorical processing will help the model focus more on the age group rather than the individual age. Similar categorical processing has been done for other features as well. All these features make the modelling nontrivial as well interesting to see how the different models will behave based on their strengths. The dataset contains around 11500 instances and 12 features, so I have good number of instances to play with.

![bank dataset distribution](/assets/images/ml_assets/ml_sl_1.png)

Datset2 is a database of character image features from [UCI](https://archive.ics.uci.edu/ml/datasets/letter+recognition) where the classification goal is to identify the alphabets of a language based on Holland-Style Adaptive Classifiers systems (Letter Recognition Using Holland-Style Adaptive Classifiers, Frey, Slate, 1991). These systems create a list of fixed length condition-action rules that identifies the presence or absence of specific features for each letters of alphabets. Each row in the data set represents an image of a handwritten alphabet. Using some basic image processing, the images are converted into m*n pixels, where m and n depend on the size and resolution of the original image. Each pixel contains numeric values, with higher values denoting the presence of dense 'ink'. Using the pixelated images, 16 features are derived for each image, such as the width of the box, the ratio of the mean variance of x divided by the width of the box, etc. There are 16 attributes like this which is made for around 20000 instances. This data set is interesting because it will help us to understand if our ML models can learn the rules which Holland Style Adaptive Classifier has designed and identify the letters based on this letter recognition algorithm. This is also multiclass classification problem (26 classes) so it will be interesting to see to see how different models perform as this is not trivial. The data is well distributed as seen in the graph. Without adding any synthetic data to put more balance or adding any complex pre-processing technique, I tried to analyse the existing data set. I am training on 80% of the datasets and testing on the rest 20%. 

![alphabet dataset distribution](/assets/images/ml_assets/ml_sl_2.png)

# Decision Trees
## Learning Curve Analysis
For dataset 1, to study the decision trees, I have plotted the learning curve for the bank data with varying depth on 30% cross validated data from the training set with 10 times folding, along with the training set. This is because cross validation will help me to understand how the model with perform on the training data. Here I am trying to study the learning curve of different decision trees with varying depth. In the first figure with maximum depth=1, it is seen that the two graphs have converged so there is no need to add more instances. When the maximum depth = 1 and training size is low (e.g. 10), then the model overfits the data, because the training set generalizes the model too much. But the validation set accuracy is low as the model have not learned properly yet. With the increase of the training sizes (e.g at training size = 2000), the model becomes more robust and generalizes itself becoming a good fit. But when max_depth = 1, the tree will be wide, and the model accuracy is not maximum. With the increase of depth, it is seen that the model accuracy increases. At maximum depth =15, it is seen that the training data fits the data well with increased accuracy, which is good, but the validation accuracy decreases. A good accuracy is noticed for the tree having maximum depth=8, where both the training data and cross validated data have attained good accuracy and the data fits well. If we study the tree at max_depth = 8, we can see that the cross-validation accuracy does not jump to good accuracy immediately like depth=1, but does a smooth gradual transition with the increase of training data and becomes stabilized. At around 5000 instances, the bias-variance trade-off is also less for the same making the model stable.
![bank dataset learning curve](/assets/images/ml_assets/ml_alphabet_data_dt_learning_curve.png)

For the alphabet dataset, I created the learning curves in the similar way. Here it is seen that at depth = 1, the validation error is high, thus it is having high bias and low variance. So, it is not able to generalize with limited amount of data. With the increase of data also the model shows underfitting, where the training accuracy decreases, and the cross-validation accuracy is also very low. With the increase of the depth of the variance increases and the bias decreases. With the tree having maximum depth of 25, the bias-variance attains a balance when the training size = 10000 where we can see that the training score is good, and the cross validation also performed well. If the maximum depth is increased, then no improvement is seen in the scores of the decision tree and little overfitting is seen, which is not clear from the picture. But the accuracy score dropped from 87.8% to 87.4%. 
![alphabet data learning curve](/assets/images/ml_assets/ml_bank_data_dt_learning_curve.png)

## Minimum Sample Split 
For dataset 1, this is one of the most important hyper parameters of the decision tree. I have varied the values of min_samples_split parameter of the sklearn.tree.DecisionTreeClassifier to understand the behaviour of this hyper parameter. By this parameter a split of the decision tree will not happen if there is a smaller number of records specified by the min_samples_split in a node. This value is sent as a percentage of the total number of samples. This helps in pruning the decision tree during the time of creation and can be referred as pre-pruning. It is seen that when the value is 0.0001, though the training accuracy is more, but the validation accuracy is less, which means it is overfitting because the model does not generalize the data well. When the value is 0.1, the node count comes down considerably to 41 making it a pruned tree and the train and test accuracy is also balanced, thus making it a good fit. It is also seen in the graph, that the gap between training and testing lines have reduced considerably. With the increase of the value, there is not much improvement in the model. It is seen that both the training and the test score gets decreased. So, in this way, the decision tree is pruned to a much optimal one which fits the data set well.  
![bank data min sample split](/assets/images/ml_assets/ml_bank_data_hp1_min_sample_split.png)

For dataset 2, it is seen that the train and the validation accuracy come to a balance at 0.007. Similar behaviour is also seen in the graph. The number of nodes is quite high (513) at the best fit compared to the previous dataset. This is because this is a multi-class classifier (26 classes for each of the letters in the English language). So, the tree went long to generalize all the classes.  	
![alphabet data min sample split](/assets/images/ml_assets/ml_alphabet_data_hp1_min_sample_split.png)

## Maximum Depth 
For dataset 1, the maximum depth of a tree is another parameter which also decides the pre-pruning of a decision tree. Here where we can see that when the maximum depth is low, the accuracy of both training and test set is low, making the model underfit. Again, after depth value of 8, the training and testing graphs began to diverge, where the training set generalizes too much thus overfitting, because the training score increases but the validation score also decreases. A perfect balance is observed at depth = 8.
![bank data max depth](/assets/images/ml_assets/ml_bank_data_hp2_max_depth.png)

For dataset 2, in the case of the second data set the model attains a balance at the maximum depth of approx. 28. After that there is no improvement with the change of the variable. This seems very interesting to me; it seems that the model is having some saturation at that depth and it does not seem to improve. So, I tabled the data of the actual node depth with this data. And I can see that though the maximum depth is increased, the actual node depth saturates to 28.
![alphabet data max depth](/assets/images/ml_assets/ml_alphabet_data_hp2_max_depth.png)

I used those above hyper parameters in the DecisionTreeClassifier(). I used the default criteria (gini) as it doesn't require me to compute logarithmic functions, which are computationally intensive. I used the splitter as ‘best’, min_samples_leaf = 1 along with the other default parameters. For data set 1, with max depth = 8 and min_sample_split as 0.1, the confusion matrix shows that the model performance on the test set. The model has performed well where the predicted label has an accuracy of 77% and the training label has an accuracy of 78%.  It has Precision of 0.74 and recall of 0.79 with AUC 0.77.  
![bank data confusion matrix](/assets/images/ml_assets/ml_bank_data_confusion_matrix.png)

In the case of data set 2, the test set has an accuracy of 72% while the training has an accuracy of 75%. I have not mapped the confusion matrix for the second data set because the number of classification label is 26 for 26 characters, due to limited space. 

# Boosting
Boosting is a powerful method for improving the predictive accuracy of classifiers. The AdaBoost algorithm has been successfully applied to many domains and the combination of AdaBoost with the decision tree algorithm has been called the best off-the-shelf learning algorithm in practice. [Reference]. Thus, Decision tree being a low accuracy classifier boosts up to a higher one using boosting. So, I have selected Adaboost along with DecisionTreeClassifier of sklearn as the base estimator for the boosting algorithm. 
## Learning Curve
For dataset 1, while analysing the learning curve, again I have used varying depth to generate many learning curves to understand the bias-variance trade off. For max_depth = 1, the behaviour is almost similar to a normal decision tree. But it gets interesting with the increase of the depth. With just one increase of max_depth to 2 and the training set size = 4000  the accuracy of the cross-validation increases, and the training data also fits well, as it has received a boost. This is much better than the normal decision tree where the stability occurs at max depth of 8. Also, it is noticed that the accuracy level is much better than that of the normal one. When the max depth is more (max_depth = 3), the tree needs more training examples to generalize itself. 
![bank data boosting learning curve](/assets/images/ml_assets/ml_bank_boosting_learning_curve.png)

With the increase of the max_depth to 5, the tree gradually overfits when the training size is low, and with the increase of size (from 5000), it starts to underfit. Thus, it cannot generalize itself after this depth and it is not required to study more.  

For the alphabet dataset, similarly we can see that at depth = 20, the model attains some stability and fits the data well. When the depth = 1, there is an underfitting easily identified where the training score is very low, and the validation score is also very low. With the increase in depth, the model improves its performance gradually overfitting from max_depth =22, where it is seen that the validation accuracy decreases. And it decreases more with more instances at depth = 25. So, there is overfitting because the training accuracy remains good. Compared to the non-boosted decision tree, the model converged on a smaller depth. 
![alphabet data boosting learning curve](/assets/images/ml_assets/ml_alphabet_boosting_learning_curve.png)

## Learning Rate
Slowing down learning is an important for boosting because using weak learners sometimes have lower generalization error by not overfitting early (like simple non boosted decision trees as we have seen before). In case of AdaBoost, the Output (G(x)) and estimator coefficient ( αm ) is defined by,
![lr formula](/assets/images/ml_assets/ml_lr_formula.png)

Decreasing learning rate L, makes αm smaller which reduces the sum of the sample weights at each step. Thus, there are smaller variations of weighted data and fewer differences between weak learner decision boundaries

For the bank dataset, as boosting can afford more pruning, the max_depth has been kept at 3 and with learning rate of 0.15 the cross-validation set achieves an accuracy of more than 80% which is much more than of simple decision tree.  When the learning rate is very low, like 0.01, the accuracy of both training and test set is low thus underfitting. But with gradual increase of learning rate, the model becomes more stable. But when the learning rate is increased more, the model overfits with more bias as the training set improves but the test set deteriorates its performance. Increasing the learning rate, creates large variations of weighted data, which creates strong decision tree boundaries, causing it to overfit. The learning rate of 0.15 is considered high but in the sklearn there is a trade-off between n_estimators and the learning rate. I have created a balance and tested each of the hyper parameters to understand their impact in the boosting process.
![bank_data_hp1_learning_rate](/assets/images/ml_assets/bank_data_hp1_learning_rate.png)

For the second dataset, this scenario is interesting where the model achieves its accuracy at maximum depth of 20 in boosted decision tree. This means that the tree is very complex, this is true because this data set is a multiclass classifier where classification of 26 classes (A to Z) is required. When the learning rate is very low the training and validation scores are low, so there is an underfit. The model achieves a good fit at learning rate of 1.1. After 1.1, the model overfits where the training score stabilises, but the validation score decreases. The converged learning rate value is high compared to normal values of learning rates because I have not optimized the n_estimator and kept it default. There is a trade-off between them. The decision tree overfits when the learning rate becomes more than 1.5.

![alphabet_data_hp1_learning_rate](/assets/images/ml_assets/alphabet_data_hp1_learning_rate.png)

## Actual Result
For dataset 1, the test set is run with maximum depth of 2 with a learning rate of 0.15 and n_estimator value of 50. The model achieves a training accuracy of 82% and test accuracy of 81%. The F1 score is 0.80, AUC is 0.81, Precision is 0.80 and recall 0.80. For the second dataset, the test accuracy is 96% while the training accuracy is 100%. This means that the boosting has really improved the performance of the weak learner with some aggressive pruning on decision tree max depth parameter of the DecisionTreeClassifier.

# kNN 
## Learning Curve Analysis
For dataset 1, to study the k-nearest neighbours, I have plotted the learning curves for the bank data with varying nearest neighbours (k) on 30% cross validated data from the training set with 10 times folding, along with the training set. In the first figure with k=1, it is seen that when the instances are less the test accuracy is low but with the increase of instances, the accuracy improved. Thus, there is a clear overfit. With the increase in the k value the model becomes more stable. A perfect balance is seen when at value k = 29. When k= 89, it is seen that with increase in the number of samples, the validation score decreases, which means the training becomes more biased towards available sample. The training score also decreases from the previous graphs. So, it might not be able to generalize well and it is underfitting the data. From the examples of the learning curve, a perfect balance between bias and variance at k = 29. 
![alphabet_data_hp1_learning_rate](/assets/images/ml_assets/ml_bank_data_knn_lc.png)

The learning curve of data set2 is very interesting. Here it is seen that k=1, the training set attains good accuracy, and the cross-validation set attains around 90% accuracy. With the increase of K value, the training and testing performance deteriorates. The model achieves a good stability at k=1. But we know that at k=1, if the model fits then the behaviour is like a dictionary, and it should overfit. But the validation accuracy does not show that. I also tried to make more folds in cross validations to see any change in behaviour. But it is the same. I raised a Piazza question and based on the suggestions given by the TA s, I tried comparing the different distance metric and both proved that k=1 is the best fit. Normally k=1 means that that it is low bias, and the model will be close to the training data.
![KNN LC Alphabet Data](/assets/images/ml_assets/ml_alphabet_knn_lc.png)

## Nearest Neighbours(k)
For the bank database (dataset 1), I have plotted the accuracy of the cross-validation set (30% of training set, kFold= 10) based on the changing value of k. When the nearest neighbour is 1, we can see there is overfitting in the model as there is high variance and low bias. This is expected behaviour from the design of the knn model. With the increase of the k value the models attain stability. When k = 25, the variance is low, and the model becomes simple. With further increase of k value from 35, the training accuracy starts to decrease thus the model tends to underfit the data. This is because with k→∞, the model becomes simplest, where all data points will belong to the same class. So, this becomes high bias and low variance and thus underfitting.
![Bank Data k](/assets/images/ml_assets/ml_bank_data_k.png)

For the alphabet’s classifier (dataset 2), which is a multi-classifier, a weird behaviour is observed. It is seen that the model attains highest accuracy at k =1. After that the model tends to lose its accuracy with the increase of neighbours. The same behaviour is observed whether the distance metric is Manhattan or Euclidean. The data for training and cross validation testing are not the same and it is shuffled and cross validated 10 folds to obtain this result, which I have plotted in the form of a table. 

Also, the classes are well balanced as explained in the dataset introductions. The only reason for this might be that the boundaries between the classes are very clear.
![Alphabet Data k](/assets/images/ml_assets/ml_alphabet_data_k.png)

## Distance Metric (p)
This is the power parameter for the Minkowski metric. When p=1, this is equivalent to using Manhattan distance, and Euclidean distance for p=2. For arbitrary p, minkowski distance (l_p) is used. In most cases, the choice is always between Manhattan and Euclidean but it’s interesting to see the results of higher minkowski distances. 
In data set1, p=1 or Manhattan distance attains higher accuracy.  Similar behaviour is observed for dataset 2. This is because if the dimensions of the data is more, then Manhattan is supposed to perform better than the Euclidean. Both of my datasets are high dimensional, so the evaluation seems to be correct.

![Distance Metric](/assets/images/ml_assets/ml_ann_distance_metric.png)

## Final Result
For the 1st dataset, Knn performed good and converged to a proper model.  The training score is 76%, while the testing score is 72%. The F1 score is 0.70, AUC is 0.72, Precision = 0.72 and Recall is 0.68 which is greater than 0.5. The confusion matrix is also plotted in the left side.
For the 2nd dataset Knn did not perform well with bigger k values on the cross-validated set. For the testing set with k=1, p=1, the accuracy is 95%. So, I believe in this dataset, the classes are well separated from each other in the space spanned by the explanatory values and behaves like a dictionary thus making 1-NN classification as the most effective one. 

# Artificial Neural Network
There are many libraries to model a neural network. I have tried and tested many of them like the keras and mlpclassifier. I used MLPClassifier based on Multilayer Perceptron to do the experiment because it is easy to configure and tuning of hyperparameters is an easy task. I am using SGD solver (Stochastic Gradient Descent) for the experiments. It is recommended to use ‘adam’ solver for large datasets, but there are more hyperparameters available for tuning when the solver is SGD, and I wanted to understand the impact of them in the model. For running the final tests, I am using ‘adam’ for the dataset1, because I saw an improved performance, while I use ‘sgd’ for the second one.

## Learning Curve Analysis
For dataset 1, using the learning curve, I tried to visualize the effect of the number of observations on the performance metric. For this, I am using an MLP Classifier and doing 10 folds cross validation to generate the comparison of the training and test score. Here I see that when the training set size was very low, there the training accuracy was around 85%, and the validation accuracy is around 72%, which means the model underfits.  This is because the model generalizes based on the training data and as the model does not have enough training data, it is not able to generalize well. With the increase of number of training data, the model can generalize more based on the available data and it achieves some stability. When the training data size is 7000, there is less variance between the training and testing curve and the model fits well with around 80% accuracy. But it is seen that the model learns quite quickly, it can reach 75% of accuracy with a very low amount of training data (approx. 500), unlike the second dataset.

![bank data lc](/assets/images/ml_assets/ml_bank_data_ann_lc.png)

For the alphabet dataset (dataset 2), which is a multiclass classifier, the accuracy is low at start (training size = 100), this is because there are 26 classes in this dataset and the number of features is also more than the first data set. So model is not able to generalize with less amount of data compared to the first dataset (at size = 500, the cross-validation accuracy is around 40%). With the increase of the training data, the model learns more aggressively till the size = 6000, the model jumps to a 80% accuracy. By this time, the model understands all the 14 features of the dataset and can create the classifier model which is able to generalise most of the alphabets. With further increase of the training size, the model fine tunes itself and around 10000 it achieves 90% accuracy for both the training and testing set. 
![alphabet data lc](/assets/images/ml_assets/ml_alphabet_data_ann_lc.png)

## Adaptive Learning Rate  
The amount by which weights are updated during training is the step size or the learning rate. Adaptive learning rate keeps the initial learning rate as constant till the training loss decreases. After that it keeps on decreasing if the training error decreases. So it starts with a larger learning rate and keeps on decreasing if required by the model. It is one of the most important and complex hyperparameters to tune for neural networks which decides how the model is adapted to a problem. Typical values for a neural network with standardized inputs (or inputs mapped to the (0,1) interval) are less than 1 and greater than 10^−6. [Reference]A smaller learning rate may take time for the model to converge while a large learning rate may make the model to converge to a sub-optimal solution (local minimum skipping the actual global minima). For dataset2, I have studied adaptive learning rate with initial learning rate as 0.00001, 0.0001, 0.01, 0.1. The training error is plotted for the model based on the number of iterations. It is seen that when the learning rate is very small the model is no where near to convergence. Similarly, when the learning rate is increased, the convergence of the model also become quick. When the initial learning rate is 0.1, the model achieves convergence in around 100 iterations. But this does not mean that the model is always a good fit at the same adaptive learning. The training error might be reduced, but the model may still overfit. So, for that cross-validation testing is essential.
![Adaptive LR](/assets/images/ml_assets/ml_ann_adaptive_lr.png)

## Regularization Parameter (Alpha)
Alpha is a parameter for regularization term, that combats overfitting by constraining the size of the weights. Increasing alpha may fix high variance (a sign of overfitting) by encouraging smaller weights. Similarly, decreasing alpha may fix high bias (a sign of underfitting) by encouraging larger weights. Here, for the bank dataset, we can see that when the alpha is very small, like 10-6, the training accuracy is 66% and the cross-validation accuracy is 62%. This means that the model overfits because of high variance. With the increase in alpha, the variance decreases. At the alpha value of 0.02, the training and test accuracy achieves a perfect balance with accuracy of around 76%. But with further increase of alpha, the model starts to underfit, and the training accuracy decreases, and the validation accuracy decreases, thus the model underfits the data. 
![Alpha](/assets/images/ml_assets/ml_bank_data_ann_alpha.png)
For the second dataset, similar behaviour is noticed, when the alpha is low, the model overfits with high variance, but with the increase of alpha, the model stabilizes. Around alpha= 0.07, the validation score goes the highest and the model stabilizers. With further increase of alpha, the model starts to underfit with the training and the validation score starts to deteriorate.
![Alpha](/assets/images/ml_assets/ml_alphabet_data_ann_alpha.png)

## Layers and Nodes
The different layers of a neural network can also impact the behaviour of a neural network. Single layer is enough for linearly separable Data. But if the data is not linearly separable, then less of layers may underfit the model.  
For the first dataset, where the data is linearly separable, one layer will be enough for the neural network. But the number of nodes may decide the complexity of the model. When the number of nodes is 5 on a single layer, then the model might not be able to generalize itself. So, it underfits the data. But when the number of nodes is more, then the model is able to generalize itself. When the number of layers is increased, then the model starts to overfit again.
![Layers & Nodes](/assets/images/ml_assets/ml_bank_data_ann_layers_node.png)

For the second dataset, with the increase of layers the model attains stability. When the number of nodes is (5,) the model is not able to fit the data. When the number of nodes is increased to 100, keeping the number of layers as 1, the model still underfits because the data is not linearly separable. The model achieves good fit at 3 layers with 50,100,50 nodes. When the number of layers in increased, the model starts to overfit.
![Layers & Nodes](/assets/images/ml_assets/ml_alphabet_data_ann_layers_node.png)

## Actual Test
For the first dataset, I am using the alpha as 0.02, hidden layer as (100,) logistic as activation function and solver as ‘adam’. I see better performance in ‘adam’ than ‘sgd’ because my dataset size is large. The test set performs with an accuracy of 78.7%, F1 score being 0.77, AUC 0.78, Precision 0.77 and Recall 0.77. 
For the second dataset, the training accuracy is 99.7% whereas the test accuracy is 96.8%. The model is built with alpha as 0.07, solver as ‘sgd’ with initial learning rate as 0.01 with adaptive learning rate and hidden layer as (50,100,50). 
It is seen that the second data set performs much better than the second one while modelling with neural networks.

# Support Vector Machines
## Learning Curve Analysis
A support vector machines (SVM) is known as a pattern classifier with a high generalization ability and one of its advantages is that the generalization ability is theoretically guaranteed. [Reference]But larger values of Penalty parameter C of the error term ( C ) in SVM cause the classifier to attempt to classify more points at the expense of a wider margin (and vice versa for smaller values of C). So, in terms of a bias-variance trade off, larger values of C increase the variance and decrease the bias of the model. This can also be related to the "regular" regularization trade off. SVMs are written as, min regularization(w)+C loss(w;X,y), 
whereas ridge regression / LASSO / etc are formulated like:	 min loss(w;X,y)+λ regularization(w).
Both of them are same with C=1/λ. If λ→∞, the solution is determined entirely by the regularization term, so bias is very high and variance very low; as λ→0, all the regularization bias goes off, but it also loses its variance reduction.

For studying the bank data, I plotted learning curve by varying the C value for a linear kernel. I also captured the training score and testing score after 1000 training samples in the form of a table to show the overfitting. With the increase of the C to 10000, the more overfitting shows up in the learning curve as well as in the table above where the validation score tends to decrease with the increase of training score, so more variance is noticed.
![SVM LC Analysis](/assets/images/ml_assets/ml_bank_svm_lc_analysis.png)

For the alphabet data, similarly at C=10000 an overfitting is noticed where more variance is noticed with the increase of C. Here I plotted the graphs with gamma= 0.01 and kernel type as ‘rbf’. I have studied the used of those parameters in the next section where I study the different hyper parameters. 

![SVM LC Analysis](/assets/images/ml_assets/ml_alphabet_svm_lr_analysis.png)

## Kernel
If the dataset is having the data which is linearly separable, a linear kernel will work fine; otherwise kernels like poly, rbf, sigmoid etc should be used. Among the different kernels, I plotted the linear, poly, rbf and sigmoid. Linear SVM being a parametric model is much faster. On the other hand, in the case of RBF kernel SVM, the complexity grows with the size of the training set In both the data sets which I listed here, I saw that a kernel choice can be made distinctively. If linear and Radial Bias Function (rbf) both performs same, we can choose linear based on Occam’s Razor. 


For dataset 1, there are 2 classes (yes/no) and the linear kernel was able to separate the data distinctively and the linear shows better accuracy than ‘rbf’. 
For dataset 2, when the data is plotted, I can see that rbf kernel performed better than the linear one. The second data set is a multiclass classification problem, so it tends to make more errors when we try to linearly separate it in the form of hyperplanes. In this RBF does a better job.

![SVM Kernel Analysis](/assets/images/ml_assets/ml_svm_kernel.png)

## Gamma
Gamma is one of the most important hyperparamater if the kernel type is not linear. For the kernel type as ‘rbf’ the dataset 2 shows the change in behaviour with the change in gamma. If the gamma is too large the radius of the area of influence of the support vectors only includes the support vector itself and no amount of regularization with C will be able to prevent overfitting. When gamma is very small, the model is too constrained and cannot capture the complexity or “shape” of the data. The region of influence of any selected support vector would include the whole training set. The resulting model will behave similarly to a linear model with a set of hyperplanes that separate the centres of high density of any pair of two classes. For intermediate values, we can see on the gamma=0.01 that good models can be found on a diagonal of C and gamma.

![SVM Gamma](/assets/images/ml_assets/ml_svm_gamma.png)

## Final Result
For the data set 1, I trained the model with a linear kernel and C=1000. The train accuracy was 79% and test accuracy was 78%. The F1 score for the test set was 0.77 and the AUC is 0.78, with precision value as 0.78 and recall 0.75. So, the model looks very stable. For the second data set or the alphabet data set, the model performs well with 91% accuracy. 

# Final Analysis

![Final Analysis](/assets/images/ml_assets/ml_supervised_learning_final_analysis.png)
For my dataset1, if I compare accuracy, I can say that Boosting with Decision Tree is a winner. If I compare based on prediction time, I should say that neural network is a winner. For my second dataset, neural network is a winner. Though the accuracy of kNN is 95% with good running time, I will avoid using the KNN in this dataset because it has done an overfit fit for 1NN. I have Neural Network having a better performance but with little more training time. So, if the training time is a constraint, I will choose Boosting over KNN. 
 My first dataset though shows around 80% accuracy for most of the models, still it is not able to reach 90% accuracy, which my second dataset was able to reach for most of the algorithms.
