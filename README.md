# Bank Account Application Fraud Analysis
## Objective
This project analyses applications to open a bank account to find which applicant, behavioural, device and session features are associated with fraud. It tests simple rules on later months, compares them with a basic machine learning model and presents the main patterns in an interactive Power BI dashboard.
## Dataset
The project uses the base file of the [Bank Account Fraud Dataset Suite (NeurIPS 2022)](https://www.kaggle.com/datasets/sgpjesus/bank-account-fraud-dataset-neurips-2022) from Kaggle. It contains 1,000,000 bank account applications with 32 columns. Out of these, 11,029 applications (1.10%) are labelled as fraudulent. Each row represents an application, not a transaction. The data is synthetic and privacy-preserving.It was generated from an anonymised real-world dataset, and some categorical values are coded, so their exact meaning is not available. The dataset is licensed under CC BY-NC-SA 4.0.
The dataset file is not included in this repository. To run the notebook, download `Base.csv` from Kaggle and place it next to the notebook.
## Tools
Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, Jupyter Notebook, Power BI Desktop
## Analysis
Data check (including missing values coded as -1), fraud rate by applicant and application features, behavioural variables, device and session features, features associated with fraud, 3 simple rules set on months 0-5 and tested on months 6-7 and a Random Forest model compared with the rules.
## Key Findings
1. Only 1.10% of applications are fraudulent and the rate rose from 1.03% in months 0-5 to 1.40% in months 6-7, so the data shifts over time.
2. Fraud increases with customer age (from about 0.4% to 5.3%), reaches around 3.7% for housing status BA and 2.47% for Windows devices. Windows applications through TELEAPP have an even higher rate of 5.79%. Proposed credit limits of 1,900-2,100 also show high fraud rates (around12-20%), but these groups contain only a few applications.
3. Fraudulent applications have a lower median name-email similarity (0.29 vs 0.49). Application velocity and session length show much smaller differences between fraudulent and normal applications.
4. Three simple rules (credit limit, name-email similarity and credit risk score) were set on months 0-5 and tested on months 6-7. When at least two rules are triggered, precision reaches 11.45%, around eight times the overall fraud rate, but only 10.4% of fraud cases are detected. When at least one rule is triggered, recall increases to 48.2%, but precision drops to 3.34%.
5. Random Forest finds 63% of fraud (recall 0.63) with a precision of 0.08. This means around 11 false alarms for each detected fraud case. It detects more fraud than the rules, but a large number of its alerts are false positives.
## Power BI Dashboard
I also created an interactive one-page dashboard in Power BI Desktop using the same dataset, with 14 of the 32 available columns. 

*The dashboard shows:*
- Total number of applications, fraud cases and fraud rate.
- Fraud rate by customer age, device operating system, month, housing status and proposed credit limit.
- A matrix comparing device operating systems and application sources.
- Filters for application source and employment status.

The filters update all charts, and selecting a bar (for example windows) also changes the other visuals to show the selected group. The totals match the notebook (1,000,000 applications, 11,029 fraud cases, 1.10%). The Power BI file is not included because it contains a copy of the dataset. Instead, the Power BI (.pbix) file is provided on GitHub for download and further editing.
## Limitations
- The data is synthetic and anonymised, so the patterns may differ from those found in real banking data.
- The test period covers only two months and its fraud rate is higher than in the training period.
- One of the rules was based on a pattern first noticed on the whole dataset and then checked on months 0-5. This may make its results slightly optimistic.
- The model is a basic, untuned Random Forest trained on a 200,000-row sample.
- The dashboard shows descriptive fraud rates only, and some groups (for example high credit limits) contain only a few applications.
- Fraud rates rises strongly with age, and related research reports that models trained on this dataset raise more false alerts for  customers aged 50 and over. This was not tested here.
