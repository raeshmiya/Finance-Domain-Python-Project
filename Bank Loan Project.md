# BANK LOAN ANALYSIS REPORT

### Import Libraries


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
import plotly.express as px
```


```python
df = pd.read_excel("C:/Users/QU561FR/OneDrive - EY/Reference/Personal/Learning/Power BI/Python/financial_loan.xlsx")
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>address_state</th>
      <th>application_type</th>
      <th>emp_length</th>
      <th>emp_title</th>
      <th>grade</th>
      <th>home_ownership</th>
      <th>issue_date</th>
      <th>last_credit_pull_date</th>
      <th>last_payment_date</th>
      <th>...</th>
      <th>sub_grade</th>
      <th>term</th>
      <th>verification_status</th>
      <th>annual_income</th>
      <th>dti</th>
      <th>installment</th>
      <th>int_rate</th>
      <th>loan_amount</th>
      <th>total_acc</th>
      <th>total_payment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1077430</td>
      <td>GA</td>
      <td>INDIVIDUAL</td>
      <td>&lt; 1 year</td>
      <td>Ryder</td>
      <td>C</td>
      <td>RENT</td>
      <td>2021-02-11</td>
      <td>2021-09-13</td>
      <td>2021-04-13</td>
      <td>...</td>
      <td>C4</td>
      <td>60 months</td>
      <td>Source Verified</td>
      <td>30000.0</td>
      <td>0.0100</td>
      <td>59.83</td>
      <td>0.1527</td>
      <td>2500</td>
      <td>4</td>
      <td>1009</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1072053</td>
      <td>CA</td>
      <td>INDIVIDUAL</td>
      <td>9 years</td>
      <td>MKC Accounting</td>
      <td>E</td>
      <td>RENT</td>
      <td>2021-01-01</td>
      <td>2021-12-14</td>
      <td>2021-01-15</td>
      <td>...</td>
      <td>E1</td>
      <td>36 months</td>
      <td>Source Verified</td>
      <td>48000.0</td>
      <td>0.0535</td>
      <td>109.43</td>
      <td>0.1864</td>
      <td>3000</td>
      <td>4</td>
      <td>3939</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1069243</td>
      <td>CA</td>
      <td>INDIVIDUAL</td>
      <td>4 years</td>
      <td>Chemat Technology Inc</td>
      <td>C</td>
      <td>RENT</td>
      <td>2021-01-05</td>
      <td>2021-12-12</td>
      <td>2021-01-09</td>
      <td>...</td>
      <td>C5</td>
      <td>36 months</td>
      <td>Not Verified</td>
      <td>50000.0</td>
      <td>0.2088</td>
      <td>421.65</td>
      <td>0.1596</td>
      <td>12000</td>
      <td>11</td>
      <td>3522</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1041756</td>
      <td>TX</td>
      <td>INDIVIDUAL</td>
      <td>&lt; 1 year</td>
      <td>barnes distribution</td>
      <td>B</td>
      <td>MORTGAGE</td>
      <td>2021-02-25</td>
      <td>2021-12-12</td>
      <td>2021-03-12</td>
      <td>...</td>
      <td>B2</td>
      <td>60 months</td>
      <td>Source Verified</td>
      <td>42000.0</td>
      <td>0.0540</td>
      <td>97.06</td>
      <td>0.1065</td>
      <td>4500</td>
      <td>9</td>
      <td>4911</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1068350</td>
      <td>IL</td>
      <td>INDIVIDUAL</td>
      <td>10+ years</td>
      <td>J&amp;J Steel Inc</td>
      <td>A</td>
      <td>MORTGAGE</td>
      <td>2021-01-01</td>
      <td>2021-12-14</td>
      <td>2021-01-15</td>
      <td>...</td>
      <td>A1</td>
      <td>36 months</td>
      <td>Verified</td>
      <td>83000.0</td>
      <td>0.0231</td>
      <td>106.53</td>
      <td>0.0603</td>
      <td>3500</td>
      <td>28</td>
      <td>3835</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>




```python
df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>address_state</th>
      <th>application_type</th>
      <th>emp_length</th>
      <th>emp_title</th>
      <th>grade</th>
      <th>home_ownership</th>
      <th>issue_date</th>
      <th>last_credit_pull_date</th>
      <th>last_payment_date</th>
      <th>...</th>
      <th>sub_grade</th>
      <th>term</th>
      <th>verification_status</th>
      <th>annual_income</th>
      <th>dti</th>
      <th>installment</th>
      <th>int_rate</th>
      <th>loan_amount</th>
      <th>total_acc</th>
      <th>total_payment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>38571</th>
      <td>803452</td>
      <td>NJ</td>
      <td>INDIVIDUAL</td>
      <td>&lt; 1 year</td>
      <td>Joseph M Sanzari Company</td>
      <td>C</td>
      <td>MORTGAGE</td>
      <td>2021-07-11</td>
      <td>2021-05-16</td>
      <td>2021-05-16</td>
      <td>...</td>
      <td>C1</td>
      <td>60 months</td>
      <td>Verified</td>
      <td>100000.0</td>
      <td>0.1986</td>
      <td>551.64</td>
      <td>0.1299</td>
      <td>24250</td>
      <td>33</td>
      <td>31946</td>
    </tr>
    <tr>
      <th>38572</th>
      <td>970377</td>
      <td>NY</td>
      <td>INDIVIDUAL</td>
      <td>8 years</td>
      <td>Swat Fame</td>
      <td>C</td>
      <td>RENT</td>
      <td>2021-10-11</td>
      <td>2021-04-16</td>
      <td>2021-05-16</td>
      <td>...</td>
      <td>C1</td>
      <td>60 months</td>
      <td>Verified</td>
      <td>50000.0</td>
      <td>0.0458</td>
      <td>579.72</td>
      <td>0.1349</td>
      <td>25200</td>
      <td>18</td>
      <td>31870</td>
    </tr>
    <tr>
      <th>38573</th>
      <td>875376</td>
      <td>CA</td>
      <td>INDIVIDUAL</td>
      <td>5 years</td>
      <td>Anaheim Regional Medical Center</td>
      <td>D</td>
      <td>RENT</td>
      <td>2021-09-11</td>
      <td>2021-05-16</td>
      <td>2021-05-16</td>
      <td>...</td>
      <td>D5</td>
      <td>60 months</td>
      <td>Verified</td>
      <td>65000.0</td>
      <td>0.1734</td>
      <td>627.93</td>
      <td>0.1749</td>
      <td>25000</td>
      <td>20</td>
      <td>35721</td>
    </tr>
    <tr>
      <th>38574</th>
      <td>972997</td>
      <td>NY</td>
      <td>INDIVIDUAL</td>
      <td>5 years</td>
      <td>Brooklyn Radiology</td>
      <td>D</td>
      <td>RENT</td>
      <td>2021-10-11</td>
      <td>2021-05-16</td>
      <td>2021-05-16</td>
      <td>...</td>
      <td>D5</td>
      <td>60 months</td>
      <td>Verified</td>
      <td>368000.0</td>
      <td>0.0009</td>
      <td>612.72</td>
      <td>0.1825</td>
      <td>24000</td>
      <td>9</td>
      <td>33677</td>
    </tr>
    <tr>
      <th>38575</th>
      <td>682952</td>
      <td>NY</td>
      <td>INDIVIDUAL</td>
      <td>4 years</td>
      <td>Allen Edmonds</td>
      <td>F</td>
      <td>RENT</td>
      <td>2021-07-11</td>
      <td>2021-05-16</td>
      <td>2021-05-16</td>
      <td>...</td>
      <td>F3</td>
      <td>60 months</td>
      <td>Verified</td>
      <td>80000.0</td>
      <td>0.0600</td>
      <td>486.86</td>
      <td>0.2099</td>
      <td>18000</td>
      <td>7</td>
      <td>27679</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>



### Metadata of data


```python
print("No. of rows:", df.shape[0])
```

    No. of rows: 38576
    


```python
print("No. of columns:", df.shape[1])
```

    No. of columns: 24
    


```python
df.info
```




    <bound method DataFrame.info of             id address_state application_type emp_length  \
    0      1077430            GA       INDIVIDUAL   < 1 year   
    1      1072053            CA       INDIVIDUAL    9 years   
    2      1069243            CA       INDIVIDUAL    4 years   
    3      1041756            TX       INDIVIDUAL   < 1 year   
    4      1068350            IL       INDIVIDUAL  10+ years   
    ...        ...           ...              ...        ...   
    38571   803452            NJ       INDIVIDUAL   < 1 year   
    38572   970377            NY       INDIVIDUAL    8 years   
    38573   875376            CA       INDIVIDUAL    5 years   
    38574   972997            NY       INDIVIDUAL    5 years   
    38575   682952            NY       INDIVIDUAL    4 years   
    
                                 emp_title grade home_ownership issue_date  \
    0                                Ryder     C           RENT 2021-02-11   
    1                       MKC Accounting     E           RENT 2021-01-01   
    2                Chemat Technology Inc     C           RENT 2021-01-05   
    3                  barnes distribution     B       MORTGAGE 2021-02-25   
    4                        J&J Steel Inc     A       MORTGAGE 2021-01-01   
    ...                                ...   ...            ...        ...   
    38571         Joseph M Sanzari Company     C       MORTGAGE 2021-07-11   
    38572                        Swat Fame     C           RENT 2021-10-11   
    38573  Anaheim Regional Medical Center     D           RENT 2021-09-11   
    38574               Brooklyn Radiology     D           RENT 2021-10-11   
    38575                    Allen Edmonds     F           RENT 2021-07-11   
    
          last_credit_pull_date last_payment_date  ... sub_grade        term  \
    0                2021-09-13        2021-04-13  ...        C4   60 months   
    1                2021-12-14        2021-01-15  ...        E1   36 months   
    2                2021-12-12        2021-01-09  ...        C5   36 months   
    3                2021-12-12        2021-03-12  ...        B2   60 months   
    4                2021-12-14        2021-01-15  ...        A1   36 months   
    ...                     ...               ...  ...       ...         ...   
    38571            2021-05-16        2021-05-16  ...        C1   60 months   
    38572            2021-04-16        2021-05-16  ...        C1   60 months   
    38573            2021-05-16        2021-05-16  ...        D5   60 months   
    38574            2021-05-16        2021-05-16  ...        D5   60 months   
    38575            2021-05-16        2021-05-16  ...        F3   60 months   
    
           verification_status annual_income     dti installment int_rate  \
    0          Source Verified       30000.0  0.0100       59.83   0.1527   
    1          Source Verified       48000.0  0.0535      109.43   0.1864   
    2             Not Verified       50000.0  0.2088      421.65   0.1596   
    3          Source Verified       42000.0  0.0540       97.06   0.1065   
    4                 Verified       83000.0  0.0231      106.53   0.0603   
    ...                    ...           ...     ...         ...      ...   
    38571             Verified      100000.0  0.1986      551.64   0.1299   
    38572             Verified       50000.0  0.0458      579.72   0.1349   
    38573             Verified       65000.0  0.1734      627.93   0.1749   
    38574             Verified      368000.0  0.0009      612.72   0.1825   
    38575             Verified       80000.0  0.0600      486.86   0.2099   
    
           loan_amount  total_acc  total_payment  
    0             2500          4           1009  
    1             3000          4           3939  
    2            12000         11           3522  
    3             4500          9           4911  
    4             3500         28           3835  
    ...            ...        ...            ...  
    38571        24250         33          31946  
    38572        25200         18          31870  
    38573        25000         20          35721  
    38574        24000          9          33677  
    38575        18000          7          27679  
    
    [38576 rows x 24 columns]>



### Data types


```python
df.dtypes
```




    id                                int64
    address_state                    object
    application_type                 object
    emp_length                       object
    emp_title                        object
    grade                            object
    home_ownership                   object
    issue_date               datetime64[ns]
    last_credit_pull_date    datetime64[ns]
    last_payment_date        datetime64[ns]
    loan_status                      object
    next_payment_date        datetime64[ns]
    member_id                         int64
    purpose                          object
    sub_grade                        object
    term                             object
    verification_status              object
    annual_income                   float64
    dti                             float64
    installment                     float64
    int_rate                        float64
    loan_amount                       int64
    total_acc                         int64
    total_payment                     int64
    dtype: object




```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>issue_date</th>
      <th>last_credit_pull_date</th>
      <th>last_payment_date</th>
      <th>next_payment_date</th>
      <th>member_id</th>
      <th>annual_income</th>
      <th>dti</th>
      <th>installment</th>
      <th>int_rate</th>
      <th>loan_amount</th>
      <th>total_acc</th>
      <th>total_payment</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>3.857600e+04</td>
      <td>38576</td>
      <td>38576</td>
      <td>38576</td>
      <td>38576</td>
      <td>3.857600e+04</td>
      <td>3.857600e+04</td>
      <td>38576.000000</td>
      <td>38576.000000</td>
      <td>38576.000000</td>
      <td>38576.000000</td>
      <td>38576.000000</td>
      <td>38576.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>6.810371e+05</td>
      <td>2021-07-16 02:31:35.562007040</td>
      <td>2021-06-08 13:36:34.193280512</td>
      <td>2021-06-26 09:52:08.909166080</td>
      <td>2021-07-26 20:42:20.605557760</td>
      <td>8.476515e+05</td>
      <td>6.964454e+04</td>
      <td>0.133274</td>
      <td>326.862965</td>
      <td>0.120488</td>
      <td>11296.066855</td>
      <td>22.132544</td>
      <td>12263.348533</td>
    </tr>
    <tr>
      <th>min</th>
      <td>5.473400e+04</td>
      <td>2021-01-01 00:00:00</td>
      <td>2021-01-08 00:00:00</td>
      <td>2021-01-08 00:00:00</td>
      <td>2021-02-08 00:00:00</td>
      <td>7.069900e+04</td>
      <td>4.000000e+03</td>
      <td>0.000000</td>
      <td>15.690000</td>
      <td>0.054200</td>
      <td>500.000000</td>
      <td>2.000000</td>
      <td>34.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>5.135170e+05</td>
      <td>2021-04-11 00:00:00</td>
      <td>2021-04-15 00:00:00</td>
      <td>2021-03-16 00:00:00</td>
      <td>2021-04-16 00:00:00</td>
      <td>6.629788e+05</td>
      <td>4.150000e+04</td>
      <td>0.082100</td>
      <td>168.450000</td>
      <td>0.093200</td>
      <td>5500.000000</td>
      <td>14.000000</td>
      <td>5633.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>6.627280e+05</td>
      <td>2021-07-11 00:00:00</td>
      <td>2021-05-16 00:00:00</td>
      <td>2021-06-14 00:00:00</td>
      <td>2021-07-14 00:00:00</td>
      <td>8.473565e+05</td>
      <td>6.000000e+04</td>
      <td>0.134200</td>
      <td>283.045000</td>
      <td>0.118600</td>
      <td>10000.000000</td>
      <td>20.000000</td>
      <td>10042.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>8.365060e+05</td>
      <td>2021-10-11 00:00:00</td>
      <td>2021-08-13 00:00:00</td>
      <td>2021-09-15 00:00:00</td>
      <td>2021-10-15 00:00:00</td>
      <td>1.045652e+06</td>
      <td>8.320050e+04</td>
      <td>0.185900</td>
      <td>434.442500</td>
      <td>0.145900</td>
      <td>15000.000000</td>
      <td>29.000000</td>
      <td>16658.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.077501e+06</td>
      <td>2021-12-12 00:00:00</td>
      <td>2022-01-20 00:00:00</td>
      <td>2021-12-15 00:00:00</td>
      <td>2022-01-15 00:00:00</td>
      <td>1.314167e+06</td>
      <td>6.000000e+06</td>
      <td>0.299900</td>
      <td>1305.190000</td>
      <td>0.245900</td>
      <td>35000.000000</td>
      <td>90.000000</td>
      <td>58564.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2.113246e+05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.668105e+05</td>
      <td>6.429368e+04</td>
      <td>0.066662</td>
      <td>209.092000</td>
      <td>0.037164</td>
      <td>7460.746022</td>
      <td>11.392282</td>
      <td>9051.104777</td>
    </tr>
  </tbody>
</table>
</div>



### Total Loan Applications


```python
total_loan_application = df['id'].count()
print("Total Loan Applications:",total_loan_application)
```

    Total Loan Applications: 38576
    

### MTD Total Loan Applications



```python
latest_issue_date = df['issue_date'].max()
latest_year =  latest_issue_date.year
latest_month = latest_issue_date.month

mtd_data = df[(df['issue_date'].dt.year == latest_year) & (df['issue_date'].dt.month == latest_month)]

mtd_total_loan_applications = mtd_data['id'].count()

print(f"MTD Loan Applications (for {latest_issue_date.strftime('%B %Y')}): {mtd_total_loan_applications}")
```

    MTD Loan Applications (for December 2021): 4314
    

### Total Funded Amount


```python
total_funded_amount = df['loan_amount'].sum()
total_funded_amount_millions = total_funded_amount / 1000000
print("Total Funded Amount: ${:.2f}M".format(total_funded_amount_millions))
```

    Total Funded Amount: $435.76M
    

### MTD Total Funded Amount


```python
latest_issue_date = df['issue_date'].max()
latest_year =  latest_issue_date.year
latest_month = latest_issue_date.month

mtd_data = df[(df['issue_date'].dt.year == latest_year) & (df['issue_date'].dt.month == latest_month)]

mtd_total_funded_amount = mtd_data['loan_amount'].sum()
mtd_total_funded_amount_millions = mtd_total_funded_amount/ 1000000

print("MTD Total Funded Amount: ${:.2f}M".format(mtd_total_funded_amount_millions))
```

    MTD Total Funded Amount: $53.98M
    

### Total Amount Received


```python
total_amount_received = df['total_payment'].sum()
total_amount_received_millions = total_funded_amount / 1000000
print("Total Funded Amount: ${:.2f}M".format(total_amount_received_millions))
```

    Total Funded Amount: $435.76M
    

### MTD Total Amount Received


```python
latest_issue_date = df['issue_date'].max()
latest_year =  latest_issue_date.year
latest_month = latest_issue_date.month

mtd_data = df[(df['issue_date'].dt.year == latest_year) & (df['issue_date'].dt.month == latest_month)]

mtd_total_amount_received = mtd_data['total_payment'].sum()
mtd_total_amount_received_millions = mtd_total_amount_received/ 1000000

print("MTD Total Amount Received: ${:.2f}M".format(mtd_total_amount_received_millions))
```

    MTD Total Amount Received: $58.07M
    

### Average Interest Rate


```python
average_interest_Rate = df['int_rate'].mean()*100
print("Average Interest Rate:{:.2f}%".format(average_interest_Rate))
```

    Average Interest Rate:12.05%
    

### Average Debt-to-Income Ratio (DTI)


```python
average_dti = df['dti'].mean()*100
print("Average DTI:{:.2f}%".format(average_dti))
```

    Average DTI:13.33%
    

### Good Loan Metrics


```python
good_loans = df[df['loan_status'].isin(["Fully Paid","Current"])]  # good loans

total_loan_applications = df['id'].count()

good_loan_applications = good_loans['id'].count()
good_loan_funded_amount = good_loans['loan_amount'].sum()
good_loan_received = good_loans['total_payment'].sum()

good_loan_funded_amount_millions = good_loan_funded_amount / 1000000
good_loan_received_millions = good_loan_received / 1000000

good_loan_percentage = (good_loan_applications / total_loan_applications) *100

print("Good Loan Applications:",good_loan_applications)
print("Good Loan Funded Amount (in Millions): ${:.2f}M".format(good_loan_funded_amount_millions))
print("Good Loan Received Amount (in Millions): ${:.2f}M".format(good_loan_received_millions))
print("Percentage of Good Loan Applications: ${:.2f}%".format(good_loan_percentage))
```

    Good Loan Applications: 33243
    Good Loan Funded Amount (in Millions): $370.22M
    Good Loan Received Amount (in Millions): $435.79M
    Percentage of Good Loan Applications: $86.18%
    

### Bad Loan Metrics


```python
bad_loans = df[df['loan_status'].isin(["Charged Off"])]  # bad loans

total_loan_applications = df['id'].count()

bad_loan_applications = bad_loans['id'].count()
bad_loan_funded_amount = bad_loans['loan_amount'].sum()
bad_loan_received = bad_loans['total_payment'].sum()

bad_loan_funded_amount_millions = bad_loan_funded_amount / 1000000
bad_loan_received_millions = bad_loan_received / 1000000

bad_loan_percentage = (bad_loan_applications / total_loan_applications) *100

print("Bad Loan Applications:",bad_loan_applications)
print("Bad Loan Funded Amount (in Millions): ${:.2f}M".format(bad_loan_funded_amount_millions))
print("Bad Loan Received Amount (in Millions): ${:.2f}M".format(bad_loan_received_millions))
print("Percentage of Bad Loan Applications: ${:.2f}%".format(bad_loan_percentage))
```

    Bad Loan Applications: 5333
    Bad Loan Funded Amount (in Millions): $65.53M
    Bad Loan Received Amount (in Millions): $37.28M
    Percentage of Bad Loan Applications: $13.82%
    

### Monthly Trends by Issue Date for Total Funded Amount


```python
monthly_funded = (
    df.sort_values('issue_date')
    .assign(month_name=lambda x: x['issue_date'].dt.strftime('%b %Y'))
    .groupby('month_name', sort=False)['loan_amount']
    .sum()
    .div(1000000)
    .reset_index(name='loan_amount_millions')
)

fig, ax = plt.subplots(figsize=(10, 6), layout='constrained') 

ax.fill_between(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], color='green', alpha=0.5)
ax.plot(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], color='green', linewidth=2)

# Place labels relative to the data points - this block is indented
for i, row in monthly_funded.iterrows():
    ax.text(i, row['loan_amount_millions'] + 0.1, 
            f"{row['loan_amount_millions']:.2f}",
            ha='center', va='bottom', fontsize=9, rotation=0, color='black')

# These lines MUST be aligned with the ax.fill_between line above, NOT inside the for loop
ax.set_title('Total Funded Amount by Month', fontsize=14)
ax.set_xlabel('Month')
ax.set_ylabel('Funded Amount ($ Millions)')
ax.set_xticks(ticks=range(len(monthly_funded)), labels=monthly_funded['month_name'], rotation=45, ha='right')
ax.grid(True, linestyle='--', alpha=0.6)

plt.show()
```


    
![png](output_34_0.png)
    


### Monthly Trends by Issue Date for Total Amount Received


```python
monthly_received = (
    df.sort_values('issue_date')
    .assign(month_name=lambda x: x['issue_date'].dt.strftime('%b %Y'))
    .groupby('month_name', sort=False)['total_payment']
    .sum()
    .div(1000000)
    .reset_index(name='received_amount_millions')
)

fig, ax = plt.subplots(figsize=(10, 6), layout='constrained') 

ax.fill_between(monthly_received['month_name'], monthly_received['received_amount_millions'], color='green', alpha=0.5)
ax.plot(monthly_received['month_name'], monthly_received['received_amount_millions'], color='green', linewidth=2)

# Place labels relative to the data points - this block is indented
for i, row in monthly_received.iterrows():
    ax.text(i, row['received_amount_millions'] + 0.1, 
            f"{row['received_amount_millions']:.2f}",
            ha='center', va='bottom', fontsize=9, rotation=0, color='black')

# These lines MUST be aligned with the ax.fill_between line above, NOT inside the for loop
ax.set_title('Total Received Amount by Month', fontsize=14)
ax.set_xlabel('Month')
ax.set_ylabel('Received Amount ($ Millions)')
ax.set_xticks(ticks=range(len(monthly_received)), labels=monthly_received['month_name'], rotation=45, ha='right')
ax.grid(True, linestyle='--', alpha=0.6)

plt.show()
```


    
![png](output_36_0.png)
    


### Monthly Trends by Issue Date for Total Loan Applications


```python
monthly_applications = (
    df.sort_values('issue_date')
    .assign(month_name=lambda x: x['issue_date'].dt.strftime('%b %Y'))
    .groupby('month_name', sort=False)['total_payment']
    .count()
    .reset_index(name='loan_applications_count')
)

fig, ax = plt.subplots(figsize=(10, 6), layout='constrained') 

ax.fill_between(monthly_applications['month_name'], monthly_applications['loan_applications_count'], color='orange', alpha=0.5)
ax.plot(monthly_applications['month_name'], monthly_applications['loan_applications_count'], color='darkorange', linewidth=2)

# Place labels relative to the data points - this block is indented
for i, row in monthly_applications.iterrows():
    ax.text(i, row['loan_applications_count'] + 0.1, 
            f"{row['loan_applications_count']:.2f}",
            ha='center', va='bottom', fontsize=9, rotation=0, color='black')

# These lines MUST be aligned with the ax.fill_between line above, NOT inside the for loop
ax.set_title('Total Loan Applications by Month', fontsize=14)
ax.set_xlabel('Month')
ax.set_ylabel('Number of Applications')
ax.set_xticks(ticks=range(len(monthly_applications)), labels=monthly_applications['month_name'], rotation=45, ha='right')
ax.grid(True, linestyle='--', alpha=0.6)

plt.show()
```


    
![png](output_38_0.png)
    


### Regional Analysis by State for Total Funded Amount


```python
# Calculate total loan amount per state and sort
state_funding = df.groupby('address_state')['loan_amount'].sum().sort_values(ascending=True)
state_funding_thousands = state_funding / 1000

# Create the figure and axes for the plot
plt.figure(figsize=(10, 8))
bars = plt.barh(state_funding_thousands.index, state_funding_thousands.values, color='lightcoral')

# Add data labels to each bar
for bar in bars:
    # Get the width of the bar (which is the data value)
    width = bar.get_width()
    # Position the text slightly to the right of the bar's end
    # Use formatted string to show value with a K for thousands
    plt.text(width + 10, bar.get_y() + bar.get_height() / 2,
             f'{width:,.0f}K',
             va='center', fontsize=9)

# Set the title and axis labels
plt.title('Total Funded Amount by State (in ₹ Thousands)')
plt.xlabel('Funded Amount (₹\'000)')
plt.ylabel('State')

# Adjust plot layout
plt.tight_layout()
plt.show()
```


    
![png](output_40_0.png)
    


### Regional Analysis by State for Total Received Amount


```python
# Calculate total payment per state and sort
state_receiving = df.groupby('address_state')['total_payment'].sum().sort_values(ascending=True)
state_receiving_thousands = state_receiving / 1000

# Create the figure and axes for the plot
plt.figure(figsize=(10, 8))
bars = plt.barh(state_receiving_thousands.index, state_receiving_thousands.values, color='lightblue')

# Add data labels to each bar
for bar in bars:
    # Get the width of the bar (which is the data value)
    width = bar.get_width()
    # Position the text slightly to the right of the bar's end
    # Use formatted string to show value with a K for thousands
    plt.text(width + 10, bar.get_y() + bar.get_height() / 2,
             f'{width:,.0f}K',
             va='center', fontsize=9)

# Set the title and axis labels
plt.title('Total Received Amount by State (in ₹ Thousands)')
plt.xlabel('Received Amount (₹\'000)')
plt.ylabel('State')

# Adjust plot layout
plt.tight_layout()
plt.show()
```


    
![png](output_42_0.png)
    


### Loan Term Analysis by Total Funded Amount


```python
term_funding_millions = df.groupby('term')['loan_amount'].sum() / 1000000

# Create the figure and a square plot area for the pie chart
plt.figure(figsize=(5, 5))

# Plot the pie chart. The autopct lambda function has been corrected.
plt.pie(
    term_funding_millions,
    labels=term_funding_millions.index,
    autopct=lambda p: f"{p:.1f}%\n${p*sum(term_funding_millions)/100:.1f}M",
    startangle=90,
    wedgeprops={'width': 0.4}
)

# Add a white circle in the center to create the donut shape.
# `gca()` gets the current axes, and `add_artist()` adds the circle to it.
plt.gca().add_artist(plt.Circle((0, 0), 0.70, color='white'))

# Set the title and show the plot.
plt.title("Total Funded Amount by Term (in $ Millions)")
plt.show()
```


    
![png](output_44_0.png)
    


### Loan Term Analysis by Total Received Amount


```python
term_receiving_millions = df.groupby('term')['total_payment'].sum() / 1000000

# Create the figure and a square plot area for the pie chart
plt.figure(figsize=(5, 5))

# Plot the pie chart. The autopct lambda function has been corrected.
plt.pie(
    term_receiving_millions,
    labels=term_receiving_millions.index,
    autopct=lambda p: f"{p:.1f}%\n${p*sum(term_receiving_millions)/100:.1f}M",
    startangle=90,
    wedgeprops={'width': 0.4}
)

# Add a white circle in the center to create the donut shape.
# `gca()` gets the current axes, and `add_artist()` adds the circle to it.
plt.gca().add_artist(plt.Circle((0, 0), 0.70, color='white'))

# Set the title and show the plot.
plt.title("Total Received Amount by Term (in $ Millions)")
plt.show()
```


    
![png](output_46_0.png)
    


### Loan Term Analysis by Total Loan Applications


```python
term_applications_received = df.groupby('term')['id'].count()

# Create the figure and a square plot area for the pie chart
plt.figure(figsize=(5, 5))

# Plot the pie chart. The autopct lambda function has been corrected.
plt.pie(
    term_applications_received,
    labels=term_applications_received.index,
    autopct=lambda p: f"{p:.1f}%\n${p*sum(term_applications_received)/100:.1f}",
    startangle=90,
    wedgeprops={'width': 0.4}
)

# Add a white circle in the center to create the donut shape.
# `gca()` gets the current axes, and `add_artist()` adds the circle to it.
plt.gca().add_artist(plt.Circle((0, 0), 0.70, color='white'))

# Set the title and show the plot.
plt.title("Total Applications Received by Term (in $ Millions)")
plt.show()
```


    
![png](output_48_0.png)
    


### Employee Length by Total Funded Amount


```python
emp_funding_thousands = df.groupby('emp_length')['loan_amount'].sum().sort_values()/1000

plt.figure(figsize=(10, 6))

bars = plt.barh(emp_funding_thousands.index, emp_funding_thousands, color='purple')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 5, bar.get_y() + bar.get_height() / 2,
             f"{width:,.0f}K", va='center', fontsize=9)

plt.xlabel("Funded Amount (₹ Thousands)")
plt.title("Total Funded Amount by Employment Length")
plt.grid(axis='x', linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()

```


    
![png](output_50_0.png)
    


### Employee Length by Total Received Amount


```python
emp_receiving_thousands = df.groupby('emp_length')['total_payment'].sum().sort_values()/1000

plt.figure(figsize=(10, 6))

bars = plt.barh(emp_receiving_thousands.index, emp_receiving_thousands, color='purple')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 5, bar.get_y() + bar.get_height() / 2,
             f"{width:,.0f}K", va='center', fontsize=9)

plt.xlabel("Received Amount (₹ Thousands)")
plt.title("Total Received Amount by Employment Length")
plt.grid(axis='x', linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()

```


    
![png](output_52_0.png)
    


### Employee Length by Total Loan Applications


```python
emp_applications_thousands = df.groupby('emp_length')['id'].count()

plt.figure(figsize=(10, 6))

bars = plt.barh(emp_applications_thousands.index, emp_applications_thousands, color='gray')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 5, bar.get_y() + bar.get_height() / 2,
             f"{width:,.0f}", va='center', fontsize=9)

plt.xlabel("Loan Applications")
plt.title("Total Loan Applications by Employment Length")
plt.grid(axis='x', linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()
```


    
![png](output_54_0.png)
    


### Loan Purpose by Total Funded Amount


```python
purpose_funding_millions = (df.groupby('purpose')['loan_amount'].sum().sort_values()/ 1000000)

plt.figure(figsize=(10, 6))
bars = plt.barh(purpose_funding_millions.index, purpose_funding_millions.values, color='skyblue')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 0.1, bar.get_y() + bar.get_height()/2,
             f'{width:.2f} M', va='center', fontsize=9)

plt.title('Total Funded Amount by Loan Purpose (₹ Millions)', fontsize=14)
plt.xlabel('Funded Amount (₹ Millions)')
plt.ylabel('Loan Purpose')
plt.grid(axis='x', linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```


    
![png](output_56_0.png)
    


### Loan Purpose by Total Received Amount


```python
purpose_receiving_millions = (df.groupby('purpose')['total_payment'].sum().sort_values()/ 1000000)

plt.figure(figsize=(10, 6))
bars = plt.barh(purpose_receiving_millions.index, purpose_receiving_millions.values, color='darkgreen')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 0.1, bar.get_y() + bar.get_height()/2,
             f'{width:.2f} M', va='center', fontsize=9)

plt.title('Total Received Amount by Loan Purpose (₹ Millions)', fontsize=14)
plt.xlabel('Received Amount (₹ Millions)')
plt.ylabel('Loan Purpose')
plt.grid(axis='x', linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```


    
![png](output_58_0.png)
    


### Loan Purpose by Total Loan Applications


```python
purpose_loan_applications = (df.groupby('purpose')['id']).count()

plt.figure(figsize=(10, 6))
bars = plt.barh(purpose_loan_applications.index, purpose_loan_applications.values, color='darkgreen')

for bar in bars:
    width = bar.get_width()
    plt.text(width + 0.1, bar.get_y() + bar.get_height()/2,
             f'{width:.2f}', va='center', fontsize=9)

plt.title('Total Loan Applications by Loan Purpose', fontsize=14)
plt.xlabel('Loan Applications')
plt.ylabel('Loan Purpose')
plt.grid(axis='x', linestyle='--', alpha=0.6)
plt.tight_layout()
plt.show()
```


    
![png](output_60_0.png)
    


### Home Ownership by Total Funded Amount


```python
home_funding = (
    df.groupby('home_ownership')['loan_amount']
    .sum()
    .sort_values()
    .reset_index(name='loan_amount_millions')
)

fig = px.treemap(
    home_funding,
    path=['home_ownership'],
    values='loan_amount_millions',
    color='loan_amount_millions',
    color_continuous_scale='Blues',
    title='Total Funded Amount by Home Ownership (₹ Millions)'
)

fig.show()
```


    
![png](output_62_0.png)
    


### Home Ownership by Total Received Amount


```python
home_receiving = (
    df.groupby('home_ownership')['total_payment']
    .sum()
    .sort_values()
    .reset_index(name='total_payment_millions')
)

fig = px.treemap(
    home_receiving,
    path=['home_ownership'],
    values='total_payment_millions',
    color='total_payment_millions',
    color_continuous_scale='Blues',
    title='Total Received Amount by Home Ownership (₹ Millions)'
)

fig.show()
```


    
![png](output_64_0.png)
    


### Home Ownership by Total Loan Applications


```python
home_ownership_loan_applications = (
    df.groupby('home_ownership')['id']
    .count()
    .sort_values()
    .reset_index(name='total_loan_applications')
)

fig = px.treemap(
    home_ownership_loan_applications,
    path=['home_ownership'],
    values='total_loan_applications',
    color='total_loan_applications',
    color_continuous_scale='Blues',
    title='Total Loan Applications by Home Ownership (₹ Millions)'
)

fig.show()
```


    
![png](output_66_0.png)
    



```python

```
