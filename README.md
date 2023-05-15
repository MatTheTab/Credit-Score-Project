# Credit-Score-Project
Analysis of Credit score dataset from Kaggle for a case study

Dataset: https://www.kaggle.com/datasets/parisrohan/credit-score-classification?datasetId=2289007&sortBy=voteCount

### General Important Infromation when Working on this Dataset:

The classification lebel is the Credit_Score column present as the last column for train.csv dataset,
test.csv does not contain this column and as such it is impossible to evaluet the model using test.csv

### Explanation of columns in the dataset:

<b> ID </b> - Identificator for every transaction, primary key in relation database terms. <br>
<b> Customer_ID </b> - Identificator unique for each customer, not primary key, since customers can repeat in the database. <br>
<b> Month </b> - According to the original kaggle dataset description:"Represents the month of the year", presumably the date when the request was made. Different values are possible for the same Customer_iD. <br>
<b> Name </b> - Name of the person. <br>
<b> Age </b> - Age of the person (integer). <br>
<b> SSN </b> - Represents the social security number of a person. Should (probably) be unique for each Customer_ID but some values appear to be corrupted in the dataset. In the US first 4 digits used to be related to geaographic area but since 2011 this is no longer the case, so depending on when the dataset was constructed it might not be useful anymore.<br>
<b> Occupation </b> - Job of the customer. String but also a nominal attribute. Some missing values are not actually denoted as multiple-> _ characters  <br>
<b> Annual_Income </b> - Annual income of the customer. Some values contain _ at the end of the number for some reason, like: 35547.71_. Also there seem to be some significant outliers or errors like for example customer with Customer_ID: CUS_0x284a had Annual_Income=131313.4 for transcation ID=0x164f but then had Annual_Income=10909427.0 for transaction ID=0x1650 <br>
<b> Monthly_Inhand_Salary </b> - Represents the monthly base salary of a person. Contains a lot of missing values and may also contain outliers, although it is not certain. This time there does not seem to be a problem with _ sign at the end of some values but it may require further analysis. <br>
<b> Num_Bank_Accounts </b> - Number of bank accounts owned by the given customer. Possible errors/outliers like: 1414. <br>
<b> Num_Credit_Card </b> - Represents the number of other credit cards held by a person. Also contains errors/outliers like: 1385. <br>
<b> Interest_Rate </b> - Represents the interest rate on credit card. Contains some errors since I think that: 5318 is not legal <br>
<b> Num_of_Loan </b> - Represents the number of loans taken from the bank. Some values contain _ at the end or errors like: -100 <br>
<b> Type_of_Loan </b> - String values seperated by ',' sign. When seperated, seems nominal <br>
<b> Delay_from_due_date </b> - Represents the average number of payments delayed by a person. Might be integer or float. <br>
<b> Num_of_Delayed_Payment </b> - Represents the average number of payments delayed by a person. Might be integer or float. <br>
<b> Changed_Credit_Limit </b> - Represents the percentage change in credit card limit. Float numbers, can be negative. <br>
<b> Num_Credit_Inquiries </b> - Represents the number of credit card inquiries. Possibly contains errors/outliers like: 1936.0 <br>
<b> Credit_Mix </b> - Ordinal, seems to refer to the rating given to previous credits, but I am not certain. Definiton according to chatgpt is: "Credit mix refers to the types of accounts that make up your credit report. It determines 10% of your FICO score. The different types of credit that might be part of your credit mix include credit cards, student loans, automobile loans, and mortgages.". Missing values denoted with '-' <br>
<b> Outstanding_Debt </b> - Represents the remaining debt to be paid (in USD). Some values still contain _ sign at the end <br>
<b> Credit_Utilization_Ratio </b> - Represents the utilization ratio of credit card. Credit utilization is the ratio of your outstanding credit balances (on both credit cards and lines of credit) compared to your overall credit limit combined across your accounts. For example, if you currently have a balance of $500 against your $1,000 credit limit, your credit utilization is 50%. <br>
<b> Credit_History_Age </b> - Represents the age of credit history of the person. Represented as a string like: "22 Years and 1 Months". Missing values denoted using "NA". <br>
<b> Payment_of_Min_Amount </b> - Represents whether only the minimum amount was paid by the person. Values like: "Yes, No, NM". NM could mean Not Mentioned but it is not stated explicitly. <br>
<b> Total_EMI_per_month </b> - Represents the monthly amount invested by the customer (in USD). EMI is a fixed payment amount made by a borrower to a lender at a specified date each calendar month <br>
<b> Amount_invested_monthly </b> - Represents the monthly amount invested by the customer (in USD). Contains missing values and some values denoted as in an unexpected way like: \_ \_1000\_ \_" <br>
<b> Payment_Behaviour </b> - Seems categorical but very verbouse and contains corrupted values like: !@9#%8 <br>
<b> Monthly_Balance </b> - Represents the monthly balance amount of the customer (in USD). <br>
<b> Credit_Score </b> - Classification variable. Possible values: "Poor, Standard, Good" <br>
