# User Modeling for Detection of Intent to Lie in Likert-Based Online Forms

## About

This is the official repository for the research paper "User Modeling for Detection of Intent to Lie in Likert-Based Online Forms". Our research focuses on identifying lies in questionnaires consisting of Likert scale questions. The repository includes the processed version of the dataset gathered during the experiment that is used for training the machine learning model, along with the data processing pipeline and the model evaluation steps. The purpose of this repository is to enable other researchers to reproduce the data manipulation and model development processes. If you have any questions, you may contact the authors at the [contact information found below](#a-authors).

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
In this study, we created a dataset that contains information on user behavior during completion of the Big Five personality questionnaire. To collect data in two groups, Honest (H) and Faking-good (FG) (a.k.a. lying in the context of a personality questionnaire), one half of participants was instructed to present themselves in the questionnaire as better than they actually are, with lying being explicitly encouraged. The other half was asked to fill in the questionnaire truthfully. The dataset has two original sources of information. [Limesurvey](https://www.limesurvey.org/) provided completed questionnaire data. [UXtweak](https://www.uxtweak.com/) provided information about the user's low-level interactions with the questionnaire (mouse dynamics). The data was then cleaned, preprocessed, and formatted into a structure that is suitable for machine learning. The dataset contains pageview records, with each row representing metrics for a single pageview - [Dataset one-pageview-per-one-row](Data/Prepared_datasets/dataset_one_pv_per_one_row.json).
  
### <a name="a-dataset-access"> Dataset Access  

To access the original anonymized dataset, please contact the authors at delie.research([AT])gmail.com.

## <a name="a-questionnaire"> Questionnaire Preview

Betweem the H (Honest) and FG (Faking-good) groups, we used 2 variants of the same questionnaire with different instruction. Participants were required to use a physical computer mouse during the questionnaire completion.

<table>
  <tr>
    <td align="center"><img src="Questionnaire/Preview/Mouse alert.jpg">Mouse</td>
    <td align="center"><img src="Questionnaire/Preview/Faking Good Question.jpg">Faking Good</td>
    <td align="center"><img src="Questionnaire/Preview/Honest Question.jpg">Honest</td>
  </tr>
</table>

Previews of the study to view the experiment from the perspective of the participants (without any data being collected):
  - [Study preview - English translation](https://study.uxtweak.com/webusability/duWYfMNUeZSL4odlpZJDa)
  - [Study preview - Original Slovak version used during the experiment](https://study.uxtweak.com/webusability/1gy7SMSugUNnLJtWKtJ0L)
  
The study randomly assigns participants one of two questionnaire variants. Previews to access specific variants directly:
  - [FG - Faking-good response triggering instructions variant - English translation](https://delie.limesurvey.net/628192?lang=en)
  - [H - Honest response triggering instructions - English translation](https://delie.limesurvey.net/778728?lang=en)
  - [FG - Faking-good response triggering instructions variant - Original Slovak version](https://delie.limesurvey.net/919549?lang=sk)
  - [H - Honest response triggering instructions - Original Slovak version](https://delie.limesurvey.net/192868?lang=sk)

Questionnaire files that can be imported into [Limesurvey](https://www.limesurvey.org/):
  - [FG - Faking-good response triggering instructions variant - English translation](Questionnaire/Files/fg_en.lss)
  - [H - Honest response triggering instructions - English translation](Questionnaire/Files/h_en.lss)
  - [FG - Faking-good response triggering instructions variant - Original Slovak version](Questionnaire/Files/fg_sk.lss)
  - [H - Honest response triggering instructions - Original Slovak version](Questionnaire/Files/h_sk.lss)

## <a name="a-scripts"> Scripts
The scripts for this project are all written in Python (version 3.10.7), with the aid of libraries obtained through pip (version 22.2.2). They were run on Jupyter notebooks. A detailed list of dependencies can be found in the [requirements file](Scripts/requirements.txt). We recommend using a [virtual environment](https://docs.python.org/3/library/venv.html) to install the necessary components and start the notebooks.

The scripts are intended to be run in the order in which they are numbered. This repository contains all the data needed to run scripts from 05 to 09. To access the rest of the data, follow the instructions in the [Dataset Access](#a-dataset-access) section.

#### [1 - Pairing pageviews with coresponding question](Scripts/01_Pageviews_pairing_v0.ipynb)

Script for pairing pageviews with Big Five questions. The function loads session data and extracts the text of the questions displayed on each pageview. This text is compared to the Big Five questions, and if a match is found, the pageview is marked with the corresponding page number. The resulting pairs are saved.

#### [2 - Extraction of mouse events](Scripts/02_Events_preparing_script_v0.ipynb)

Script for extracting important data from sessions JSON. For every pageview of session, *move, scroll, click and input* information is extracted and saved. This script creates new dataset containing only necessary information.

#### [3 - Calculation of movement metrics](Scripts/03_Sessions_metrics_calculator_v0.ipynb)

Script for calculation of all metrics of mouse movements based on extracted events. All attributes of the proposed user model that are also used as features in machine learning algorithms are metrics calculated by this script.

#### [4 - Combining dataset of movement metrics with questionnaire responses](Scripts/04_Merge_tables_v0.ipynb)

Combining information about sessions with calculated metrics with information about filled-in forms with Big Five questionnaire responses.

#### [5 - Data exploration and cleaning](Scripts/05_Data_exploration_and_cleaning_v0.ipynb)

Simple explorative analysis, proof of concept based on simple statistical test over means of metrics. This script drops unusable pageviews from sessions.

#### [6 - Data preprocessing and transformations](Scripts/06_Data_Preprocessing_v0.ipynb)

Transformation of **1 row = 1 session** dataframe to **1 row = 1 pageview** dataframe. This script creates the dataset suitable for machine learning.

#### [7 - Model training and evaluation](Scripts/07_Model_training_and_evaluation_v0.ipynb)

Script contains explorative analysis of the dataset, feature selection, model selection, cross validation, model evaluation based on pageview classification and also based on session classification. This script generates reports with metrics of machine learning.

#### [8 - Hyperparameter tuning for Gradient Boosting](Scripts/08_Hyperparameter_GB_v0.ipynb)

Script for search of hyperparameters for Gradient Boosting.

#### [9 - Hyperparameter tuning for Logistic Regression](Scripts/09_Hyperparameter_LR_v0.ipynb)

Script for search of hyperparameters for Logistic Regression.

## <a name="a-authors"> Authors
  
### Eduard Kuric
He is a researcher and lecturer at [Faculty of Informatics and Information Technologies](https://www.fiit.stuba.sk/), [Slovak University of Technology in Bratislava](https://www.stuba.sk/). He is also a founder of [UXtweak](https://www.uxtweak.com). His research interests include human-computer interaction, user modeling, and machine learning.
- Email: eduard.kuric([AT])stuba.sk
- [LinkedIn](https://www.linkedin.com/in/eduard-kuric-b7141280/)
- [Google Scholar](https://scholar.google.com/citations?user=MwjpNoAAAAAJ&hl=en&oi=ao)

### Peter Demcak
He is a researcher at [UXtweak](https://www.uxtweak.com/). His current research topics of interest involve user behavior, UX research methods and design practices, and machine learning.
- Email: peter.demcak([AT])uxtweak.com

### Peter Smrecek
He is a Machine Learning Engineer and Computer Science student at [Faculty of Informatics and Information Technologies](https://www.fiit.stuba.sk/), [Slovak University of Technology in Bratislava](https://www.stuba.sk/). He is focusing on development and operations in field of Data Science. 
- [LinkedIn](https://www.linkedin.com/in/peter-smrecek/)
- Email: petersmrecek([AT])gmail.com

### General contact
- Email: delie.research([AT])gmail.com

## <a name="a-licence"> Licence

This work is licensed under a
<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">
Creative Commons Attribution-NonCommercial 4.0 International License.
</a>

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/" style="margin-left: 8rem">
<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" />
</a>
