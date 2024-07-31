# BFSI_Credit_Risk_Score

## Problem Statement

For this assignment, we will focus on the Loss Given Default (LGD) component of the ECL computation. The objective is to build a statistical model to estimate borrowers’ LGD.

As a business analyst working for a bank, you have been tasked with developing a model that can estimate borrowers’ LGD. To develop this model, you have been provided with relevant data sets that include information about defaulted accounts and the amount of money that has been retrieved from them using collaterals and other collection methods. Details about the data sets are provided in subsequent sections. 

Please note that in the real-worls, the LGD model will be used in conjunction with the PD (estimated using an existing PD model) to calculate the ECL. This will provide the bank with a more accurate understanding of the potential losses from its loans, thus allowing it to make more informed decisions about credit risk management and provisioning. The bank will also be able to identify high-risk loans and take appropriate actions to mitigate the risks.

To complete this, you will need to do the following:

  1. Understand the business problem deeply in the context of the current business and domain.
  2. Define your business objective. For this assignment, you need to build a model that can predict the loss given default       (LGD) for defaulted accounts and evaluate it based on the performance metric that will be described in the subsequent        segments.
  3. Thoroughly understand the data sets provided to you and familiarise yourself with the variables in the data set, data        types and data distribution. Ensure that you have a thorough understanding of the target variable, which is the LGD of       the accounts, and how it is calculated. The collection data is provided in a separate data set and needs to be               aggregated and merged to gather relevant information. It is essential to ensure that the data types of the variables         are identified correctly, as Python is notorious for running into errors owing to datatype mismatch errors.
  4. Clean and pre-process the data. This includes handling missing values, outliers and any other issues that may affect         the model's performance. Also, perform any necessary feature engineering or feature extraction to create new variables       that may be useful for the model.
  5. The target variable LGD is not specified directly and, hence, needs to be calculated. Calculate the LGD using the            following formula:
  
  # LGD = (Loan Amount - (Collateral value + Sum of Repayments)) / Loan Amount
  
  The LGD would be represented as a decimal value ranging from 0 to 1. The value represents the proportion of the total loan   amount that is expected to be lost in the event of default. A value of 0 indicates that no loss is expected, whereas a       value of 1 indicates that the entire loan amount is expected to be lost. The collateral value and collected amount through   repayments need to be utilised to calculate this.
  
  6. Use any appropriate statistical or machine learning technique to develop a model for predicting the borrowers’ LGD.
  7. Once the model is built, the next step is to evaluate its performance. For this purpose, you will be provided with a         separate test data set that does not include the repayment data. The collateral value will be provided in this test          data set as well. Run the model on the test data set and submit the predicted LGD values. Submit your workings in the        form of a Jupyter Notebook.
  8. Articulate the model’s implications for the bank's business operations - specifically, its ability to enhance risk           management and compliance with regulatory standards such as Basel norms. Summarise the results of the analysis,              highlighting successes and areas for improvement, as well as potential avenues for further improvisation.

Note that although the scope of this is confined to calculating the LGD only, it would be beneficial to understand how the expected credit loss (ECL) is calculated and used to determine the amount of provisioning required. Understand the role of the probability of default (PD) and the loss given default (LGD) in the ECL calculation.



## Dataset Description

The train_data folder contains three data sets in the form of .csv files titled: main_loan_base.csv, repayment_base.csv, and monthly_balance_base.csv. The main_loan_base data set contains information about loan accounts and other relevant information for the corresponding borrowers. The repayment_base data set contains information about the repayments received by the banks in the form of EMIs or through other collection efforts pertaining to the loan accounts in the lmain_loan_base. The monthly_balance_base contains the information pertaining to the monthly balance statements in the borrower’s accounts.

1. Dataset main_loan_base.csv

The main_loan_base data set contains information about 20,000 loan accounts with a fictitious bank. The dataset also contains other relevant information about the borrowers. The features of the data set are as follows:
 
  loan_acc_num: This is the unique loan account number associated with each loan account.
  customer_name: This is the name of the customer who has taken the loan.
  customer_address: This is the customer’s address.
  loan_type: This is the type of loan that the customer has taken, such as a car loan, two-wheeler loan or personal loan.
  loan_amount: This is the amount of the loan that the customer has taken.
  collateral_value: This is the value of the collateral provided by the customer to secure the loan.
  cheque_bounces: This is the number of cheques that have bounced for the customer in the past few months.
  number_of_loans: This is the total number of loans that the customer has taken.
  missed_repayments: This is the total number of the customer’s missed loan repayments for any loan taken from the bank.                          This would also include any other loans that the customer has had with the bank.
  vintage_in_months: the number of months since the customer has joined the bank.
  tenure_years: This is the total tenure of the loan in years. (Also referred to as loan tenor)
  interest: This is the interest rate at which the loan is provided.
  monthly_emi: This is the monthly installment that the customer needs to pay to repay the loan.
  disbursal_date: This is the date on which the loan was disbursed to the customer.
  default_date: This is the date on which the loan has defaulted on the loan.

2. Dataset repayment_base.csv

The repayment_base dataset contains information about the repayments made by the customers for the loan accounts in the first data set, main_loan_base. It should be expected that accounts without any repayments would not be present in this dataset. It includes the following features:

  loan_acc_num: This is the unique loan account number associated with each loan account.
  repayment_date: This is the date on which the repayment was made.
  repayment_amount: This is the amount of money that was repaid on the repayment date.
 
3. Dataset monthly_balance_base.csv

The monthly_balance_base dataset contains the details of the customer’s monthly bank balance for the duration of the loan. The features in this dataset include:

  loan_acc_num: This is the unique loan account number associated with each loan account.
  date: This is the date on which the monthly bank statement was generated.
  balance_amount: This is the amount of money that was present in the customer’s account on the specified date.

The three datasets can be merged using the loan_acc_num as the common key. The information from these datasets can be combined to get a more complete picture of the loan accounts, including the repayment history for each account.

Caution: When you merge the main_loan_base and repayment_base datasets, it should be noted that not all accounts present in the main_loan_base will have corresponding entries in the repayment_base. This results in the presence of null values in the merged data set, which must be properly handled before you proceed with the calculation of the loss given default (LGD) metric. Failure to address these null values may result in errors during the LGD calculation process.
