# User Modeling for Detection of Intent to Lie in Likert-Based Online Forms Using Low-Level Interactions

## About

This is the official repository for the research paper "User Modeling for Detection of Intent to Lie in Likert-Based Online Forms Using Low-Level Interactions". The research focuses on identifying lies in Likert-style personality questionnaires. The repository includes the processed dataset used for training the model, the data processing pipeline, and the model evaluation steps. The goal is to enable other researchers to reproduce the data manipulation and model development processes. If you have any questions, you can contact the authors using the [contact information provided below](#a-authors).

#### Table of Contents
* [Paper Citation](#a-citation)
* [Datasets](#a-datasets)
* [Questionnaire Preview](#a-questionnaire)
* [Scripts](#a-scripts)
* [Authors](#a-authors)
* [Licence](#a-licence)

## <a name="a-citation"> Paper Citation
TBA

## <a name="a-datasets"> Dataset
In this study, we created a dataset that includes information on user behavior during completion of the Big 5 personality questionnaire. A portion of the users were instructed to present themselves as better than they actually are while filling out the questionnaire. The original data sources were two: information about the completed questionnaire was obtained from the [Limesurvey](https://www.limesurvey.org/) service, information about the user's interactions with the questionnaire was collected by the [UXtweak](https://www.uxtweak.com/) service. These two data sources were combined. The data was then cleaned, preprocessed, and formatted into a structure that is suitable for machine learning. The dataset contains pageview records, with each row representing metrics for a single pageview - [Dataset one-pageview-per-one-row](Data/Prepared_datasets/dataset_one_pv_per_one_row.json).
  
### <a name="a-dataset-access"> Dataset Access  

To access the original anonymized dataset, please contact the authors at dielie.research([AT])gmail.com.

## <a name="a-questionnaire"> Questionnaire Preview

We were using 2 variants of the same questionnaire with different instruction. Also, it was required to use mouse during questionnaire completion.

<table>
  <tr>
    <td align="center"><img src="Questionnaire/Preview/Mouse alert.jpg">Mouse</td>
    <td align="center"><img src="Questionnaire/Preview/Faking Good Question.jpg">Faking Good</td>
    <td align="center"><img src="Questionnaire/Preview/Honest Question.jpg">Honest</td>
  </tr>
</table>

Previews of the study are available here:
  - [Study - ENG](https://study.uxtweak.com/webusability/Tih31u3YlnxIQWI7hzKHN)
  - [Study - SK](https://study.uxtweak.com/webusability/t3L55N4ZIWhAkKory8Br2)
  
Study randomly selects you one of two variants of questionnaire variants. To access questionnaire directly, you can use these links:
  - [FG - ENG](https://delie.limesurvey.net/628192?lang=en)
  - [H - ENG](https://delie.limesurvey.net/778728?lang=en)
  - [FG - SK](https://delie.limesurvey.net/919549?lang=sk)
  - [H - SK](https://delie.limesurvey.net/192868?lang=sk)

Questionnaire files that can be imported into [Limesurvey](https://www.limesurvey.org/):
  - [FG - ENG](Questionnaire/Files/fg_en.lss)
  - [H - ENG](Questionnaire/Files/h_en.lss)
  - [FG - SK](Questionnaire/Files/fg_sk.lss)
  - [H - SK](Questionnaire/Files/h_sk.lss)

## <a name="a-scripts"> Scripts
The scripts for this project are all written in Python (version 3.10.7), with the aid of various libraries obtained through pip (version 22.2.2). They were run on Jupyter notebooks. A detailed list of dependencies can be found in the [requirements file](Scripts/requirements.txt). We recommend using a [virtual environment](https://docs.python.org/3/library/venv.html) to install the necessary components and start the notebooks.

The scripts are intended to be run in the order in which they are numbered. This repository contains all the data needed to run scripts from 05 to 09. To access the rest of the data, follow the instructions in the [Dataset Access](#a-dataset-access) section.

#### [1 - Pairing pageviews with coresponding question](Scripts/01_Pageviews_pairing_v0.ipynb)

Script for pairing pageviews with BIG5 questions. The function loads session data and extracts the text of the questions displayed on each pageview. This text is compared to the BIG5 questions, and if a match is found, the pageview is marked with the corresponding page number. The resulting pairs are saved.

#### [2 - Extraction of mouse events](Scripts/02_Events_preparing_script_v0.ipynb)

Script for extracting important data from sessions JSON. For every pageview of session, *move, scroll, click and input* information are extracted and saved. Script creates new dataset containing only necessary information.

#### [3 - Calculation of movement metrics](Scripts/03_Sessions_metrics_calculator_v0.ipynb)

Script for calculation of all metrics of mouse movements based on extracted events. All features of Machine Learning algorithms are metrics calculated by this script.

#### [4 - Combining dataset of movement metrics with questionnaire responses](Scripts/04_Merge_tables_v0.ipynb)

Combining information about sessions with calculated metrics with information about filled forms with user responses.

#### [5 - Data exploration and cleaning](Scripts/05_Data_exploration_and_cleaning_v0.ipynb)

Simple explorative analysis, proof of concept based on simple statistical test over means of metrics. Script is dropping pageviews from sessions that are not usable.

#### [6 - Data preprocessing and transformations](Scripts/06_Data_Preprocessing_v0.ipynb)

Transformation of **1 row = 1 session** dataframe to **1 row = 1 pageview** dataframe. Script creates dataset suitable for machine learning.

#### [7 - Model training and evaluation](Scripts/07_Model_training_and_evaluation_v0.ipynb)

Script contains explorative analysis of the dataset, feature selection, model selection, cross validation, model evaluation based on pageview classification and also based on session classification. Script is generating reports with metrics of machine learning.

#### [8 - Hyperparameter tuning for Gradient Boosting](Scripts/08_Hyperparameter_GB_v0.ipynb)

Script for search of hyperparameters for Gradient Boosting.

#### [9 - Hyperparameter tuning for Logistic Regression](Scripts/09_Hyperparameter_LR_v0.ipynb)

Script for search of hyperparameters for Logistic Regression.

## <a name="a-authors"> Authors
  
### Eduard Kuric
TBA

### Peter Demcak
TBA

### Peter Smrecek
He is a Machine Learning Engineer and Computer Science student at [Faculty of Informatics and Information Technologies](https://www.fiit.stuba.sk/), [Slovak University of Technology in Bratislava](https://www.stuba.sk/). He is focusing on development and operations in field of Data Science. 
- [LinkedIn](https://www.linkedin.com/in/peter-smrecek/)
- Email: petersmrecek([AT])gmail.com

### General contact
- Email: dielie.research([AT])gmail.com

## <a name="a-licence"> Licence

This work is licensed under a
<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">
Creative Commons Attribution-NonCommercial 4.0 International License.
</a>

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/" style="margin-left: 8rem">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
</a>
