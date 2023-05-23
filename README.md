# Credit-Score-Project
Analysis of Credit score dataset from Kaggle for a case study

Dataset: https://www.kaggle.com/datasets/parisrohan/credit-score-classification?datasetId=2289007&sortBy=voteCount

### General Important Infromation when Working on this Dataset:

The classification lebel is the Credit_Score column present as the last column for train.csv dataset,
test.csv does not contain this column and as such it is impossible to evaluate the model using test.csv

Each customer in dataset appears 8 times, measured for consecutive months from January to August (concrete year is unknown)

### Features in the dataset:

#### Nominal
- **ID** - Identificator for every transaction, primary key in relational database terms.
- **Customer_ID** - Identificator unique for each customer, not primary key, since customers can repeat in the database.
- **Name** - Name of the person.
- **SSN** - Represents the social security number of a person. Should (probably) be unique for each Customer_ID but some values appear to be corrupted in the dataset. In the US first 4 digits used to be related to geaographic area but since 2011 this is no longer the case, so depending on when the dataset was constructed it might not be useful anymore.

- **Occupation** - Job of the customer. Some values are denoted as multiple-> _ characters but we can infer the real occupation by looking at different rows of with the same *Customer_ID
- **Payment_Behaviour** - Seems categorical but very verbouse and contains corrupted values like: !@9#%8
- **Credit_Score** - Classification variable (TARGET). Possible values: "Poor, Standard, Good"
- **Type_of_Loan** - String values seperated by ',' sign. When seperated, is nominal and could be transformed to binary attributes

##### Binary
- **Payment_of_Min_Amount** - Represents whether only the minimum amount was paid by the person. Values like: "Yes, No, NM". NM could mean Not Mentioned but it is not stated explicitly.


#### Ordinal
- **Month** - Month names from January to August from some year
- **Credit_Mix** - Possible values: Bad, Standard, Good. Seems to refer to the rating given to previous credits, but I am not certain. Definiton according to chatgpt is: "Credit mix refers to the types of accounts that make up your credit report. It determines 10% of your FICO score. The different types of credit that might be part of your credit mix include credit cards, student loans, automobile loans, and mortgages.". Missing values denoted with '-'

#### Numerical (Many values contain _ in them and ranges of attributes are broken)
##### Integer
- **Age** - Age of the person (integer). Some value contain _, range is incorrect negative or super high ages. *[Cleaning - remove _, convert to int, fix range]*
- **Num_Bank_Accounts** - Number of bank accounts owned by the given customer. Possible errors/outliers like: 1414.
- **Num_Credit_Card** - Represents the number of other credit cards held by a person. Also contains errors/outliers like: 1385.
- **Num_of_Loan** - Represents the number of loans taken from the bank. Some values contain _ at the end or errors like: -100
- **Interest_Rate** - Represents the interest rate on credit card. Contains some errors since I think that: 5318 is not legal
- **Num_of_Delayed_Payment** - Represents the average number of payments delayed by a person. Contains some NaNs
- **Num_Credit_Inquiries** - Represents the number of credit card inquiries. Possibly contains errors/outliers like: 1936.0 \
- **Delay_from_due_date** - Represents the average number of payments delayed by a person.
- **Credit_History_Age** - Represents the age of credit history of the person. Represented as a string like: "22 Years and 1 Months". Missing values denoted using "NA". *[Cleaning - convert to int, remove NA]*
#### Float
- **Annual_Income** - Annual income of the customer. Some values contain _ at the end of the number for some reason, like: 35547.71_. Also there seem to be some significant outliers or errors like for example customer with Customer_ID: CUS_0x284a had Annual_Income=131313.4 for transcation ID=0x164f but then had Annual_Income=10909427.0 for transaction ID=0x1650 \
- **Monthly_Balance** - Represents the monthly balance amount of the customer (in USD).
- **Amount_invested_monthly** - Represents the monthly amount invested by the customer (in USD). Contains missing values and some values denoted as in an unexpected way like: "\_ \_1000\_ \_" \
- **Total_EMI_per_month** - Represents the monthly amount invested by the customer (in USD). EMI is a fixed payment amount made by a borrower to a lender at a specified date each calendar month \
- **Monthly_Inhand_Salary** - Represents the monthly base salary of a person. Contains a lot of missing values and may also contain outliers, although it is not certain. This time there does not seem to be a problem with _ sign at the end of some values but it may require further analysis. \
- **Changed_Credit_Limit** - Represents the percentage change in credit card limit. Can be negative.
- **Outstanding_Debt** - Represents the remaining debt to be paid (in USD).
- **Credit_Utilization_Ratio** - Represents the utilization ratio of credit card. Credit utilization is the ratio of your outstanding credit balances (on both credit cards and lines of credit) compared to your overall credit limit combined across your accounts. For example, if you currently have a balance of $500 against your $1,000 credit limit, your credit utilization is 50%.

### Data Cleaning
- Set all weird values to NaN
- Fix missing values in categorical data (Name, Occupation, Payment_Behaviour, Credit_Mix), Probably leave Payment_of_Min_Amount as is because NM can be important
- Augment list in Type_of_Loan to binary attributes

- Remove trailing _ from numerical values
- Convert numerical values to int
- Convert Credit_History_Age to int (maybe number of months)
- Fix ranges of integer numerical values (except Credit_History_Age) - you can find correct range by finding minimum and maximum mode, where modes are calculated for each customer
- Fix ranges of float numerical values - similiar approach as above but maybe use median or mean instead of mode
