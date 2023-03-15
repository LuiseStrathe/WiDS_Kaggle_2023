# WiDS_Kaggle_2023

Contribution to the datathon hosted by <a href="https://www.kaggle.com/competitions/widsdatathon2023">Women in Data Science as Kaggle competition</a>.

The goal for the model is to predict mean temperatures from given 245 features. The dataset contains 376k samples for training and validation.


<br>

## Approach

<dl>
<dt>1. Data Analysis</dt>
<dd>The data contains many feature clusters, such as one metric for several points in time within one sample. Some other inputs, such as the timestamp not only represents a trend, but also periodicity and therefore information in a higher dimension than the given 1. </dd>

<dt>2. Data Pipeline</dt>
<dd>Each version of the data pipeline processes the given raw data into a dataset ready for training, validation and testing. To avoid leaking all sets go through the same functions. The validation and test were excluded for parametrizing the pipeline. 

Feature engineering and selection evolved given their test performance on different models (4).</dd>

<dt>3. Model Training</dt>
<dd>Models (RMSE, regression) were trained either as random forest (XGBoost) or DNN (Keras). Both model types were tuned on their test performance (4) for given datasets. </dd>

<dt>4. Dataset and Model Evaluation</dt>
<dd>Based on the test set performance the models and datasets were tuned in an alternating pattern (basic data to tune first model > then evolve data with given model > ...)</dd>
</dl>

<b>Findings</b>: 
RF's performed better than DNN's and were less sensitive to the data. Yet feature reduction lowered results. Especially after feature selection the DNN's performance improved significantly comes closer to RF - this would be a thread to observe for overall improvement. 

<br>
<b>Best result (RMSE):  
0.259 (RF) | 0.338 (DNN)</b>

<br>

## Overview & Structure

The project is structured as follows:

```

├── data
│   ├── additional       # additional input for feature engineering
│   ├── preprocessed     # versioned datasets for training 
│   └── raw              # data as provided by the competition
│ 
├── models               # trained models
│ 
├── notebooks            # executionable code (no python scripts)
│   ├── pre              # data analysis & 
│   │                      preprocessing pipeline (versioned)
│   ├── train            # training models 
│   │                      (Random Forests_XGBoost and NN_Keras)
│   └── results          # model evaluation
│ 
├── results              # output on test data, ready for upload
│ 
└── README
```