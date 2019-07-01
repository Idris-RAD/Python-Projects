Breast Cancer Prediction


********************
Slides presentation :

https://slides.com/jvbw/breast-cancer-prediction


********************

Dataset comes from : https://www.kaggle.com/uciml/breast-cancer-wisconsin-data

********************


*** Exploratory analysis :

Its initial shape is 512 rows for 31 columns, which is fairly small.
We'll try and minimize data loss while cleaning.
The good news is : all data types are correct (floats) and there are no NaNs, after dropping an empty 'unnamed' column.

Some visualizations : there seems to be detectable differences between benign and malignant tumour characteristics.

The correlation matrix shows some strong collinearity between non target columns, which means we'll be able to sample features.

*** Outliers :
I tested outliers using IQR and Zscores.

The aim was to eliminate outliers, while keeping enough data (small dataset) and data representativeness.
The ratio between the target labels (benign and malignant) should be 65/35, MAX !

IQR ended up eliminating too much data.

Zscores worked well, even though my data didn't have a perfect normal distribution.
I also tinkered with the threshold, making it a bit larger, to lose less data.

*** Modelling :

Using Logistic Regression with sklearn, my first model was already fairly accurate.

The confusion matrix was :
[[71,  2],
[ 1, 29]]

Not bad for a first try ! However, I wanted to minimize false positives and negatives as much as possible.
I moved on to feature engineering to improve the model.

*** Feature engineering :
Using RFE, I narrowed down the columns to 10. I could probably have used even less.

Testing logistic regression with less columns, the confusion matrix was perfect :
[[71,  0],
 [ 0, 32]]

*** More models :

I tested different models. Gaussian Naive Bayes also gave perfect results.
However, KNN and SVM both returned false negatives and positives.

*** PCA :

I used PCA to narrow down to 2 dimensions. The 2 dimensional plot looks good !


*** Conclusions :
All numeric is paradise after working with text/categorical values

Keep it "simple" : logistic regression was the simplest and most accurate

RFE boosted accuracy