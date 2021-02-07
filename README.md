# WIDS-2020-Hackathon
WIDS Datathon focused on patient health

Introduction
Databased Hackathons, intending to find a particular solution have always been super exciting to participate in. All three of us are from data science background and always have interests to try any new packages. And we believe hackathons are the best to apply our learnings in the practical world scenarios. The experience may be a bit intimidating but feels great when you can have built a model which can provide predictions on real time data.

Abstract
Data Science when applied to health studies is quite interesting and can turn out to serve for a broader noble cause. Likewise this year’s WIDS Datathon focused on patient health.
Source of the data - The challenge was to create a model that uses data from the first 24 hours of intensive care to predict patient survival. MIT's GOSSIS community initiative, with privacy certification from the Harvard Privacy Lab, has provided a dataset of more than 130,000 hospital Intensive Care Unit (ICU) visits from patients, spanning a one-year timeframe. This data is part of a growing global effort and consortium spanning Argentina, Australia, New Zealand, Sri Lanka, Brazil, and more than 200 hospitals in the United States.(creditshttps://www.widsconference.org/datathon.html)

Method and Instructions
As Data Cleaning is an essential part of all data science projects which is very important more when the data is real time. Likewise we did the same for the WIDS Hackathon activity :-
•	Remove all id columns like icu id, hospital id
•	Missing value imputation by MICE for 7 columns ('age', 'bmi', 'height', 'weight','gender','apache_4a_hospital_death_prob', 'apache_4a_icu_death_prob').

We tried to apply as many ensemble methods we thought would be helpful for predicting the results.
The problem type is Supervised predicting hospital_death. Since the response variable was an integer, we had to convert into a factor variable. We tried to use all the columns as it may help giving us better results.But yes there may be chances of multicollinearity, which we tried to eliminate as much as we could by using the PCA method which identifies which variables gives us better results and which are not important by generating the VIF(variable Importance Factor).We split the data into three pieces: 60% for training, 20% for validation, 20% for final testing.
We tried 3 different methods as mentioned below :-

•	Applying H2O and gbm
Model1
For establishing baseline performance, we built some default models to see what accuracy we can expect. We used the AUC metric for, but you can use h2o.logloss and stopping_metric="logloss" as well. It ranges from 0.5 for random models to 1 for perfect models.The first model is a default GBM, trained on the 60% training split
We got the AUC of 0.897.

Model2
The second model is another default GBM, but trained on 80% of the data (here, we combine the training and validation splits to get more training data), and cross-validated using 4 folds.We used early stopping to automatically tune the number of trees using the validation AUC and a lower learning rate.We also used stochastic sampling of rows and columns to (hopefully) improve generalization. After applying these techniques we achieved a better AUC of 0.9027116.We then carefully tuned the remaining hyper-parameters without “too much” human guess-work. We used both Cartesian and Random hyper-parameter searches to find good models. We got an AUC of 0.90488 though this was not picked up as our final result.
 
•	AutoML
H20 + AutoML
We first ran autoML for 20 base models.We used the similar cleaning process as our previous model.If you need to generate predictions on a test set, you can make predictions directly on the `"H2OAutoML"` object, or on the leader
model object directly.We got an AUC of 0.90436


•	H20 and glm
We recommend letting GLM handle categorical columns, as it can take advantage of the categorical column for better performance and memory utilization. We got an AUC of 0.88574


Results and Discussion
The best result was obtained by using H2O and AutoML, accuracy was the best for gbm model .
The feature age is an important variable based on the VIF value.

Lessons learned
For H2O and gbm,the cross-validation takes longer and is not usually done for really large datasets.
We found the cross-validated performance is similar to the validation set performance(one of the lessons learnt)
For gbm lower learning rate is always better, just takes more trees to converge.

Conclusions
Through the models built, we can predict the fatality rate of the patients. And can prevent the unseen circumstance if we take some precautionary steps ahead of time.

REFERENCES
https://www.h2o.ai/blog/h2o-gbm-tuning-tutorial-for-r/
http://docs.h2o.ai/h2o/latest-stable/index.html
https://www.widsconference.org/datathon.html


 

