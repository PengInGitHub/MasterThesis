# MasterThesis
## An Empirical Study of The Improved Partially Stacking Blend Model

My Master Thesis:  

1. points out XGBoost, as a single model itself, is actually weak in classifying the data points around the classification boundry (yeas the tough ones), it ranks such data points only randomly. This problem is especially severe in the situation of **imbalanced data**.

2. introduces an improved version of a **custom Ensemble Learning model**. In short, the data points which are hard-to-classify are given to classifiers which are different from XBG. Then blends results of these data points with results of other data points which are predicted by XGB. Thanks to this stacking and blending, the overall predictive power is improved. 

3. investigates and compares the state-of-the-arts credit scoring classifiers and algorithms implemented in online banking industry, where **imbalanced data** is quite a big trouble.

4. conducts an **empirical study** to test this model, especially on how to do model ensemble in a more informative way. When it comes to the datasets, there are **four** up-to-date and large-scale datasets in the field of **online banking credit scoring** used.    

### 1. Define the problem  

In the field of credit scoring, **imbalanced data** frequently occur as the number of
defaulting loans in a portfolio is usually much lower than the number of observations that
do not default. Under the scheme of misclassification costs, the state-of-the-art ensemble
methods used for credit risk assessment, i.e. **Random Forest** and **XGBoost** etc., tend to
misclassify plenty of ‘good’ instances as ‘bad’ when these instances are close to the
decision boundary. 

The figure below visualizes this problem.

![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/rank%20distribution.png)

The dots int the chart are applicants who have applied loans from QianHai, 
a Chinese online lending platform. Those in red indicate that these users are 'bad'because they default.
By contrast the green ones refer to the 'good' users that payback in time. Clearly there is an imbalance problem.  

Further, the x-axis is the prediction result of the best base model, in this case XGB with 2000 times of iterations (XGB_2000).
Moreover the y-axis are the prediction difference between the best base model(XGB_2000) and the XGB_1000. In other words,
y-axis tells how unstable the XGB is, since a change in round of iterations would triger a change of prediciton result of 
the almost same model(all other parameters remain the same).

To note, the left hand side (rank from 0) means these are top trust-worthy users that predicted as paying back in time. 
While the ones rank close to 30,000 are those predicted as bad ones, clearly XGB has done a rather good job in putting
these people in correct positions.  

However, according to the egg-wise shape, one can argue that
XGB is accurate in extreme instances that are close to either 0 or 1 and especially give
robust evaluation on these samples, since the difference (values on Y) is much smaller than
the values of samples locate in the middle of the line. These samples are those nearby the
decision boundary and XGB clearly classifies them randomly. This implies that XGB is
naive to these tough samples.

From the perspective of business, this type of **misclassification** especially has an impact on the Internet banking
industry. This is because the negative impact of mouth of word from the disappointed rejected
users may be substantially enlarged by the Internet.

### 2. Propose an approach

I proposed an improved version of an Ensemble Learning model to make use of the differences of classification rules
of different types of model. By blending their prediction result the overall prediction accuray rate could be increased.  

This idea is illustrated by the chart below.

![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/missclassification.png
)

The y-axis is the difference between the single best model (XGB) and the most different model
from the single best, a liner model. By re-fitting the dots above the line, this ensemlbe model helps to
correct the previously mis-classified 'good' ones.

### 3. Conduct an empirical study

The approach is tested by an empirical research.
#### 1.Data
![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/data.png)
  
#### 2.Several single classifiers are used:
![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/base%20models.png)
  
#### 3.Process Data and Feature Engineering
![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/process%20data.png)
  
#### 4.Train Data
![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/train%20data.png)
  
#### 5.Implement Custom Model
![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/implement%20custom%20model.png)
  
#### 6.Evaluate Performance
![alt text](https://github.com/PengInGitHub/MasterThesis/blob/master/image/test%20performance.png)

### 4. Draw a conclusion
The model has a moderate peformance when the data distribution is consistant. In a situation that users could be exposured to the distribution of ground truth, for example in a Data Mining or Machine Learning contest, this model could be a useful tool. Nonetheless it requires more discreet to implement in industry. 
