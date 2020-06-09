## Data Science Question

Given the dataset from http://www.cbioportal.org/ is it feasable to build a classification model that can accurately predict if a patient will survive or die from breast cancer?

## Table of Contents

#### Code Folder

**Breast Cancer Survival Modeling.ipynb** - Jupyter notebook with all Imports, EDA, and Modeling

#### Data Folder

**brca_metabric_clinical_data (1).tsv** - Breast cancer tumor dataset of 2509 patients conatining 35 features from http://www.cbioportal.org/study/clinicalData?id=brca_metabric

## Data and Process Overview 

The dataset used in this analysis was sourced from CBioPortal.org and included two studies: One from 2012 and another from 2016. The dataset included 2509 unique breast cancer patients and 35 features.

Created a feature ‘died_survived’ that classifies patients who survived breast cancer or died of other causes as 0 and classifies patients who died of breast cancer as 1. This became the y variable for the classification models.

During exploratory data analysis, I compared the correlation of all initial features to ‘died_survived’ and dropped those with correlation <=(+-0.10) from the data frame.
This was done to maximize the number of patients included in modeling while eliminating null values. By dropping the low correlation columns (19) an additional 261 cases (1,353 total) were able to be included in the modeling. 

2nd degree polynomial feature engineering was utilized to create new interaction variables for potential inclusion in modeling. All features were run through a Ridge Regression to see which has the most impact. The enigneered fearures with the top 4 highest impacting coeficients were inlcuded in modeling.

Seven different classification models (Logistic Regression, Bagging Classifier, Support Vector Classifier, AdaBoost, KNN, Decision Tree, and Random Forrest) were fit and evaluated for: F1 Score, Specificity, Sensitivity, Accuracy, Precision, ROC AUC Score, and Cross Val Score.

## Data Dictionary

| Feature | Description | Status in Model |
| --- | --- | --- |
| Study ID | ID number of breast cancer study | Not Included |
| Patient ID | Unique identification number of patient | Not Included | 
| Sample ID | Unique identification number of the tumor sample taken | Not included |
| Age at Diagnosis | Age at which patient was diagnosed with breast cancer | Not Included |
| Type of Breast Surgery | Type of surgery performed | Not Included |
| Cancer Type | Always 'Breast Cancer' | Not Included |
| Cancer Type Detailed | Specific type of breast cancer | Not Included |
| Cellularity | The proportion of cancer within the residual tumor bed | Not Included |
| Chemotherapy | Whether or not Chemotherapy was performed | Included |
| Pam50 + Claudin-low subtype | Genetic classifier of breast cancer subtypes (7 subtypes) | Included |
| Cohort | Patient group (1 - 9) | Not Included |
| ER status measured by IHC | Either positive or negative, whether or not the cancer cell grows in response to estrogen | Not Included |
| ER Status | Either positive or negative, whether or not the cancer cell grows in response to estrogen | Not Included |
| Neoplasm Histologic Grade | 1 to 3 score of how fast growing and normal the cancer cells are | Included |
| HER2 status measured by SNP6 | Human Epidermal Growth Factor Receptor 2. Approximately one in five breast cancers are driven by amplification and overexpression of HER2 | Not Included |
| HER2 Status | Human Epidermal Growth Factor Receptor 2. Approximately one in five breast cancers are driven by amplification and overexpression of HER2 | Included |
| Tumor Other Histologic Subtype | Subtype of tumor (8 types) | Not Included |
| Hormone Therapy | Whether or not patient was treated with hormone therapy | Not Included |
| Inferred Menopausal State | Whether patient was pre or post menopausal | Not Included |
| Integrative Cluster | 4 Sub-types of breast cancer molecular classifiers | Not Included |
| Primary Tumor Laterality | Whether the tumor was aligned to the right or left | Not Included
| Lymph nodes examined positive | The number of lymph nodes in which cancer was detected | Included |
| Mutation Count | Number of cancer mutations detected | Not Included |
| Nottingham prognostic index | Determines prognosis following surgery. Calculated score using three pathological criteria. Lower is more survivable | Included |
| Oncotree Code | Code for the type of breast cancer based on the OncoTree cancer classifier tree (6 Types) | Not Included |
| Overall Survival (Months) | Length of time patient survived with and after breast cancer | Not Included |
| Overall Survival Status | Living or Deceased | Not Included | 
| PR Status | Whether or not the breast cancer cells have progesterone receptors | Included |
| Radio Therapy | Whether or not Radio Therapy was performed | 
| Number of Samples Per Patient | How many samples were taken from the patient | Not Included |
| Sample Type | All sample types are ‘Primary’ | Not Included |
| 3-Gene classifier subtype | Used to identify the four primary molecular subtypes of breast cancer | Inlcuded |
| Tumor Size | Size of the tumor | Included |
| Tumor Stage | Stage of the tumor (0 to 4) | Included |
| Patient's Vital Status | Whether or not the patient died of breast cancer or survived (y variable) | Included |

## Required Software

- pandas
- numpy
- sklearn.model_selection: train_test_split, cross_val_score, GridSearchCV
- sklearn.preprocessing: StandardScaler, PolynomialFeatures
- sklearn: metrics
- matplotlib
- seaborn
- sklearn.linear_model: Ridge, LogisticRegression
- sklearn.tree: DecisionTreeClassifier
- sklearn.ensemble: BaggingClassifier, RandomForestClassifier, AdaBoostClassifier
- sklearn.svm: SVC
- sklearn.neighbors: KNeighborsClassifier
- sklearn.pipeline: Pipeline
- sklearn.metrics: f1_score, confusion_matrix, roc_auc_score
- tensorflow.keras.models: Sequential
- tensorflow.keras.layers: Dense

