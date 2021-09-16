# COVID-19 - clinical data to assess diagnosis
Data challenge: https://www.kaggle.com/S%C3%ADrio-Libanes/covid19

<img src="/images/covid_ml.jpg" width="500" alt="Rossmann logo" title="Rossmann" align="right" height="300" class="center"/>

## Purpose of this work
The objective of this work is to provide a machine learning overview using Python language and a real database from Sírio-Libanês Hospital in Brazil. The datase contains health monitoring data of patients in different time windows of events and their eventual evolution to the intensive care unit (ICU).

This can be a great source of study for those who are having their first contacts with machine learning modeling as it is full of detailed explanations.

## Scenario
The covid-19 pandemic has plagued the world since the beginning of 2020, crowding hospitals and resulting in a scarcity of resources.

It is known that healthcare systems can be a scarce resource in pandemic times; therefore, being able to predict whether or not a patient will occupy a bed in ICU can be a strong ally in structuring plans to fight the disease considering the limited resources in terms of medical staff and hospital infrastructure.

The ultimate goal is to avoid collapse in the health care system, which is defined when there are cases above hospital capacity in terms of ICU beds, human resources and personal protective equipment.

One possible solution to avoid this collapse can be obtained with machine learning application.

With machine learning it is possible to adjust algorithms to make predictions or decisions. For this application, it will be used supervised algorithms in order to predict, based in patient's initial medical conditions, if he/she will need an intensive therapy unit or not during the covid-19 treatment.

Three different models (decision tree classifier, random forest classifier and logistic regression) were explanied and evaluated.


## Data understanding
The dataset contains data from just over 380 patients who were admitted at the Sírio-Libanês Hospital for Covid-19 treatment.

All data were anonymized following the best international practices and recommendations by hospital collaborators;  also, the data has been cleaned and scaled by column according to Min Max Scaler to fit between -1 and 1.

For each patiet, data such as blood results and vital signs were aggregated by time windows in chronological order. The objective of this study is to predict, based on health data, whether a particular patient will need an ICU or not.

It can't be used the data when the target variable is present, as it is unknown the order of the event (maybe the target event happened before the results were obtained); this is represented in the following figure.

<p align="center">
  <img src = "/images/ICU_use_data.jpg" width="800"> <br>
</p>

Early identification of those patients who will develop an adverse course of illness (and need intensive care) is a key for an appropriate treatment (saving lives) and to managing beds and resources. This is the reason why in this work all models are using only the values of the first time window (0-2h) to predict whether, in any other time window, the patient will go to the ICU or not.

## Evaluation metrics adopted
The metrics were chosen based on the worst scenario of the 2 types of errors:
- False positive: the patient occupied an ICU bed that he/she would not need to occupy and there was a lack of beds for those who needed it, and the patient without an ICU bed ended up dying.

- False negative: the patient went home, his/her health deteriorated and he/she died.

In the worst scenario for the false positive cases there is still a chance that there will be no collapse of the ICU system and, as a result, there will be no more deaths because of this error. But we cannot say that about the false negative error.

To evaluate the performance of the models, **recall** metric (which is sensitive to false negatives) and the **F1-score** were used; note that precision (which is sensitive to false positives) is still present in the F1-score metric as this is a harmonic average of recall and precision, being very sensitive to any low value of these metrics.

## Data cleaning and modeling - iterative process

Four different rounds of training and evaluation of each of the three models were performed.

For each of these rounds, datasets were reworked, in addition to hyperparameter tuning.

In summary about the reworks in the dataset:
- round 1: after the first data treatment, including forward filling and backward filling to fill missing values (always considering the patient's own data); in addition, 1 patient was removed for extreme lack of data and 32 were also removed for having already arrived at the hospital and being forwarded directly to the ICU because.
- round 2
- round 3
- round 4

## Hyperparameter tuning
As the objective of this work is to provide a machine learning overview using Python language, a slow and visual process was used to adjust the hyperparameters.
For each of the variations of the hyperparameters, boxplot graphs were plotted containing the performance obtained with the different values of the studied hyperparameter, all evaluated using cross-validation (stratified, n_splits = 3 and n_repeats = 10).

The evaluated hyperparameters of each model were:

- decision tree classifier: max_depth
- random forest classifier: max_depth, n_estimators
- logistic regression: solver, C

### Example of the hyperparameter tuning

To visualize the overfitting process, the performance for each of the hyperparameter variations was compared with the training data; in other words, how the model performed, testing with the data used for its construction.

EXAMPLE 1

<p align="center">
  <img src = "/images/tuning_ex_1.jpg" width="800"> <br>
</p>

EXAMPLE 2
EXAMPLE 3

The choice of the hyperparameter value was always made outside the overfitting zone, which is when the model performs on the verge of perfection.

## Model performance

TABLE OF PERFORMANCE

## Conclusions
As will be seen throughout this work, it is part of the data scientist's life to iterate between exploratory data analysis, treatment of the database, modifications of the hyperparameters of the estimators, model training and testing;

An extensive exploratory data analysis was carried out, which resulted in the elimination of some data that would compromise the quality of the models;

A first round of machine learning was carried out for 3 different estimators: decision tree classifier, random forest and logistic regression; it was concluded, however, that the performance of such predictions represented nothing, being a mere product of luck;

To support a real evaluation of the model, cross-validation was presented and performed for other 4 training and testing rounds.

In addition to cross-validation, some hyperparameters were also varied and tested for the 3 different estimators mentioned above; the difference in predictive power, in general, varied considerably as the hyperparameter varied;

The best estimator, for the analyzes carried out in this work, was the random forest, followed by the logistic regression;

It was noticed a considerable increase in performance for all the estimators by reducing the number of database columns (features) that were duplicated and highly correlated with themselves; however, by exaggerating the dose and removing more features, we negate the benefits previously obtained;

It was diagnosed that in the initial treated database there was a data leakage that could be impacting the predictive capacity of the models; a new round of tests was carried out, but there was no success in improving the performance obtained previously;

The failure of this attempt, however, has resulted in reflection and consideration of the impact on classification analysis when data collection and data availability is already carried out in an unbalanced manner from the beggining of the work.

Next steps and strategies were discussed in an attempt to improve the predictive performance of the estimators.
