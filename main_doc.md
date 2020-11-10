Problem 

A significant fraction of patients who had heart failure is at risk of being readmitted to the hospital. A risk stratification model, i.e. identifying patients who are at higher risk of having another event, can be used by clinicians to identify high risk patients who need immediate treatment. 

Task
1. Propose a solution on how can RWD (i.e. EHR data) be used to develop a risk stratification model.
- What kind of data would you use for this purpose? (You can assume EHR covers patient demographics, in-patient visits, diagnosis, prescriptions, lab measurements, & clinical notes)
    
    Good data is essential for model training. I would recommend to obtain as much data as we can. EHR data is important and the main source to provide feature to the model, other public data source such may also be worth to look into such as location wise general disease population, death rate, etc.
- What is the modelling approach and how would you use the data in the model?

    A duration-based classification approach can be considered because the readmission rate prediction without a specific duration can be less determinative. Therefore, I will build a classification model to predict how likely a patient will be readmitted within 30 days (the duration should be determined by the subject matter experts). This approach could also help to utilize more data points for the purpose of training, e.g. a patient hasn’t been readmitted within 30 days can be labelled as 0 without the need of tracking.

    For a benchmark, I would start with a simple logistic regression model with regularization. An Xgboost model can be explored next as a more complex non-linear approach. ROC-AUC should be used for model performance evaluation.







2. Notes or reports in the form of free text are commonly generated in clinical practice, which might contain information that could be useful in understanding patient condition and risk factors that are not captured in the structured database. Attached csv file contains samples of some radiology reports or notes.
- How would you use them to solve the problem above? What kind of information would you extract? 
  
    There are definitely a lot of information contained in both Description and Notes columns. There are 2 ways to extract information to get started. 
    - A Custome Named entity recognizer. A custom NER can be used to extract all kinds of info such as patient demographics, in-patient visits reason, prescribed exam, diagnosis, medications, lab measurements etc. However, without custome labelled training data, it is difficult to build a custom NER. Therefore, I tested a pretrained NER model using SpaCy and it does not satisfy our need as expected.
    - Document embedding. There are many ways to embed documents, and the one I chose to start with is Word2vec GloVe embedding. Defintely, Bert family models are more powerful and can be our next step. 


- Can you develop a proof-of-concept NLP pipeline that extracts information that you need for the model? 
  
    Please find the jupyter notebook.




3. Can you propose the other ways RWD can be leveraged to reduce the disease burden? For example, can you suggest effective interventions to mitigate risk for high-risk patients?

    - Entity normalization especially on medical terms will definitely be very helpful across the EHR records. 

    - LDA topic modeling as an unsupervised way to discover and tag the EHR records.

    - Build the Knowledge graph based on diseases as nodes and symptoms as edges to further understand the diseases.





