# Untitled

![D:\Sreeraj Working Folder\Surya-Logo.gif](.gitbook/assets/0.png)

**IFRS**

**Probability of Default \(PD\) - Rating based Model**

**Functional Specifications**

| **Version** | **Date** | **Prepared By** | **Description** |
| :--- | :--- | :--- | :--- |
| 1.0 | 17-August-2018 | Bharath | Document consists of Flow chart on PD model, input data details i.e. input data and components, PD Calculation method with detailed steps and Output details with illustrations. |
|  |  |  |  |
|  |  |  |  |
|  |  |  |  |

Contents

[Terminology/ Acronyms 4]()

[1. Introduction 5]()

[2. Flow chart 6]()

[3. Input 7]()

[4. PD Estimation – Rating based method 8]()

[4.1 Deriving Default rates 8]()

[4.2 TTC PD Calculation 9]()

[4.3 Calibration of PD to Rating Table 11]()

[5. Deriving PIT PD from TTC PD 12]()

[5.1 Determining Macro-economic variables 12]()

[5.2 Regression technique 13]()

[6. Output 15]()

## Terminology/ Acronyms

Below is a table of definitions of special terms referenced throughout the document:

| **Terminology** | **Definition** |
| :--- | :--- |
| PD | Probability of default \(PD\) is a financial term describing the likelihood of a default over a particular time horizon. It provides an estimate of the likelihood that a borrower will be unable to meet its debt obligations. |
| Default | An obligor will be regarded as defaulted for the purpose of rating model development if the obligor is past due more than 90 days on the respective contractual payment obligations. |
|  TTC | Through the cycle: Risk parameters, such as PD or LGD, are called through the cycle \(TTC\) parameters, when they represent the average estimated value for this risk parameter, over a full economic cycle. TTC parameters are independent of the current macroeconomic situation |
|  PIT | Point in time: Risk parameters, such as PD or LGD, are called point in time \(PIT\) parameters, when they represent the estimated value for a certain fraction of an economic cycle, e.g. one year. PIT parameters are dependent on the current macroeconomic situation. |
| ECL | IFRS 9 defines Expected Credit Loss \(ECL\) as a probability-weighted estimate of credit losses i.e. the present value of all cash shortfalls over the expected life of the financial instrument. |
| Lifetime ECL | IFRS 9 defines Expected Credit Loss \(ECL\) as a probability-weighted estimate of credit losses i.e. the present value of all cash shortfalls over the expected life of a financial instrument |
| 12 month ECL | IFRS 9 defines Expected Credit Loss \(ECL\) as a probability-weighted estimate of credit losses i.e. the present value of all cash shortfalls instrument within the 12 months after the reporting date |

## 1. Introduction

Document consists of

* Flow chart – Complete process of PD calculation
* Input data and components
* PD estimation method with detailed steps
* Output

## 2. Flow chart

**INPUT**

* Five year account data consists of both default and non-default accounts
* Macro-economic factors data
* Ratings and scores mapping table

**Section 5.1**

**Section 5.2**

**Section 4.2**

**Section 6**

**OUTPUT**

* TTC PD term Structure

**Cumulative PDN = 1- \(1- PD12M\) N**

* PIT PD term Structure

Prepared using Scaling factor

* Determining macro-economic variables which affect PD
* Determining the link function between macro factors and PD, which is then used to compute conditional or PIT PD

**Deriving PIT PD from TTC PD**

**Section 4.3**

**Section 4.1**

**Section 3**

* Bucketing of accounts
* Calculation of average score and log-odd ratios for each bucket
* Running a regression between average scores and Log-odd ratios
* Calculation of bucket wise TTC PD using regression equation

**Calibration of PD to Rating table**

* Calculation of Calibrated PD for each rating band using mid-scores.
* Scaling up calibrated PD using average default rate
* Define Year wise historical Default rates
* Average Default rate
* Total Sample Default rate

**Calculation of Through the Cycle PD**

**Deriving Historical Default rates**

**PD Estimation**

## 3. Input

A minimum of last 5 years accounts data which consists of both default and non-default accounts is required for developing this PD model.

The following input data need to be captured:

1. Data

| **Item** | **Note** |
| :--- | :--- |
| Account ID | Account number |
| RATING | Account Rating given by experts as per rating scale |
| RATING YEAR | Year of Rating |
| DEFAULT STATUS | Dummy variable for default accounts as ‘1’ and non-default accounts as ‘0’ |
| DEFAULT YEAR | Year of Default |
| MID SCORE | Mid Score of score band in rating scale that assigned to particular account |
| MACRO ECONOMIC VARIABLES | Various Macro-economic variables can be used as time dependent covariates. There are no limitation on the number of these variables can be used. In general, leading indicators such as Inflation rate, interest rates and bond yields, unemployment rate and employment growth rate, housing price index, consumer price index, average personal income growth rate, growth rate, stock market index, oil price, GDP, money supply etc. are considered. |

1. Mapping Table

| Rating scale and Credit Score Mapping Table is required. | Useful in bucketing of accounts rating wise |
| :--- | :--- |


## 4. PD Estimation – Rating based method

In this rating based method, Rating for an account as of the reporting date is used to estimate marginal PD. Rating for an account is given internally by expert judgments at the bank which is driven by past history of obligors’ financial obligations or credit worthiness.

This approach assumes no rating transition matrix going forward i.e. assumes constant rating for an account throughout the period.

Steps in estimation of Point in Time \(PIT\)[\[1\]]() PD are:

* Deriving Historical Default rates
* Calculating Through the Cycle \(TTC\)[\[2\]]() PD
* Calibration of PD to Rating table
* Deriving PIT PD from TTC PD

### 4.1 Deriving Default rates

Derive Year wise default rates. Default rate is the ratio between the number of default accounts and total number of accounts.

Default Rate =

Illustration: Assuming the last 5 year data as follows,

Default rate - Year Wise

| YEAR | CUSTOMERS | DEFAULTS | Default Rate \(%\) |
| :--- | :--- | :--- | :--- |
| 2013 | 90 | 7 | 7.78% |
| 2014 | 159 | 14 | 8.81% |
| 2015 | 228 | 13 | 5.70% |
| 2016 | 276 | 29 | 10.51% |
| 2017 | 266 | 31 | 11.65% |
|  | **1019** | **94** | **Average Default rate = 7.41%** |

| Sample Default Rate | = \(94/1019\) | 9.22% |
| :--- | :--- | :--- |
| Average Default Rate | = | 7.41% |
| St. dev. of Default Rate | = | 4.18% |

### 4.2 TTC PD Calculation

The following steps are involved in TTC PD Calculation:

* **Step 1**: Bucketing of accounts.

Bucketing should be based on the rating of customers.

**Illustration**: Assumed a rating scale and data for illustration purposes throughout the document.

Bucketing could be done by grouping similar rating bands as shows below.

| Rating | Bucket | Upper bound of credit score |
| :--- | :--- | :--- |
| **1** | 1 | 100.000 |
| **2+** | 2 | 94.700 |
| **2** | 89.500 |  |
| **2-** | 84.200 |  |
| **3+** | 3 | 78.900 |
| **3** | 73.700 |  |
| **3-** | 68.400 |  |
| **4+** | 4 | 63.200 |
| **4** | 57.900 |  |
| **4-** | 52.600 |  |
| **5+** | 5 | 47.400 |
| **5** | 42.100 |  |
| **5-** | 36.800 |  |
| **6+** | 6 | 31.600 |
| **6** | 26.300 |  |
| **6-** | 21.100 |  |
| **7+** | 7 | 15.800 |
| **7** | 10.500 |  |
| **7-** | 5.300 |  |

* **Step 2**: Calculate average Credit score for each bucket.
* **Step 3:** Calculate adjusted default rate for each bucket.

**Adjusted Default rate = Number of defaults / \(Number of defaults + \(Number of total accounts-Number of defaults\) x Adjustment factor\)**

Adjustment factor =

For any rating band, if the Adjusted Default rate is zero, then take the average of above two ratings’ adjusted default rates.

**Illustration:**

Adjustment factor = = 1.27

* **Step 4:** Calculation of Log-odds ratio for each bucket.

In present case,

**Log-odds \(z\) = ln \(Adjusted Default rate / \(1- Adjusted Default rate\)\)**

* **Step 5:** Run a linear regression between Log-odds as ‘dependent variable’ and scores as ‘independent variable’.

**Z = Coefficient x \(Score\) + intercept**

* **Step 6:** Calculate PD for each bucket using the Z values of each bucket.

**PD = 1 / \(1+e-z\)**

**Illustration:** All the above steps are performed on assumed data and illustrated in the table below,

|  | _Coefficients_ |
| :--- | :--- |
| Intercept | 0.028331 |
| X Variable \(i.e. Score\) | -0.06848 |

**Z = 0.0285 – 0.06848 x Score**

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| New Bucket \(Step 1\) | Average Score \(Step 2\) | No. of Customers | defaults | Default Rate | Adj. DR \(Step 3\) | Log-odds \(Step 4\) | PD \(TTC\) \(Step 6\) |
|  |  |  |  | = 3 ÷ 4 |  | = ln \(6/\(1-6\)\) | = 1/\(1+e-z\) |
| 1 | 97.35 | 0 | 0 | 0.00% | 0.03% | -8.111 | 0.13% |
| 2 | 84.56 | 37 | 0 | 0.00% | 0.93% | -4.673 | 0.31% |
| 3 | 71.72 | 304 | 7 | 2.30% | 1.82% | -3.987 | 0.75% |
| 4 | 55.93 | 293 | 8 | 2.73% | 2.16% | -3.812 | 2.18% |
| 5 | 40.90 | 158 | 10 | 6.33% | 5.05% | -2.934 | 5.88% |
| 6 | 24.27 | 101 | 17 | 16.83% | 13.74% | -1.837 | 16.33% |
| 7 | 7.03 | 126 | 52 | 41.27% | 35.62% | -0.592 | 38.87% |
| Total |  | 1019 | 94 |  |  |  |  |

### 4.3 Calibration of PD to Rating Table

**Step 1:** Calculate PD for each rating band using mid-score \(mid-point of each score band\) as independent variable in linear regression function.

**Step 2:** These calibrated PDs should be scaled up using average calibrated PD and average default rate of data.

**Scaled PD = \(Calibrated PD** ÷ **Average Calibrated PD\) x Average Default rate**

**Illustration:**

For Rating band 1, Scaled PD = \(0.13% / 8.33%\) x 7.41%\) = 0.12%

<table>
  <thead>
    <tr>
      <th style="text-align:left">1</th>
      <th style="text-align:left">2</th>
      <th style="text-align:left">3</th>
      <th style="text-align:left">4</th>
      <th style="text-align:left">5</th>
      <th style="text-align:left">6</th>
      <th style="text-align:left">7</th>
      <th style="text-align:left">8</th>
      <th style="text-align:left">9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Rating</td>
      <td style="text-align:left">Calibration bucket</td>
      <td style="text-align:left">Upper bound</td>
      <td style="text-align:left">Mid-point</td>
      <td style="text-align:left">No. of borrowers</td>
      <td style="text-align:left">No. of defaults</td>
      <td style="text-align:left">Observed DR</td>
      <td style="text-align:left">Calibrated PD</td>
      <td style="text-align:left">Scaled PD (TTC)</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">= 5 &#xF7; 6</td>
      <td style="text-align:left">= 1/(1+e-z)</td>
      <td style="text-align:left">= (Calibrated PD &#xF7; Average calibrated PD) x Average Default rate</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>1</b>
      </td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">100.000</td>
      <td style="text-align:left">97.350</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">0.00%</td>
      <td style="text-align:left">0.13%</td>
      <td style="text-align:left">0.12%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>2+</b>
      </td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">94.700</td>
      <td style="text-align:left">92.100</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">0.00%</td>
      <td style="text-align:left">0.19%</td>
      <td style="text-align:left">0.17%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>2</b>
      </td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">89.500</td>
      <td style="text-align:left">86.850</td>
      <td style="text-align:left">19</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">0.00%</td>
      <td style="text-align:left">0.27%</td>
      <td style="text-align:left">0.24%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>2-</b>
      </td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">84.200</td>
      <td style="text-align:left">81.550</td>
      <td style="text-align:left">17</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">0.00%</td>
      <td style="text-align:left">0.38%</td>
      <td style="text-align:left">0.34%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>3+</b>
      </td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">78.900</td>
      <td style="text-align:left">76.300</td>
      <td style="text-align:left">124</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">0.81%</td>
      <td style="text-align:left">0.55%</td>
      <td style="text-align:left">0.49%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>3</b>
      </td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">73.700</td>
      <td style="text-align:left">71.050</td>
      <td style="text-align:left">95</td>
      <td style="text-align:left">6</td>
      <td style="text-align:left">6.32%</td>
      <td style="text-align:left">0.79%</td>
      <td style="text-align:left">0.70%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>3-</b>
      </td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">68.400</td>
      <td style="text-align:left">65.800</td>
      <td style="text-align:left">85</td>
      <td style="text-align:left">0</td>
      <td style="text-align:left">0.00%</td>
      <td style="text-align:left">1.12%</td>
      <td style="text-align:left">1.00%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>4+</b>
      </td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">63.200</td>
      <td style="text-align:left">60.550</td>
      <td style="text-align:left">103</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">1.94%</td>
      <td style="text-align:left">1.60%</td>
      <td style="text-align:left">1.42%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>4</b>
      </td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">57.900</td>
      <td style="text-align:left">55.250</td>
      <td style="text-align:left">124</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">4.03%</td>
      <td style="text-align:left">2.29%</td>
      <td style="text-align:left">2.03%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>4-</b>
      </td>
      <td style="text-align:left">4</td>
      <td style="text-align:left">52.600</td>
      <td style="text-align:left">50.000</td>
      <td style="text-align:left">66</td>
      <td style="text-align:left">1</td>
      <td style="text-align:left">1.52%</td>
      <td style="text-align:left">3.24%</td>
      <td style="text-align:left">2.88%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>5+</b>
      </td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">47.400</td>
      <td style="text-align:left">44.750</td>
      <td style="text-align:left">73</td>
      <td style="text-align:left">2</td>
      <td style="text-align:left">2.74%</td>
      <td style="text-align:left">4.58%</td>
      <td style="text-align:left">4.08%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>5</b>
      </td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">42.100</td>
      <td style="text-align:left">39.450</td>
      <td style="text-align:left">55</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">9.09%</td>
      <td style="text-align:left">6.46%</td>
      <td style="text-align:left">5.74%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>5-</b>
      </td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">36.800</td>
      <td style="text-align:left">34.200</td>
      <td style="text-align:left">30</td>
      <td style="text-align:left">3</td>
      <td style="text-align:left">10.00%</td>
      <td style="text-align:left">9.00%</td>
      <td style="text-align:left">8.01%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>6+</b>
      </td>
      <td style="text-align:left">6</td>
      <td style="text-align:left">31.600</td>
      <td style="text-align:left">28.950</td>
      <td style="text-align:left">39</td>
      <td style="text-align:left">7</td>
      <td style="text-align:left">17.95%</td>
      <td style="text-align:left">12.41%</td>
      <td style="text-align:left">11.04%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>6</b>
      </td>
      <td style="text-align:left">6</td>
      <td style="text-align:left">26.300</td>
      <td style="text-align:left">23.700</td>
      <td style="text-align:left">34</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">14.71%</td>
      <td style="text-align:left">16.87%</td>
      <td style="text-align:left">15.01%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>6-</b>
      </td>
      <td style="text-align:left">6</td>
      <td style="text-align:left">21.100</td>
      <td style="text-align:left">18.450</td>
      <td style="text-align:left">28</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">17.86%</td>
      <td style="text-align:left">22.53%</td>
      <td style="text-align:left">20.04%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>7+</b>
      </td>
      <td style="text-align:left">7</td>
      <td style="text-align:left">15.800</td>
      <td style="text-align:left">13.150</td>
      <td style="text-align:left">29</td>
      <td style="text-align:left">5</td>
      <td style="text-align:left">17.24%</td>
      <td style="text-align:left">29.48%</td>
      <td style="text-align:left">26.23%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>7</b>
      </td>
      <td style="text-align:left">7</td>
      <td style="text-align:left">10.500</td>
      <td style="text-align:left">7.900</td>
      <td style="text-align:left">47</td>
      <td style="text-align:left">16</td>
      <td style="text-align:left">34.04%</td>
      <td style="text-align:left">37.46%</td>
      <td style="text-align:left">33.32%</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>7-</b>
      </td>
      <td style="text-align:left">7</td>
      <td style="text-align:left">5.300</td>
      <td style="text-align:left">2.650</td>
      <td style="text-align:left">50</td>
      <td style="text-align:left">31</td>
      <td style="text-align:left">62.00%</td>
      <td style="text-align:left">46.18%</td>
      <td style="text-align:left">41.08%</td>
    </tr>
    <tr>
      <td style="text-align:left">Total</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left">1019</td>
      <td style="text-align:left">94</td>
      <td style="text-align:left">9.22%</td>
      <td style="text-align:left"><b>8.33%</b> (Avg. Calibrated PD)</td>
      <td style="text-align:left">
        <p><b>7.41%</b>
        </p>
        <p>(Average Default rate)</p>
      </td>
    </tr>
  </tbody>
</table>

## 5. Deriving PIT PD from TTC PD

IFRS9 require PIT PD conditioned on macroeconomic forecasts to estimate ECL. This involve a two-step process to derive conditional PD from TTC PD,

1. Determining various macro variables which affect PD
2. Determining the link function between macro factors and PD, which is then used to compute conditional or PIT PD

### 5.1 Determining Macro-economic variables

In order to determine significant Macro-economic variables, Run regressions between year wise ‘Observed default rates’ and all possible set of various ‘combinations of time dependent macro-economic factors’.

Minimum number of macro-factors in a combination is one and maximum number is all available factors.

The ‘combination’ which has highest R-square and highly significant variables should be used in deriving a link function between TTC PD and PIT PD

**Illustration:**

Assuming GDP, Expenditure and Revenue combination has high significance and highest R-square value.

|  | **Dependent Variable** | **Variable 1** | **Variable 2** | **Variable 3** |
| :--- | :--- | :--- | :--- | :--- |
| **Year** | **Observed Default rate** | **GDP** | **Expenditure** | **Revenue** |
| 2013 | 7.78% | 5.417 | 1.620 | 24.634 |
| 2014 | 8.81% | 4.351 | 3.445 | 25.238 |
| 2015 | 5.70% | 2.863 | 12.070 | 19.777 |
| 2016 | 10.51% | 2.915 | 35.376 | 17.638 |
| 2017 | 11.65% | 2.260 | 34.774 | 22.583 |

|  | Coefficient | P-value |
| :--- | :--- | :--- |
| R Square | 0.9507 |  |
| Adjusted R Square | 0.9027 |  |
| Intercept | -0.0917 | 0.03518 |
| GDP | 0.0087 | 0.04490 |
| Expenditure | 0.0022 | 0.01612 |
| Revenue | 0.0050 | 0.02659 |

### 5.2 Regression technique

**Step 1:** Regression based framework is commonly used as a link function when abundant data is available.

This model uses a linear regression between significant macro variables and historically observed PD values. The underlying regression model is expressed as follows:

PIT PD = Constant + ∑ Bi x Macroi \(T\)

Where,

**Βi** is a coefficient indicating the strength of correlation between the macro variables Macroi and the historically observed PD.

**Macroi \(T\)** is the normalised value of a macroeconomic variable Macroi at the time T

**Illustration:**

| Year | PD \(Dependent variable\) | GDP \(Independent variable 1\) | Expenditure \(Independent variable 2\) | Revenue \(Independent variable 3\) |
| :--- | :--- | :--- | :--- | :--- |
| 2013 | 7.78% | 5.417 | 1.620 | 24.634 |
| 2014 | 8.81% | 4.351 | 3.445 | 25.238 |
| 2015 | 5.70% | 2.863 | 12.070 | 19.777 |
| 2016 | 10.51% | 2.915 | 35.376 | 17.638 |
| 2017 | 11.65% | 2.260 | 34.774 | 22.583 |

|  | Coefficient | P-value |
| :--- | :--- | :--- |
| R Square | 0.9507 |  |
| Adjusted R Square | 0.9027 |  |
| Intercept | -0.0917 | 0.03518 |
| **GDP** | 0.0087 | 0.04490 |
| **Expenditure** | 0.0022 | 0.01612 |
| **Revenue** | 0.0050 | 0.02659 |

Therefore Link Function is **PIT PD = -0.0917 + \(0.0087 x GDP\) + \(0.0022 x Expenditure\) + \(0.0050 x Revenue\)**

**Step 2:** Calculate PIT PDs for future years using forecasted Macro factors

| Year | Observed Default rate | GDP | Expenditure | Revenue | PIT PD |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2013 | 7.78% | 5.417 | 1.620 | 24.634 | 8.28% |
| 2014 | 8.81% | 4.351 | 3.445 | 25.238 | 8.07% |
| 2015 | 5.70% | 2.863 | 12.070 | 19.777 | 5.97% |
| 2016 | 10.51% | 2.915 | 35.376 | 17.638 | 10.17% |
| 2017 | 11.65% | 2.260 | 34.774 | 22.583 | 11.95% |
| 2018 |  | 1.624 | 33.668 | 22.584 | 11.15% |
| 2019 |  | 1.711 | 33.518 | 22.253 | 11.03% |
| 2020 |  | 2.127 | 32.918 | 21.392 | 10.82% |
| 2021 |  | 2.219 | 32.655 | 21.101 | 10.70% |
| 2022 |  | 2.229 | 32.409 | 20.492 | 10.34% |

**Step 3:** Calibrate PIT PD to Rating Table using a scaling factor.

**Illustration:**

Scaling factor = Average \(Forecasted PIT PDs including previous year\) ÷ \(previous year observed Default rate\)

= Average \(11.95%, 11.15%, 11.03%, 10.82%, 10.70%, 10.34%\) ÷ 11.65% = 0.944

PIT PD = TTC PD x Scaling factor

|  RATING BAND | TTC PD | PIT PD |
| :--- | :--- | :--- |
| **1** | 0.12% | 0.12% x 0.944 = 0.11% |
| **2+** | 0.17% |  0.17% x 0.944 = 0.16% |
| **2** | 0.24% | 0.22% |
| **2-** | 0.34% | 0.32% |
| **3+** | 0.49% | 0.46% |
| **3** | 0.70% | 0.66% |
| **3-** | 1.00% | 0.94% |
| **4+** | 1.42% | 1.34% |
| **4** | 2.03% | 1.92% |
| **4-** | 2.88% | 2.72% |
| **5+** | 4.08% | 3.85% |
| **5** | 5.74% | 5.42% |
| **5-** | 8.01% | 7.56% |
| **6+** | 11.04% | 10.42% |
| **6** | 15.01% | 14.17% |
| **6-** | 20.04% | 18.92% |
| **7+** | 26.23% | 24.75% |
| **7** | 33.32% | 31.45% |
| **7-** | 41.08% | 38.77% |

## 6. Output

Output should be in the form of Term structure. Surya system should be able to Capture Cumulative PIT PD from term structure and use it in both 12m ECL and Life time ECL calculations as per the Rating given to a particular exposure.

Term Structure is prepared for both TTC PD and PIT PD.

**Output 1:** TTC PD Term Structure

Cumulative PD for year N or for lifetime is calculated using

**Cumulative PDN = 1- \(1- PD12M\) N**

**Illustration:**

| RATING | 1 | 2 | 3 | 4 | 5 | 6 |  n |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | 0.12% | =1-\(1-0.12%\)2 | =1-\(1-0.12%\)3 | =1-\(1-0.12%\)4 | =1-\(1-0.12%\)5 | =1-\(1-0.12%\)6 | =1-\(1-0.12%\)n |
| **2+** | 0.17% | 0.33% | =1-\(1-0.17%\)3 | =1-\(1-0.17%\)4 | =1-\(1-0.17%\)5 |  | =1-\(1-0.17%\)n |
| **2** | 0.24% | 0.48% | =1-\(1-0.24%\)3 | =1-\(1-0.24%\)4 |  |  | =1-\(1-0.24%\)n |
| **2-** | 0.34% | 0.68% | =1-\(1-0.34%\)3 |  |  |  |  |
| **3+** | 0.49% | 0.98% |  |  |  |  |  |
| **3** | 0.70% | 1.39% |  |  |  |  |  |
| **3-** | 1.00% | 1.99% |  |  |  |  |  |
| **4+** | 1.42% | 2.83% |  |  |  |  |  |
| **4** | 2.03% | 4.03% |  |  |  |  |  |
| **4-** | 2.88% | 5.69% |  |  |  |  |  |
| **5+** | 4.08% | 7.99% |  |  |  |  |  |
| **5** | 5.74% | 11.16% |  |  |  |  |  |
| **5-** | 8.01% | 15.37% |  |  |  |  |  |
| **6+** | 11.04% | 20.86% |  |  |  |  |  |
| **6** | 15.01% | 27.77% |  |  |  |  |  |
| **6-** | 20.04% | 36.07% |  |  |  |  |  |
| **7+** | 26.23% | 45.57% |  |  |  |  |  |
| **7** | 33.32% | 55.54% |  |  |  |  |  |
| **7-** | 41.08% | 65.29% |  |  |  |  |  |
| **8-9-10** | 100.00% | 100.00% |  |  |  |  |  |

**Output 2:** PIT PD Term Structure.

Similarly, PIT PD Term Structure should be prepared. It can be calculated by multiplying a scaling factor to each TTC PD of respective rating band and year. Scaling factors can be derived using future PIT PDs and previous year observed default rate. \(Step: 2, section-5.2\)

**Illustration:** As PIT PDs are forecasted for future 5 years \(Step: 2, Section-5.2\), scaling factors can be derived for next 5 years. Scaling factor calculation should be calculated for every year till 5th year. After that a constant scaling factor is applied.

Scaling factor for 1st year = Forecasted PIT PD ÷ Previous year observed Default rate

= 11.15% ÷ 11.65% = 0.957

Scaling factor for 2nd year = Forecasted PIT PD ÷ Previous year observed Default rate

= 11.03% ÷ 11.65% = 0.946

Scaling factor for 3rd year = Forecasted PIT PD ÷ Previous year observed Default rate

= 10.82% ÷ 11.65% = 0.928

Scaling factor for 4th year = Forecasted PIT PD ÷ Previous year observed Default rate

= 10.70% ÷ 11.65% = 0.918

Scaling factor for 5th year = Forecasted PIT PD ÷ Previous year observed Default rate

= 10.34% ÷ 11.65% = 0.888

Constant scaling factor from 6th year = Average \(Forecasted PIT PDs\) ÷ Previous year observed Default rate

= Average \(11.15%, 11.03%, 10.82%, 10.70%, 10.34%\) ÷ 11.65% = 0.928

| RATING | 1 | 2 | 3 | 4 | 5 | 6 | n |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | =0.12% x 0.957 | =0.23% x 0.946 | =1-\(1-0.12%\)3 x 0.928 | =1-\(1-0.12%\)4 x 0.918 | =1-\(1-0.12%\)5 x 0.888 | =1-\(1-0.12%\)6 x 0.928 | =1-\(1-0.12%\)n x 0.928 |
| **2+** | =0.17% x 0.957 | =0.33% x 0.946 | =1-\(1-0.17%\)3 x 0.928 | 0.61% | 0.74% | 0.92% |  |
| **2** | =0.24% x 0.957 | =0.48% x 0.946 | 0.66% | 0.87% | 1.05% | 1.32% |  |
| **2-** | =0.34% x 0.957 | 0.65% | 0.95% | 1.25% | 1.51% | 1.89% |  |
| **3+** | 0.47% | 0.92% | 1.36% | 1.78% | 2.15% | 2.69% |  |
| **3** | 0.67% | 1.32% | 1.94% | 2.54% | 3.06% | 3.83% |  |
| **3-** | 0.96% | 1.88% | 2.76% | 3.61% | 4.35% | 5.42% |  |
| **4+** | 1.36% | 2.68% | 3.91% | 5.12% | 6.14% | 7.65% |  |
| **4** | 1.95% | 3.81% | 5.55% | 7.24% | 8.66% | 10.76% |  |
| **4-** | 2.76% | 5.38% | 7.81% | 10.14% | 12.08% | 14.94% |  |
| **5+** | 3.90% | 7.56% | 10.90% | 14.07% | 16.67% | 20.49% |  |
| **5** | 5.50% | 10.56% | 15.10% | 19.34% | 22.73% | 27.71% |  |
| **5-** | 7.66% | 14.54% | 20.56% | 26.05% | 30.28% | 36.53% |  |
| **6+** | 10.56% | 19.74% | 27.48% | 34.30% | 39.30% | 46.77% |  |
| **6** | 14.36% | 26.28% | 35.85% | 43.89% | 49.40% | 57.79% |  |
| **6-** | 19.18% | 34.13% | 45.39% | 54.27% | 59.75% | 68.51% |  |
| **7+** | 25.10% | 43.13% | 55.57% | 64.59% | 69.36% | 77.79% |  |
| **7** | 31.89% | 52.56% | 65.33% | 73.64% | 77.06% | 84.59% |  |
| **7-** | 39.31% | 61.78% | 73.87% | 80.72% | 82.45% | 88.86% |  |
| **8-9-10** | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |  |

1. 
