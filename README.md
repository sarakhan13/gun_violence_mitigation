# gun_violence_mitigation
Deploying A.I-Driven Solutions to Mitigate Gun Violence

Introduction:

Project Objectives: 
Over the years gun violence such as mass shootings and hate crimes have increased in the USA. “In 2021, the most recent year for which complete data is available, 48,830 people died from gun-related injuries in the U.S, according to the CDC”. In addition, due to many advancements in AI, in particular using object detection/ recognition to interact with users in real time. Therefore, we plan to train AI to detect a suspect’s actions before the damage is caused and alert individuals nearby to avoid neighborhoods that may be dangerous.

Project Goals:
We have chosen to utilize the Washington DC homicide crime dataset from the last six years. This dataset will facilitate our analysis of several key aspects, including the average age of suspects, comparisons of neighborhood crime rates, and seasonal crime rate variations. 

Data Management:

Dataset:
Two different datasets were used to optimize the project objectives: one focusing on incidents, including mostly homicide and non-fatal shooting crime data, and the other focusing on suspects. These datasets contain comprehensive information on incidents and suspects in the DC area from 2018 to 2023.
The data comes from D.C. Witness, a nonprofit organization dedicated to increasing public awareness of such incidents.

Data Preparation:
The project was executed using Databricks, leveraging SQL and Python for data processing. Several libraries, functions and components were used for various tasks: 
Merging datasets: SparkSession and DataFrame columns(Col)
Linear regression: StringIndexer, OneHotEncoder, VectorAssembler,  and Pipeline
Model training: DecisionTreeClassifier, LogisticRegression, and RandomForestClassifier
Prediction evaluation: MulticlassClassificationEvaluator
Confusion matrix: confusion_matrix, seaborn, matplotlib.pyplot, pandas, and seaborn
Classification model assessment: classification_report
Visualization: matplotlib.pyplot

Data Merging:
The Incident and Suspect datasets were merged using an Inner join function, resulting in a combined dataset. Prior to merging, the Incident dataset contained 1960 records, while the Suspect dataset had 1458 records. However, after merging, only 573 records remained. To accomplish this merging process, SparkSession and DataFrame columns (Col) were utilized to match the corresponding records between the two datasets. Specifically, the join was performed based on the following keys from the Incident dataset: incident_year, incident_month, incident_day, block_number, street_name, neighborhood, ward, city, state, and zip code.

Data Cleaning:
By removing irrelavnt columns and dropping null records from relevant columns, the dataset resulted in a total of 406 records and 15 columns. Databricks and Google Colab were utilized in Data Cleaning. This focused dataset allowed for more precise and effective prediction modeling.

Data Transformation:
All categorical features in the dataset regardless of whether they will be used to train a model were transformed first by using a string indexer to convert the categorical values into numeric values and second using one-hot encoding to further encode the numeric values.

Problem: Identifying D.C. ward: 

Based on the features available, street name, zip code, police district, suspect gender, incident type, and neighborhood were the most appropriate features that can influence which of the 8 D.C. wards is an incident occurring. 
The independent variables were transformed using a vector assembler to form one column as “features”. The independent variable was renamed as the “label”. 
The 80% of the dataset was divided into a training set and the rest 20% was reserved to be the training dataset. 
Three models built: Logistic Regression, Decision Tree and Random Forest.
The max depth for Decision Tree and Random Forest is set to 10 and the numTrees parameter for Random Forest is set to 50. These values were determined to give the best results, this was evaluated based on fine-tuning. 

Results:

Using Classification Report and Confusion Matrices for each model the following observations can be made:

Decision Tree:

The model was 93% accurate on the test set. 
The F1 score for Wards 4, 7, and 8 is the highest. This is further validated by the confusion matrix that shows all classes for these wards were classified correctly. 
All instances for Ward 2 were misclassified by the model. 

Logistic Regression: 

The model was 90% accurate on the test set.
The F1 score for Wards 7, and 8 is the highest. All instances for Ward 2 were misclassified by the model. The model also did not perform well on Ward 6 instances.

Random Forest: 

The model was 87% accurate on the test set.
The F1 score for Ward 8 is the highest. All instances for Ward 2 were misclassified by the model. The model also did not perform well on Ward 1 and 6 instances.

Predictive insights and Conclusions:

Decision Tree performed the best among all the three classification models. Logistic regression was 2% less accurate than the Decision Tree model. The Random Forest model performed poorly on the dataset. 
It is interesting to note that in the test set, there were no records from ward 3, this could be due to the random splitting of the dataset or data on ward 3 may be less as compared to other wards.
The imbalance between the dataset for Wards can also influence the training of the model and introduce biases. Distributing the dataset with an equal number of records for each Ward can help enhance the model’s accuracy. This explains why all models predicted poorly on Ward 2.

Detailed Report: https://docs.google.com/document/d/1sdKOy5vkRLUjHA-BoCrGCn7R-jZB6nLQQ5d72upC2sY/edit?usp=sharing
