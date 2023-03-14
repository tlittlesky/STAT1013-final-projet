---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="5uCV-doSqK15">

# Employee data

</div>

<div class="cell markdown" id="ssIvTdgAqn8y">

**Description**:

Dataset describing the survival status of individual passengers on the
Titanic.

**Github**:
<https://github.com/prasertcbs/basic-dataset/blob/master/Employee%20data.csv>

**Sample size**: 474

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="16Pg-bYQ1-_0" outputId="5aec9e64-8577-4a51-e884-e78d4870c467">

``` python
## Type of data
df.info()
```

<div class="output stream stdout">

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 474 entries, 0 to 473
    Data columns (total 10 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   id        474 non-null    float64
     1   gender    474 non-null    object 
     2   bdate     473 non-null    object 
     3   educ      474 non-null    int64  
     4   jobcat    474 non-null    object 
     5   salary    474 non-null    float64
     6   salbegin  474 non-null    float64
     7   jobtime   474 non-null    float64
     8   prevexp   474 non-null    object 
     9   minority  474 non-null    object 
    dtypes: float64(4), int64(1), object(5)
    memory usage: 37.2+ KB

</div>

</div>

<div class="cell markdown" id="bSTcc4v8rd_F">

## Hypothesis

-   Tell us what your idea is and why you have chosen to pursue this
    idea.
    -   We are interested in "*Did men have higher salary in
        workplace?*"
-   What two groups you are comparing:
    -   **G1**: salary of male; **G2**: salary of female
-   What you will be measuring (i.e., what your response variable will
    be)
    -   `salary`
-   Is your response variable quantitative rather than categorical?
    -   `salary` is continuous data and the level of measurement is
        ratio. Therefore the response variable quantitative.
-   Make a prediction about what kind of difference you expect to see
    between your samples and WHY.
    -   We'd expect that **G1** \> **G2** because of the [Differences in
        industries or jobs
        worked](https://www.americanprogress.org/article/quick-facts-gender-wage-gap/)
-   Talk about how you will gather your data
    -   From Github link:
        <https://github.com/prasertcbs/basic-dataset/blob/master/Employee%20data.csv>
-   If you had unlimited resources (time, money, staff, etc.) how would
    you collect your data?
    -   \(i\) Increase the sample size and try to collect all of the
        salary data around the globe; (ii) investigate more former data
        in the past and compare the gender pay gap in different time.

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="oxBYZDT9xhjN" outputId="6b56edf9-87d7-4018-8fa4-e72944ff5c1a">

``` python
## load dataset from github

import pandas as pd

df = pd.read_csv('https://raw.githubusercontent.com/prasertcbs/basic-dataset/master/Employee%20data.csv')
df.head(5)
```

<div class="output execute_result" execution_count="6">

        id  gender       bdate  educ    jobcat   salary  salbegin  jobtime  \
    0  1.0    Male  1952-02-03    15   Manager  57000.0   27000.0     98.0   
    1  2.0    Male  1958-05-23    16  Clerical  40200.0   18750.0     98.0   
    2  3.0  Female  1929-07-26    12  Clerical  21450.0   12000.0     98.0   
    3  4.0  Female  1947-04-15     8  Clerical  21900.0   13200.0     98.0   
    4  5.0    Male  1955-02-09    15  Clerical  45000.0   21000.0     98.0   

      prevexp minority  
    0   144.0       No  
    1    36.0       No  
    2   381.0       No  
    3   190.0       No  
    4   138.0       No  

</div>

</div>

<div class="cell markdown" id="9NAGVn-dx7Ft">

-   Tell us what groups you want to compare in the dataset
    -   **G1** (salary \| sex = male) vs. **G2** (salary \| sex =
        female)

</div>

<div class="cell markdown" id="lwQ3jKG_yLNi">

Print first 5 records of each group, respectively.

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="bo8tGtqiyak5" outputId="c51289d0-14aa-4e33-9e25-0635897ff5c5">

``` python
## First 5 records of G1 (male)
(df[df['gender'] == 'Male']['salary']).head(5)
```

<div class="output execute_result" execution_count="8">

    0    57000.0
    1    40200.0
    4    45000.0
    5    32100.0
    6    36000.0
    Name: salary, dtype: float64

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="2Yq3vXXSy333" outputId="89e6abcd-af65-45ba-8908-11d3a932accc">

``` python
## First 5 records of G2 (female)
(df[df['gender'] == 'Female']['salary']).head(5)
```

<div class="output execute_result" execution_count="9">

    2    21450.0
    3    21900.0
    7    21900.0
    8    27900.0
    9    24000.0
    Name: salary, dtype: float64

</div>

</div>

<div class="cell markdown" id="peuVBBkA1HDl">

## Any other data description and visualization you want to add.

1.The mean salary of men is higher than female

2.The mean education level of men is higher than female

3.The mean job time of men is higher than female

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="maTwN79Q2W5X" outputId="78b41737-9b28-4f49-bbde-bed11c0f35e7">

``` python
print('sample mean of salary conditional on <gender = Male>')
print(df[df['gender'] == 'Male']['salary'].mean())
print('sample mean of salary conditional on <gender = Female>')
print(df[df['gender'] == 'Female']['salary'].mean())
```

<div class="output stream stdout">

    sample mean of salary conditional on <gender = Male>
    41441.782945736435
    sample mean of salary conditional on <gender = Female>
    26031.921296296296

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="RgxDCdgX3d0W" outputId="33482f9e-2482-47fa-b064-0656fb264f5c">

``` python
print('sample mean of education level on <gender = Male>')
print(df[df['gender'] == 'Male']['educ'].mean())
print('sample mean of education level on <gender = Female>')
print(df[df['gender'] == 'Female']['educ'].mean())
```

<div class="output stream stdout">

    sample mean of education level on <gender = Male>
    14.430232558139535
    sample mean of education level on <gender = Female>
    12.37037037037037

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="e48FVFnM33LO" outputId="db1c0ae5-811c-4408-daa7-2e738085020f">

``` python
print('sample mean of job time on <gender = Male>')
print(df[df['gender'] == 'Male']['jobtime'].mean())
print('sample mean of job time on <gender = Female>')
print(df[df['gender'] == 'Female']['jobtime'].mean())
```

<div class="output stream stdout">

    sample mean of job time on <gender = Male>
    81.72093023255815
    sample mean of job time on <gender = Female>
    80.37962962962963

</div>

</div>
