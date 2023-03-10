# Credit_Risk_Analyis

# Overview of the analysis:
The purpose of this analysis is to apply machine learning models in
a set of credit card credit data from LendingClub, a peer-to-peer lending services company, to see if any of them could be used to predict whether credit risk is low risk or high risk.

In the following, we will analyze each of the approaches used.

# Results:
The first step we took after loading the data, dropping null variables and columns, and converting the necessary data, was to check the balance of our target variable 'loan_status'. In the output below we can see that the high risk records "0" (347) do not have a sufficiently balanced amount with the low risk records "1"(68470) so that it can be used without any type of modeling.  

![loan_status](https://user-images.githubusercontent.com/111664141/210584154-3084646f-0983-4131-9b28-7c6d6aa73952.png)

Below we will analyze each of the models:  

- Random Oversampling:  
	In random oversampling, instances of the minority class are randomly selected and added to the training set until the majority and minority classes are balanced.  
	Applying this type of model, we arrive at the figure below where we can see that in addition to the accuracy score of 0.64 being low, and the confusion matrix presenting a high number of erroneous predicted, the classification report also shows us that the precision and sensitivity for those considered high risk ("0") are very low.   
		
![RandomOversampling](https://user-images.githubusercontent.com/111664141/210584487-80229b8a-00b7-425e-8a61-7eaee1c7a9ee.png)

- SMOTE Oversampling:  
	The synthetic minority oversampling technique (SMOTE) is similar to Random Oversampling, but use interpolated to create new instances.  
	In this technique, we had results similar to Radom, with a low accuracy of 0.66, a high number of erroneous predicted and insignificant numbers in the classification reports with a precision of only 0.01 for the high risk.  
	
![SMOTEOversampling](https://user-images.githubusercontent.com/111664141/210584658-af932412-80dc-497e-8061-5ad6370cebec.png)
	
- Cluster Centroid Undersampling:  
	Cluster centroid undersampling is akin to SMOTE. The algorithm identifies clusters of the majority class, generates centroids, then the majority class is undersampled down to the size of the minority class.  
	Using this technique, we reached an accuracy (0.54) even lower than the two previous techniques, with the confused matrix presenting a False Positive (10324) much higher than the True Negative (6780) and with the classification report with very inexpressive numbers.   
	
	![ClusterCentroids](https://user-images.githubusercontent.com/111664141/210585219-1adbca69-e152-48d3-a359-3e28608b374c.png)

- SMOTEEN:  
	SMOTEENN combines the SMOTE(oversampling) and Edited Nearest Neighbors (ENN)(undersampling) algorithms. SMOTEENN is a two-step process: oversample the minority class with SMOTE and clean the resulting data with an undersampling strategy.  
	Although this technique presents an accuracy of 0.67, a little better than the previous results, the number of erroneous predictions in the confusion matrix was also high and the classification report presented inexpressive numbers.  
	
![smoteen](https://user-images.githubusercontent.com/111664141/210585817-5be8b8b5-868d-474c-9f06-0ebf97844b58.png)

- Balanced Random Forest Classifier:  
	Random forest algorithm sample the data and build several smaller, simpler decision trees. Each tree is simpler because it is built from a random subset of features.  
	From the results of the confusion matrix, even though the precision for high risk is high, the recall is low (0.37), which is indicative of a large number of false negatives. The F1 score is also low (0.52).  
	
![Radom_Forest](https://user-images.githubusercontent.com/111664141/210586072-b2c65420-2d9e-4f40-b722-b8f442cbbf38.png)

	In the random forest algorithm we rank features by their importance, which allows us to see which features have the most impact on the decision. Below we show the most important ones:  
	
![variables](https://user-images.githubusercontent.com/111664141/210586190-c1737cda-92a2-4bdd-af45-5f3952e7f839.png)


- Easy Ensemble AdaBoost Classifier:  
	In this algorithm the classifier is an ensemble of AdaBoost learners trained on different balanced bootstrap samples. The balancing is achieved by random under-sampling.  
	In this model, although the accuracy is high (0.93), the precision for the high risk is very low (0.09), indicating a high number of false positives. The f1 score is also low (0.16).  
	
![AdaBoost](https://user-images.githubusercontent.com/111664141/210586300-5fc9e912-4dad-4a72-bf0f-2a988d4636fa.png)


# Summary:
Analyzing all the above data from the applied machine learning, we can see that the model that presented the best accuracy was the Easy Ensemble AdaBoost Classifier. But even though this is the model with the best accuracy, it did not present the other statistical data expressive enough for this model to be reliable enough to be used.  
As none of the other machine learning algorithms performed well in predicting those with high credit risk, we do not recommend using them.  
Therefore, it is recommended that new studies be carried out to find a new model that presents more accurate statistics in the classification of customers considered at high risk for credit cards.  

The machine learning algorithms Random Oversampling, SMOTE, Cluster Centroid and SMOTEEN are available in the credit_risk_resampling.ipynb file.  
The machine learning algorithms Balanced Random Forest Classifier and Easy Ensemble AdaBoost Classifier are available in the credit_risk_ensemble.ipynb file. 
