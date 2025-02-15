![Version: 0.1.4](https://img.shields.io/static/v1?label=Version&message=0.1.4&color=blue&?style=plastic)
![Python](https://img.shields.io/badge/Python-3.6%20%7C%203.7%20%7C%203.8%20%7C%203.9-blue)
![Build: Passing](https://img.shields.io/static/v1?label=Build&message=passing&color=brightgreen)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=default)](http://makeapullrequest.com)
[![GitHub Stars](https://img.shields.io/github/stars/AdrianAntico/RetroFit.svg?style=social)](https://github.com/AdrianAntico/retrofit)

<img src="https://raw.githubusercontent.com/AdrianAntico/RetroFit/main/images/PackageLogo.PNG" align="center" width="1000" />

## Quick Note
This package is currently in its beginning stages. I'll be working off a blueprint from my R package RemixAutoML so there should be minimal breakages upon new releases, only non-breaking enhancements and additions. 

## Installation
```
# Most up-to-date
pip install git+https://github.com/AdrianAntico/RetroFit.git#egg=retrofit

# From pypi
pip install retrofit==0.1.4

# Check out R package RemixAutoML
https://github.com/AdrianAntico/RemixAutoML
```


## Feature Engineering

> Feature Engineering - Some of the feature engineering functions can only be found in this package. I believe feature engineering is your best bet for improving model performance. I have functions that cover all feature types. There are feature engineering functions for numeric data, categorical data, text data, and date data. They are all designed to generate features for training and scoring pipelines and they run extremely fast with low memory utilization. The package takes advantage of datatable or polars (user chooses) for all feature engineering and data wrangling related functions which means you'll only have to go to big data tools if absolutely necessary.

## Machine Learning

> Machine Learning Training -

> Machine Learning Scoring -

> Machine Learning Evaluation -

> Machine Learning Interpretation -



<img src="https://raw.githubusercontent.com/AdrianAntico/RetroFit/main/images/Documentation.PNG" align="center" width="1000" />




## Feature Engineering
<p>

<details><summary>Expand to view content</summary>
<p>


### FE0 Feature Engineering: Row-Dependence
<p>

<details><summary>Expand to view content</summary>
<p>


#### **FE0_AutoLags()**
<p>

<details><summary>Function Description</summary>
<p>
 
<code>FE0_AutoLags()</code> Automatically generate any number of lags, for any number of columns, by any number of By-Variables, using datatable.

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# QA: Test FE0_AutoLags
import timeit
import datatable as dt
import polars as pl
import retrofit
from retrofit import FeatureEngineering as fe

## No Group Example: datatable
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE0_AutoLags(
  data=data, 
  ArgsList=None, 
  LagPeriods=1, 
  LagColumnNames='Leads', 
  DateColumnName='CalendarDateColumn', 
  ByVariables=None, 
  ImputeValue=-1, 
  Sort=True, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
data1 = Output['data']
ArgsList = Output['ArgsList']
del Output
print(data1.names)
print(ArgsList)

## No Group Example: polars
data = pl.read_csv("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE0_AutoLags(
  data=data, 
  ArgsList=None, 
  LagPeriods=1, 
  LagColumnNames='Leads', 
  DateColumnName='CalendarDateColumn', 
  ByVariables=None, 
  ImputeValue=-1.0, 
  Sort=True, 
  Processing='polars', 
  InputFrame='polars', 
  OutputFrame='polars')
t_end = timeit.default_timer()
print(t_end - t_start)
data2 = Output['data']
ArgsList = Output['ArgsList']
del Output
print(data2.columns)
print(ArgsList)

## Group Example, Single Lag: datatable
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE0_AutoLags(
  data=data, 
  ArgsList=None, 
  LagPeriods=1, 
  LagColumnNames='Leads', 
  DateColumnName='CalendarDateColumn', 
  ByVariables=['MarketingSegments','MarketingSegments2','MarketingSegments3', 'Label'], 
  ImputeValue=-1, 
  Sort=True, 
  Processing='datatable',
  InputFrame='datatable',
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
data1 = Output['data']
ArgsList = Output['ArgsList']
del Output
print(data1.names)
print(ArgsList)

## Group Exmaple: polars
data = pl.read_csv("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE0_AutoLags(
  data=data, 
  ArgsList=None, 
  LagPeriods=1, 
  LagColumnNames='Leads', 
  DateColumnName='CalendarDateColumn', 
  ByVariables=['MarketingSegments','MarketingSegments2','MarketingSegments3', 'Label'], 
  ImputeValue=-1.0, 
  Sort=True, 
  Processing='polars', 
  InputFrame='polars', 
  OutputFrame='polars')
t_end = timeit.default_timer()
print(t_end - t_start)
data2 = Output['data']
ArgsList = Output['ArgsList']
del Output
print(data2.columns)
print(ArgsList)

## Group and Multiple Periods and LagColumnNames: datatable
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE0_AutoLags(
  data=data, 
  ArgsList=None, 
  LagPeriods=[1,3,5], 
  LagColumnNames=['Leads','XREGS1'], 
  DateColumnName='CalendarDateColumn', 
  ByVariables=['MarketingSegments','MarketingSegments2','MarketingSegments3', 'Label'], 
  ImputeValue=-1, 
  Sort=True, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
data1 = Output['data']
ArgsList = Output['ArgsList']
del Output
print(data1.names)
print(ArgsList)

## Group and Multiple Periods and LagColumnNames: datatable
data = pl.read_csv("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE0_AutoLags(
  data=data, 
  ArgsList=None, 
  LagPeriods=[1,3,5],
  LagColumnNames=['Leads','XREGS1'], 
  DateColumnName='CalendarDateColumn', 
  ByVariables=['MarketingSegments','MarketingSegments2','MarketingSegments3', 'Label'], 
  ImputeValue=-1.0, 
  Sort=True, 
  Processing='polars', 
  InputFrame='polars', 
  OutputFrame='polars')
t_end = timeit.default_timer()
print(t_end - t_start)
data2 = Output['data']
ArgsList = Output['ArgsList']
del Output
print(data2.columns)
print(ArgsList)
```

</p>
</details>



#### **FE0_AutoRollStats()**
<p>


<details><summary>Function Description</summary>
<p>
 
<code>FE0_AutoRollStats()</code> Automatically generate any number of moving averages, moving standard deviations, moving mins and moving maxs from any number of source columns, by any number of By-Variables, using datatable.

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# Test Function
import timeit
import datatable as dt
import retrofit
from retrofit import FeatureEngineering as fe

## Group Example:
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.FE0_AutoRollStats(
  data=data, 
  RollColumnNames='Leads', 
  DateColumnName='CalendarDateColumn', 
  ByVariables=None, 
  MovingAvg_Periods=[3,5,7], 
  MovingSD_Periods=[3,5,7], 
  MovingMin_Periods=[3,5,7], 
  MovingMax_Periods=[3,5,7], 
  ImputeValue=-1, 
  Sort=True, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
print(data.names)
    
## Group and Multiple Periods and RollColumnNames:
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.FE0_AutoRollStats(
  data=data, 
  RollColumnNames=['Leads','XREGS1'], 
  DateColumnName='CalendarDateColumn', 
  ByVariables=['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3', 'Label'], 
  MovingAvg_Periods=[3,5,7], 
  MovingSD_Periods=[3,5,7], 
  MovingMin_Periods=[3,5,7], 
  MovingMax_Periods=[3,5,7], 
  ImputeValue=-1, 
  Sort=True, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
print(data.names)

## No Group Example:
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.FE0_AutoRollStats(
  data=data, 
  RollColumnNames='Leads', 
  DateColumnName='CalendarDateColumn', 
  ByVariables=None, 
  MovingAvg_Periods=[3,5,7], 
  MovingSD_Periods=[3,5,7], 
  MovingMin_Periods=[3,5,7], 
  MovingMax_Periods=[3,5,7], 
  ImputeValue=-1, 
  Sort=True, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
print(data.names)
```

</p>
</details>



#### **FE0_AutoDiff()**
<p>

<details><summary>Function Description</summary>
<p>
 
<code>FE0_AutoDiff()</code> Automatically generate any number of differences from any number of source columns, for numeric, character, and date columns, by any number of By-Variables, using datatable.

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# Test Function
import timeit
import datatable as dt
import retrofit
from retrofit import FeatureEngineering as fe

## Group Example:
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.FE0_AutoDiff(
  data=data, 
  DateColumnName = 'CalendarDateColumn', 
  ByVariables = ['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3', 'Label'], 
  DiffNumericVariables = 'Leads', 
  DiffDateVariables = 'CalendarDateColumn', 
  DiffGroupVariables = None, 
  NLag1 = 0, 
  NLag2 = 1, 
  Sort=True, 
  Processing='datatable',
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
print(data.names)
    
## Group and Multiple Periods and RollColumnNames:
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.FE0_AutoDiff(
  data=data, 
  DateColumnName = 'CalendarDateColumn',
  ByVariables = ['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3', 'Label'], 
  DiffNumericVariables = 'Leads', 
  DiffDateVariables = 'CalendarDateColumn', 
  DiffGroupVariables = None, 
  NLag1 = 0, 
  NLag2 = 1, 
  Sort=True, 
  Processing = 'datatable',
  InputFrame = 'datatable',
  OutputFrame = 'datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
print(data.names)

## No Group Example:
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.FE0_AutoDiff(
  data=data, 
  DateColumnName = 'CalendarDateColumn', 
  ByVariables = None, 
  DiffNumericVariables = 'Leads', 
  DiffDateVariables = 'CalendarDateColumn', 
  DiffGroupVariables = None, 
  NLag1 = 0, 
  NLag2 = 1, 
  Sort=True, 
  Processing = 'datatable',
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
print(data.names)
```

</p>
</details>



</p>
</details>


### FE1 Feature Engineering: Row-Independence
<p>

<details><summary>Expand to view content</summary>
<p>

#### **FE1_AutoCalendarVariables()**
<p>

<details><summary>Function Description</summary>
<p>
 
<code>FE1_AutoCalendarVariables()</code> Automatically generate calendar variables from your datatable.

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# Test Function
import timeit
import datatable as dt
import retrofit
from retrofit import FeatureEngineering as fe
 
# Data can be created using the R package RemixAutoML and function FakeDataGenerator
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
data = fe.AutoCalendarVariables(
  data=data, 
  ArgsList=None, 
  DateColumnNames = 'CalendarDateColumn', 
  CalendarVariables = ['wday','mday','wom','month','quarter','year'], 
  Processing = 'datatable', 
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
data.names
```

</p>
</details>





#### **FE1_DummyVariables()**
<p>

<details><summary>Function Description</summary>
<p>
 
<code>FE1_DummyVariables()</code> Automatically generate dummy variables for user supplied categorical columns

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# Example: datatable
import timeit
import datatable as dt
import retrofit
from retrofit import FeatureEngineering as fe
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE1_DummyVariables(
  data=data, 
  ArgsList=None, 
  CategoricalColumnNames=['MarketingSegments','MarketingSegments2'], 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
t_end - t_start
data = Output['data']
ArgsList = Output['ArgsList']


# Example: polars
import retrofit
from retrofit import FeatureEngineering as fe
import polars as pl
data = pl.read_csv("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
Output = fe.FE1_DummyVariables(
  data=data, 
  ArgsList=None, 
  CategoricalColumnNames=['MarketingSegments','MarketingSegments2'], 
  Processing='polars', 
  InputFrame='polars', 
  OutputFrame='polars')
t_end = timeit.default_timer()
t_end - t_start
data = Output['data']
ArgsList = Output['ArgsList']
```

</p>
</details>





</p>
</details>



### FE2 Feature Engineering: Full-Data-Set
<p>

<details><summary>Expand to view content</summary>
<p>


#### **FE2_AutoDataParition()**
<p>

<details><summary>Function Description</summary>
<p>
 
<code>FE2_AutoDataParition()</code> Automatically create data sets for training based on random or time based splits

</p>
</details>

<details><summary>Code Example</summary>
<p>


```
# FE2_AutoDataParition
import timeit
import datatable as dt
import polars as pl
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import utils as u

# datatable random Example
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='random', 
  Ratios=[0.70,0.20,0.10], 
  Sort = False,
  ByVariables=None, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
ArgsList = DataSets['ArgsList']

# polars random Example
data = pl.read_csv("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='random', 
  Ratios=[0.70,0.20,0.10], 
  ByVariables=None, 
  Sort = False,
  Processing='polars', 
  InputFrame='polars', 
  OutputFrame='polars')
t_end = timeit.default_timer()
print(t_end - t_start)
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
ArgsList = DataSets['ArgsList']

# datatable time Example
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='time', 
  Ratios=[0.70,0.20,0.10], 
  Sort = True,
  ByVariables=None, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')
t_end = timeit.default_timer()
print(t_end - t_start)
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
ArgsList = DataSets['ArgsList']

# polars time Example
data = pl.read_csv("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
t_start = timeit.default_timer()
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='time', 
  Ratios=[0.70,0.20,0.10], 
  ByVariables=None, 
  Sort = True,
  Processing='polars', 
  InputFrame='polars', 
  OutputFrame='polars')
t_end = timeit.default_timer()
t_end - t_start
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
ArgsList = DataSets['ArgsList']
```

</p>
</details>




</p>
</details>


### FE3 Feature Engineering: Model-Based
<p>

<details><summary>Expand to view content</summary>
<p>

##### Coming soon

</p>
</details>

</p>
</details>



## Machine Learning Training
<p>
 
<details><summary>Expand to view content</summary>
<p>


### ML0 Machine Learning: Prepare for Modeling
<p>

<details><summary>Expand to view content</summary>
<p>


#### **ML0_Parameters()**
<details><summary>Function Description</summary>
<p>
 
<code>ML0_Parameters()</code> Automatically generate parameters for modeling. User can update the parameters as desired.

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# Setup Environment
import timeit
import datatable as dt
from datatable import sort, f, by
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import MachineLearning as ml

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")

# Create partitioned data sets
Data = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName=None, 
  PartitionType='random', 
  Ratios=[0.7,0.2,0.1], 
  ByVariables=None, 
  Sort=False, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')

# Prepare modeling data sets
DataSets = ml.ML0_GetModelData(
  Processing='catboost',
  TrainData=Data['TrainData'],
  ValidationData=Data['ValidationData'],
  TestData=Data['TestData'],
  ArgsList=None,
  TargetColumnName='Leads',
  NumericColumnNames=['XREGS1','XREGS2','XREGS3'],
  CategoricalColumnNames=['MarketingSegments','MarketingSegments2','MarketingSegments3','Label'],
  TextColumnNames=None,
  WeightColumnName=None,
  Threads=-1,
  InputFrame='datatable')

# Get args list for algorithm and target type
ModelArgs = ml.ML0_Parameters(
  Algorithms='CatBoost', 
  TargetType="Regression", 
  TrainMethod="Train")
```

</p>
</details>



#### **ML0_GetModelData()**
<p>

<details><summary>Function Description</summary>
<p>
 
<code>ML0_GetModelData()</code> Automatically create data sets chosen ML algorithm. Currently supports catboost, xgboost, and lightgbm.

</p>
</details>

<details><summary>Code Example</summary>
<p>

```
# ML0_GetModelData Example:
import datatable as dt
from datatable import sort, f, by
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import MachineLearning as ml

############################################################################################
# CatBoost
############################################################################################

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
    
# Create partitioned data sets
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='random', 
  Ratios=[0.70,0.20,0.10], 
  ByVariables=None, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')

# Collect partitioned data
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
del DataSets

# Create catboost data sets
DataSets = ml.ML0_GetModelData(
  TrainData=TrainData, 
  ValidationData=ValidationData, 
  TestData=TestData, 
  ArgsList=None, 
  TargetColumnName='Leads', 
  NumericColumnNames=['XREGS1', 'XREGS2', 'XREGS3'], 
  CategoricalColumnNames=['MarketingSegments','MarketingSegments2','MarketingSegments3','Label'], 
  TextColumnNames=None, 
  WeightColumnName=None, 
  Threads=-1, 
  Processing='catboost', 
  InputFrame='datatable')
  
# Collect catboost training data
catboost_train = DataSets['train_data']
catboost_validation = DataSets['validation_data']
catboost_test = DataSets['test_data']

############################################################################################
# XGBoost
############################################################################################

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
    
# Create partitioned data sets
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='random', 
  Ratios=[0.70,0.20,0.10], 
  ByVariables=None, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')

# Collect partitioned data
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
del DataSets

# Create xgboost data sets
DataSets = ml.ML0_GetModelData(
  TrainData=TrainData, 
  ValidationData=ValidationData, 
  TestData=TestData, 
  ArgsList=None, 
  TargetColumnName='Leads', 
  NumericColumnNames=['XREGS1', 'XREGS2', 'XREGS3'], 
  CategoricalColumnNames=['MarketingSegments','MarketingSegments2','MarketingSegments3','Label'], 
  TextColumnNames=None, 
  WeightColumnName=None, 
  Threads=-1, 
  Processing='xgboost', 
  InputFrame='datatable')
  
# Collect xgboost training data
xgboost_train = DataSets['train_data']
xgboost_validation = DataSets['validation_data']
xgboost_test = DataSets['test_data']

############################################################################################
# LightGBM
############################################################################################

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")
    
# Create partitioned data sets
DataSets = fe.FE2_AutoDataParition(
  data=data, 
  ArgsList=None, 
  DateColumnName='CalendarDateColumn', 
  PartitionType='random', 
  Ratios=[0.70,0.20,0.10], 
  ByVariables=None, 
  Processing='datatable', 
  InputFrame='datatable', 
  OutputFrame='datatable')

# Collect partitioned data
TrainData = DataSets['TrainData']
ValidationData = DataSets['ValidationData']
TestData = DataSets['TestData']
del DataSets

# Create lightgbm data sets
DataSets = ml.ML0_GetModelData(
  TrainData=TrainData, 
  ValidationData=ValidationData, 
  TestData=TestData, 
  ArgsList=None, 
  TargetColumnName='Leads', 
  NumericColumnNames=['XREGS1', 'XREGS2', 'XREGS3'], 
  CategoricalColumnNames=['MarketingSegments','MarketingSegments2','MarketingSegments3','Label'], 
  TextColumnNames=None, 
  WeightColumnName=None, 
  Threads=-1, 
  Processing='lightgbm', 
  InputFrame='datatable')
  
# Collect lightgbm training data
lightgbm_train = DataSets['train_data']
lightgbm_validation = DataSets['validation_data']
lightgbm_test = DataSets['test_data']
```

</p>
</details>




</p>
</details>



### ML1 Machine Learning: RetroFit Class
<p>

<details><summary>Expand to view content</summary>
<p>


<details><summary>Class Goals</summary>
<p>

```
####################################
# Goals
####################################

Class Initialization
Model Initialization
Training
Feature Tuning
Grid Tuning
Model Scoring
Model Evaluation
Model Interpretation
```

</p>
</details>

<details><summary>Class Functions</summary>
<p>

```
####################################
# Functions
####################################

ML1_Single_Train()
ML1_Single_Score()
PrintAlgoArgs()
```

</p>
</details>


<details><summary>Class Attributes</summary>
<p>

```
####################################
# Attributes
####################################

self.ModelArgs = ModelArgs
self.ModelArgsNames = [*self.ModelArgs]
self.Runs = len(self.ModelArgs)
self.DataSets = DataSets
self.DataSetsNames = [*self.DataSets]
self.ModelList = dict()
self.ModelListNames = []
self.FitList = dict()
self.FitListNames = []
self.EvaluationList = dict()
self.EvaluationListNames = []
self.InterpretationList = dict()
self.InterpretationListNames = []
self.CompareModelsList = dict()
self.CompareModelsListNames = []
```

</p>
</details>


<details><summary>Ftrl Example</summary>
<p>

```
####################################
# Ftrl Example
####################################

# Setup Environment
import timeit
import datatable as dt
from datatable import sort, f, by
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import MachineLearning as ml

# Load some data
# BechmarkData.csv is located is the tests folder
Path = "./BenchmarkData.csv"
data = dt.fread(Path)

# Create partitioned data sets
DataFrames = fe.FE2_AutoDataParition(
  data = data, 
  ArgsList = None, 
  DateColumnName = None, 
  PartitionType = 'random', 
  Ratios = [0.7,0.2,0.1], 
  ByVariables = None, 
  Sort = False, 
  Processing = 'datatable', 
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')

# Prepare modeling data sets
ModelData = ml.ML0_GetModelData(
  Processing = 'Ftrl',
  TrainData = DataFrames['TrainData'],
  ValidationData = DataFrames['ValidationData'],
  TestData = DataFrames['TestData'],
  ArgsList = None,
  TargetColumnName = 'Leads',
  NumericColumnNames = ['XREGS1', 'XREGS2', 'XREGS3'],
  CategoricalColumnNames = ['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3', 'Label'],
  TextColumnNames = None,
  WeightColumnName = None,
  Threads = -1,
  InputFrame = 'datatable')

# Get args list for algorithm and target type
ModelArgs = ml.ML0_Parameters(
  Algorithms = 'Ftrl', 
  TargetType = "Regression", 
  TrainMethod = "Train")

# Initialize RetroFit
x = RetroFit(ModelArgs, ModelData, DataFrames)

# Train Model
x.ML1_Single_Train(Algorithm = 'Ftrl')

# Score data
x.ML1_Single_Score(
  DataName = x.DataSetsNames[2], 
  ModelName = x.ModelListNames[0], 
  Algorithm = 'Ftrl', 
  NewData = None)

# Scoring data names
x.DataSetsNames

# Scoring data
x.DataSets.get('Scored_test_data_Ftrl_1')

# Check ModelArgs Dict
x.PrintAlgoArgs(Algo='Ftrl')

# List of model names
x.ModelListNames

# List of model fitted names
x.FitListNames
```

</p>
</details>


<details><summary>CatBoost Example</summary>
<p>

```
####################################
# CatBoost Example Usage
####################################

# Setup Environment
import timeit
import datatable as dt
from datatable import sort, f, by
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import MachineLearning as ml

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")

# Create partitioned data sets
DataFrames = fe.FE2_AutoDataParition(
  data = data, 
  ArgsList = None, 
  DateColumnName = None, 
  PartitionType = 'random', 
  Ratios = [0.7,0.2,0.1], 
  ByVariables = None, 
  Sort = False, 
  Processing = 'datatable', 
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')

# Prepare modeling data sets
ModelData = ml.ML0_GetModelData(
  Processing = 'catboost',
  TrainData = DataFrames['TrainData'],
  ValidationData = DataFrames['ValidationData'],
  TestData = DataFrames['TestData'],
  ArgsList = None,
  TargetColumnName = 'Leads',
  NumericColumnNames = ['XREGS1', 'XREGS2', 'XREGS3'],
  CategoricalColumnNames = ['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3', 'Label'],
  TextColumnNames = None,
  WeightColumnName = None,
  Threads = -1,
  InputFrame = 'datatable')

# Get args list for algorithm and target type
ModelArgs = ml.ML0_Parameters(
  Algorithms = 'CatBoost', 
  TargetType = "Regression", 
  TrainMethod = "Train")

# Update iterations to run quickly
ModelArgs['CatBoost']['AlgoArgs']['iterations'] = 50

# Initialize RetroFit
x = ml.RetroFit(ModelArgs, ModelData, DataFrames)

# Train Model
x.ML1_Single_Train(Algorithm = 'CatBoost')

# Score data
x.ML1_Single_Score(
  DataName = x.DataSetsNames[2], 
  ModelName = x.ModelListNames[0],
  Algorithm = 'CatBoost',
  NewData = None)

# Scoring data names
x.DataSetsNames

# Scoring data
x.DataSets.get('Scored_test_data_CatBoost_1')

# Check ModelArgs Dict
x.PrintAlgoArgs(Algo = 'CatBoost')

# List of model names
x.ModelListNames

# List of model fitted names
x.FitListNames
```

</p>
</details>


<details><summary>XGBoost Example</summary>
<p>

```
####################################
# XGBoost Example Usage
####################################

# Setup Environment
import timeit
import datatable as dt
from datatable import sort, f, by
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import MachineLearning as ml

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")

# Create partitioned data sets
DataFrames = fe.FE2_AutoDataParition(
  data = data, 
  ArgsList = None, 
  DateColumnName = None, 
  PartitionType = 'random', 
  Ratios = [0.7,0.2,0.1], 
  ByVariables = None, 
  Sort = False, 
  Processing = 'datatable', 
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')

# Prepare modeling data sets
ModelData = ml.ML0_GetModelData(
  Processing = 'xgboost',
  TrainData = DataFrames['TrainData'],
  ValidationData = DataFrames['ValidationData'],
  TestData = DataFrames['TestData'],
  ArgsList = None,
  TargetColumnName = 'Leads',
  NumericColumnNames = ['XREGS1', 'XREGS2', 'XREGS3'],
  CategoricalColumnNames = ['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3', 'Label'],
  TextColumnNames = None,
  WeightColumnName = None,
  Threads = -1,
  InputFrame = 'datatable')

# Get args list for algorithm and target type
ModelArgs = ml.ML0_Parameters(
  Algorithms = 'XGBoost', 
  TargetType = "Regression", 
  TrainMethod = "Train")

# Update iterations to run quickly
ModelArgs['XGBoost']['AlgoArgs']['num_boost_round'] = 50

# Initialize RetroFit
x = ml.RetroFit(ModelArgs, ModelData, DataFrames)

# Train Model
x.ML1_Single_Train(Algorithm = 'XGBoost')

# Score data
x.ML1_Single_Score(
  DataName = x.DataSetsNames[2],
  ModelName = x.ModelListNames[0],
  Algorithm = 'XGBoost',
  NewData = None)

# Scoring data names
x.DataSetsNames

# Scoring data
x.DataSets.get('Scored_test_data_XGBoost_1')

# Check ModelArgs Dict
x.PrintAlgoArgs(Algo = 'XGBoost')

# List of model names
x.ModelListNames

# List of model fitted names
x.FitListNames
```


</p>
</details>


<details><summary>LightGBM Example</summary>
<p>

```
####################################
# LightGBM Example Usage
####################################

# Setup Environment
import timeit
import datatable as dt
from datatable import sort, f, by
import retrofit
from retrofit import FeatureEngineering as fe
from retrofit import MachineLearning as ml

# Load some data
data = dt.fread("C:/Users/Bizon/Documents/GitHub/BenchmarkData.csv")

# Dummify
Output = fe.FE1_DummyVariables(
  data = data, 
  ArgsList = None, 
  CategoricalColumnNames = ['MarketingSegments', 'MarketingSegments2', 'MarketingSegments3'], 
  Processing = 'datatable', 
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')
data = Output['data']
data = data[:, [name not in ['MarketingSegments','MarketingSegments2','MarketingSegments3','Label'] for name in data.names]]

# Create partitioned data sets
DataFrames = fe.FE2_AutoDataParition(
  data = data, 
  ArgsList = None, 
  DateColumnName = None, 
  PartitionType = 'random', 
  Ratios = [0.7,0.2,0.1], 
  ByVariables = None, 
  Sort = False, 
  Processing = 'datatable', 
  InputFrame = 'datatable', 
  OutputFrame = 'datatable')

# Features
Features = ['XREGS1', 'XREGS2', 'XREGS3', 'MarketingSegments_B', 'MarketingSegments_A', 'MarketingSegments_C', 'MarketingSegments2_a', 'MarketingSegments2_b', 'MarketingSegments2_c', 'MarketingSegments3_x', 'MarketingSegments3_z', 'MarketingSegments3_y']

# Prepare modeling data sets
ModelData = ml.ML0_GetModelData(
  Processing = 'lightgbm',
  TrainData = DataFrames['TrainData'],
  ValidationData = DataFrames['ValidationData'],
  TestData = DataFrames['TestData'],
  ArgsList = None,
  TargetColumnName = 'Leads',
  NumericColumnNames = Features,
  CategoricalColumnNames = None,
  TextColumnNames = None,
  WeightColumnName = None,
  Threads = -1,
  InputFrame = 'datatable')

# Get args list for algorithm and target type
ModelArgs = ml.ML0_Parameters(
  Algorithms = 'LightGBM', 
  TargetType = "Regression", 
  TrainMethod = "Train")

# Update iterations to run quickly
ModelArgs['LightGBM']['AlgoArgs']['num_boost_round'] = 50

# Initialize RetroFit
x = ml.RetroFit(ModelArgs, ModelData, DataFrames)

# Train Model
x.ML1_Single_Train(Algorithm = 'LightGBM')

# Score data
x.ML1_Single_Score(
  DataName = x.DataSetsNames[2],
  ModelName = x.ModelListNames[0],
  Algorithm = 'LightGBM')

# Scoring data names
x.DataSetsNames

# Scoring data
x.DataSets.get('Scored_test_data_LightGBM_1')

# Check ModelArgs Dict
x.PrintAlgoArgs(Algo = 'LightGBM')

# List of model names
x.ModelListNames

# List of model fitted names
x.FitListNames
```

</p>
</details>


</p>
</details>


</p>
</details>



## Machine Learning Evaluation
<p>
 
<details><summary>Expand to view content</summary>
<p>

#### Coming Soon

</p>
</details>




## Machine Learning Interpretation
<p>
 
<details><summary>Expand to view content</summary>
<p>

#### Coming Soon

</p>
</details>


## Machine Learning Scoring
<p>
 
<details><summary>Expand to view content</summary>
<p>

#### Coming Soon

</p>
</details>

