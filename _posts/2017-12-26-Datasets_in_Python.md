---
layout: post
title: Datasets in Python
---

There are many providers of free datasets for data science. Some of them are summarized [here](https://datascience.stackexchange.com/questions/155/publicly-available-datasets) and [here](https://www.kdnuggets.com/datasets/index.html). These datasets are often provided through an API and are stored in different formats. Getting them into a `pandas` `DataFrame` is often an overkill if we just want to quickly try out some machine-learning algorithm or a visualization. In this post, I give an overview of "built-in" datasets that are provided by popular python data science packages, such as [`statsmodels`](http://www.statsmodels.org), [`scikit-learn`](http://scikit-learn.org), and [`seaborn`](https://seaborn.pydata.org/).  These datasets can be easily accessed in form of a `pandas` `DataFrame` and can be used for quick experimenting.

## Statsmodels

[Statsmodels provides two types of datasets](http://www.statsmodels.org/dev/datasets/index.html): around two dozens of built-in datasets that are installed alongside the `statsmodels` package, and a collection of datasets from multiple R packages that can be downloaded on demand. Both types of datasets can be easily accessed using the Statsmodels' `statsmodels.api.datasets` module.

### Built-in Datasets

An example of a built-in datasets is the American National Election Studies of 1996 dataset that is stored in the `anes96` submodule of the `datasets` module. Every dataset submodule has attributes `DESCRLONG` and `NOTE` that give a detailed description of the dataset:

```python
import statsmodels.api as sm
anes96 = sm.datasets.anes96

print(anes96.DESCRLONG)
```
```
This data is a subset of the American National Election Studies of 1996.
```
<br>
```python
print(anes96.NOTE)
```
<div class="highlighter-rouge"><pre class="highlight" style="height: 20em;"><code>
 ::
    
        Number of observations - 944
        Number of variables - 10
    
        Variables name definitions::
    
                popul - Census place population in 1000s
                TVnews - Number of times per week that respondent watches TV news.
                PID - Party identification of respondent.
                    0 - Strong Democrat
                    1 - Weak Democrat
                    2 - Independent-Democrat
                    3 - Independent-Indpendent
                    4 - Independent-Republican
                    5 - Weak Republican
                    6 - Strong Republican
                age : Age of respondent.
                educ - Education level of respondent
                    1 - 1-8 grades
                    2 - Some high school
                    3 - High school graduate
                    4 - Some college
                    5 - College degree
                    6 - Master's degree
                    7 - PhD
                income - Income of household
                    1  - None or less than $2,999
                    2  - $3,000-$4,999
                    3  - $5,000-$6,999
                    4  - $7,000-$8,999
                    5  - $9,000-$9,999
                    6  - $10,000-$10,999
                    7  - $11,000-$11,999
                    8  - $12,000-$12,999
                    9  - $13,000-$13,999
                    10 - $14,000-$14.999
                    11 - $15,000-$16,999
                    12 - $17,000-$19,999
                    13 - $20,000-$21,999
                    14 - $22,000-$24,999
                    15 - $25,000-$29,999
                    16 - $30,000-$34,999
                    17 - $35,000-$39,999
                    18 - $40,000-$44,999
                    19 - $45,000-$49,999
                    20 - $50,000-$59,999
                    21 - $60,000-$74,999
                    22 - $75,000-89,999
                    23 - $90,000-$104,999
                    24 - $105,000 and over
                vote - Expected vote
                    0 - Clinton
                    1 - Dole
                The following 3 variables all take the values:
                    1 - Extremely liberal
                    2 - Liberal
                    3 - Slightly liberal
                    4 - Moderate
                    5 - Slightly conservative
                    6 - Conservative
                    7 - Extremely Conservative
                selfLR - Respondent's self-reported political leanings from "Left"
                    to "Right".
                ClinLR - Respondents impression of Bill Clinton's political
                    leanings from "Left" to "Right".
                DoleLR  - Respondents impression of Bob Dole's political leanings
                    from "Left" to "Right".
                logpopul - log(popul + .1)
</code></pre></div>

The data itself is represented by a `Dataset` object that is returned by the `load_pandas()` function of the submodule.

```python
dataset_anes96 = anes96.load_pandas()
```

The `data` property of the `Dataset` object contains a `pandas` `DataFrame` with the data.


```python
df_anes96 = dataset_anes96.data
df_anes96.head()
```
```
 	popul 	TVnews 	selfLR 	ClinLR 	DoleLR 	PID 	age 	educ 	income 	vote 	logpopul
0 	0.0 	7.0 	7.0 	1.0 	6.0 	6.0 	36.0 	3.0 	1.0 	1.0 	-2.302585
1 	190.0 	1.0 	3.0 	3.0 	5.0 	1.0 	20.0 	4.0 	1.0 	0.0 	5.247550
2 	31.0 	7.0 	2.0 	2.0 	6.0 	1.0 	24.0 	6.0 	1.0 	0.0 	3.437208
3 	83.0 	4.0 	3.0 	4.0 	5.0 	1.0 	28.0 	6.0 	1.0 	0.0 	4.420045
4 	640.0 	7.0 	5.0 	6.0 	4.0 	0.0 	68.0 	6.0 	1.0 	0.0 	6.461624
```

So, if you know the submodule in which the dataset is stored (e.g., `anes96`), you can get the `DataFrame` with the data in just one line:

```python
sm.datasets.anes96.load_pandas().data
```

The table below lists all built-in datasets provided by Statsmodels and the corresponding submodules.

**Dataset Description** | **Submodule**
:-|:-
[American National Election Survey 1996](http://www.statsmodels.org/dev/datasets/generated/anes96.html) | anes96
[Breast Cancer Data](http://www.statsmodels.org/dev/datasets/generated/cancer.html) | cancer
[Bill Greene’s credit scoring data.](http://www.statsmodels.org/dev/datasets/generated/ccard.html) | ccard
[Smoking and lung cancer in eight cities in China.](http://www.statsmodels.org/dev/datasets/generated/china_smoking.html) | china_smoking
[Mauna Loa Weekly Atmospheric CO2 Data](http://www.statsmodels.org/dev/datasets/generated/co2.html) | co2
[First 100 days of the US House of Representatives 1995](http://www.statsmodels.org/dev/datasets/generated/committee.html) | committee
[World Copper Market 1951-1975 Dataset](http://www.statsmodels.org/dev/datasets/generated/copper.html) | copper
[US Capital Punishment dataset.](http://www.statsmodels.org/dev/datasets/generated/cpunish.html) | cpunish
[El Nino - Sea Surface Temperatures](http://www.statsmodels.org/dev/datasets/generated/elnino.html) | elnino
[Engel (1857) food expenditure data](http://www.statsmodels.org/dev/datasets/generated/engel.html) | engel
[Affairs dataset](http://www.statsmodels.org/dev/datasets/generated/fair.html) | fair
[World Bank Fertility Data](http://www.statsmodels.org/dev/datasets/generated/fertility.html) | fertility
[Grunfeld (1950) Investment Data](http://www.statsmodels.org/dev/datasets/generated/grunfeld.html) | grunfeld
[Transplant Survival Data](http://www.statsmodels.org/dev/datasets/generated/heart.html) | heart
[Longley dataset](http://www.statsmodels.org/dev/datasets/generated/longley.html) | longley
[United States Macroeconomic data](http://www.statsmodels.org/dev/datasets/generated/macrodata.html) | macrodata
[Travel Mode Choice](http://www.statsmodels.org/dev/datasets/generated/modechoice.html) | modechoice
[Nile River flows at Ashwan 1871-1970](http://www.statsmodels.org/dev/datasets/generated/nile.html) | nile
[RAND Health Insurance Experiment Data](http://www.statsmodels.org/dev/datasets/generated/randhie.html) | randhie
[Taxation Powers Vote for the Scottish Parliamant 1997](http://www.statsmodels.org/dev/datasets/generated/scotland.html) | scotland
[Spector and Mazzeo (1980) - Program Effectiveness Data](http://www.statsmodels.org/dev/datasets/generated/spector.html) | spector
[Stack loss data](http://www.statsmodels.org/dev/datasets/generated/stackloss.html) | stackloss
[Star98 Educational Dataset](http://www.statsmodels.org/dev/datasets/generated/star98.html) | star98
[Statewide Crime Data 2009](http://www.statsmodels.org/dev/datasets/generated/statecrime.html) | statecrime
[U.S. Strike Duration Data](http://www.statsmodels.org/dev/datasets/generated/strikes.html) | strikes
[Yearly sunspots data 1700-2008](http://www.statsmodels.org/dev/datasets/generated/sunspots.html) | sunspots

### Datasets from R

Besides the built-in datasets, Statsmodels provides access to 1173 datasets from the [Rdatasets project](https://github.com/vincentarelbundock/Rdatasets). The Rdataets project is a collection of datasets that were originally distributed with R and its add-on packages. To access a particular dataset you need its name and the name of the original R package. For example, the famous iris dataset, which is often used to demonstrate classification algorithms, can be accessed under the name "iris" and package "datasets". Calling the `get_rdataset()` function with these arguments downloads the corresponding dataset from the Rdatasets project's repository and returns it in a `Dataset` object:


```python
import statsmodels.api as sm
dataset_iris = sm.datasets.get_rdataset(dataname='iris', package='datasets')
```

The `__doc__` attribute of the `Dataset` object stores a detailed description of the dataset.


```python
print(dataset_iris.__doc__)
```
<div class="highlighter-rouge"><pre class="highlight" style="height: 20em;"><code>
    +--------+-------------------+
    | iris   | R Documentation   |
    +--------+-------------------+
    
    Edgar Anderson's Iris Data
    --------------------------
    
    Description
    ~~~~~~~~~~~
    
    This famous (Fisher's or Anderson's) iris data set gives the
    measurements in centimeters of the variables sepal length and width and
    petal length and width, respectively, for 50 flowers from each of 3
    species of iris. The species are *Iris setosa*, *versicolor*, and
    *virginica*.
    
    Usage
    ~~~~~
    
    ::
    
        iris
        iris3
    
    Format
    ~~~~~~
    
    ``iris`` is a data frame with 150 cases (rows) and 5 variables (columns)
    named ``Sepal.Length``, ``Sepal.Width``, ``Petal.Length``,
    ``Petal.Width``, and ``Species``.
    
    ``iris3`` gives the same data arranged as a 3-dimensional array of size
    50 by 4 by 3, as represented by S-PLUS. The first dimension gives the
    case number within the species subsample, the second the measurements
    with names ``Sepal L.``, ``Sepal W.``, ``Petal L.``, and ``Petal W.``,
    and the third the species.
    
    Source
    ~~~~~~
    
    Fisher, R. A. (1936) The use of multiple measurements in taxonomic
    problems. *Annals of Eugenics*, **7**, Part II, 179–188.
    
    The data were collected by Anderson, Edgar (1935). The irises of the
    Gaspe Peninsula, *Bulletin of the American Iris Society*, **59**, 2–5.
    
    References
    ~~~~~~~~~~
    
    Becker, R. A., Chambers, J. M. and Wilks, A. R. (1988) *The New S
    Language*. Wadsworth & Brooks/Cole. (has ``iris3`` as ``iris``.)
    
    See Also
    ~~~~~~~~
    
    ``matplot`` some examples of which use ``iris``.
    
    Examples
    ~~~~~~~~
    
    ::
    
        dni3 <- dimnames(iris3)
        ii <- data.frame(matrix(aperm(iris3, c(1,3,2)), ncol = 4,
                                dimnames = list(NULL, sub(" L.",".Length",
                                                sub(" W.",".Width", dni3[[2]])))),
            Species = gl(3, 50, labels = sub("S", "s", sub("V", "v", dni3[[3]]))))
        all.equal(ii, iris) # TRUE
</code></pre></div>

The `data` attribute stores a `pandas` `DataFrame` with the data:

```python
df_iris = dataset_iris.data
df_iris.head()
```
```
 	Sepal.Length 	Sepal.Width 	Petal.Length 	Petal.Width 	Species
0 	5.1 			3.5 			1.4 			0.2 			setosa
1 	4.9 			3.0 			1.4 			0.2 			setosa
2 	4.7 			3.2 			1.3 			0.2 			setosa
3 	4.6 			3.1 			1.5 			0.2 			setosa
4 	5.0 			3.6 			1.4 			0.2 			setosa
```


So, if you know the dataname and the package of a dataset (e.g., "iris" and "datasets"), you can download the data and get the corresponding `DataFrame` in just one line:

```python
sm.datasets.get_rdataset(dataname='iris', package='datasets').data
```

[This index](https://vincentarelbundock.github.io/Rdatasets/datasets.html) provides a complete overview of all datasets available in the Rdatasets repository with the corresponding datanames (the `item` column) and packages (the `package` column). The index is also available in the [CSV format](http://vincentarelbundock.github.com/Rdatasets/datasets.csv).

## Scikit-learn

[Scikit-learn's `datasets` module provides 7 built-in toy datasets](http://scikit-learn.org/stable/datasets/index.html) that are used in Scikit-learn's documentation for quick illustration of the algorithms, but are actually too small to be representative for real-world data. More interestingly, Scikit-learn also provides a set of random sample generators that can be used to generate artificial datasets of controlled size and complexity for different machine-learning problems.

### Built-in Toy Datasets

For each of the built-in datasets there is a load function that returns a `Bunch` object representing the dataset. For example, the Boston House Prices dataset can be loaded with the `load_boston()` function:


```python
from sklearn import datasets
dataset_boston = datasets.load_boston()
```

The `DESCR` attribute of the `Bunch` object stores a detailed description of the dataset:


```python
print(dataset_boston.DESCR)
```
<div class="highlighter-rouge"><pre class="highlight" style="height: 20em;"><code>
    Boston House Prices dataset
    ===========================
    
    Notes
    ------
    Data Set Characteristics:  
    
        :Number of Instances: 506 
    
        :Number of Attributes: 13 numeric/categorical predictive
        
        :Median Value (attribute 14) is usually the target
    
        :Attribute Information (in order):
            - CRIM     per capita crime rate by town
            - ZN       proportion of residential land zoned for lots over 25,000 sq.ft.
            - INDUS    proportion of non-retail business acres per town
            - CHAS     Charles River dummy variable (= 1 if tract bounds river; 0 otherwise)
            - NOX      nitric oxides concentration (parts per 10 million)
            - RM       average number of rooms per dwelling
            - AGE      proportion of owner-occupied units built prior to 1940
            - DIS      weighted distances to five Boston employment centres
            - RAD      index of accessibility to radial highways
            - TAX      full-value property-tax rate per $10,000
            - PTRATIO  pupil-teacher ratio by town
            - B        1000(Bk - 0.63)^2 where Bk is the proportion of blacks by town
            - LSTAT    % lower status of the population
            - MEDV     Median value of owner-occupied homes in $1000's
    
        :Missing Attribute Values: None
    
        :Creator: Harrison, D. and Rubinfeld, D.L.
    
    This is a copy of UCI ML housing dataset.
    http://archive.ics.uci.edu/ml/datasets/Housing
    
    
    This dataset was taken from the StatLib library which is maintained at Carnegie Mellon University.
    
    The Boston house-price data of Harrison, D. and Rubinfeld, D.L. 'Hedonic
    prices and the demand for clean air', J. Environ. Economics & Management,
    vol.5, 81-102, 1978.   Used in Belsley, Kuh & Welsch, 'Regression diagnostics
    ...', Wiley, 1980.   N.B. Various transformations are used in the table on
    pages 244-261 of the latter.
    
    The Boston house-price data has been used in many machine learning papers that address regression
    problems.   
         
    **References**
    
       - Belsley, Kuh & Welsch, 'Regression diagnostics: Identifying Influential Data and Sources of Collinearity', Wiley, 1980. 244-261.
       - Quinlan,R. (1993). Combining Instance-Based and Model-Based Learning. In Proceedings on the Tenth International Conference of Machine Learning, 236-243, University of Massachusetts, Amherst. Morgan Kaufmann.
       - many more! (see http://archive.ics.uci.edu/ml/datasets/Housing)
</code></pre></div>

The data itself is provided in form of two `numpy` arrays: one for the independent variables (`Bunch.data` attribute) and one for the dependent variables (`Bunch.target` attribute). The names of the features are stored in the `Bunch.feature_names` attribute. A `pandas` `DataFrame` can be easily constructed from a `numpy` array and a list of feature names:


```python
import pandas as pd

# Independent variables (i.e. features)
df_boston_features = pd.DataFrame(data=dataset_boston.data,
                                  columns=dataset_boston.feature_names)
df_boston_features.head()
```
```
CRIM 			ZN 		INDUS 	CHAS 	NOX 	RM 		AGE 	DIS 	RAD 	TAX 	PTRATIO B 		LSTAT
0 	0.00632 	18.0 	2.31 	0.0 	0.538 	6.575 	65.2 	4.0900 	1.0 	296.0 	15.3 	396.90 	4.98
1 	0.02731 	0.0 	7.07 	0.0 	0.469 	6.421 	78.9 	4.9671 	2.0 	242.0 	17.8 	396.90 	9.14
2 	0.02729 	0.0 	7.07 	0.0 	0.469 	7.185 	61.1 	4.9671 	2.0 	242.0 	17.8 	392.83 	4.03
3 	0.03237 	0.0 	2.18 	0.0 	0.458 	6.998 	45.8 	6.0622 	3.0 	222.0 	18.7 	394.63 	2.94
4 	0.06905 	0.0 	2.18 	0.0 	0.458 	7.147 	54.2 	6.0622 	3.0 	222.0 	18.7 	396.90 	5.33
```
<br>
```python
# Dependent variables (i.e. targets)
df_boston_target = pd.DataFrame(data=dataset_boston.target,
                                columns=['MEDV'])
df_boston_target.head()
```
```
 	MEDV
0 	24.0
1 	21.6
2 	34.7
3 	33.4
4 	36.2
```

The table below lists the built-in datasets in Scikit-learn and the corresponding load functions. Some of these datasets are also available in Statsmodels through Rdatasets project. The corresponding datanames and packages to access these datasets from Statsmodels are also listed.

**Description** | **scikit-learn** | **statsmodels**
:--|:--|:--
Boston house-prices dataset (regression)             | load_boston() 	    | dataname='Boston', package='MASS'
The iris dataset (classification)                    | load_iris() 	        | dataname='iris', package='datasets'
The diabetes dataset (regression)                    | load_diabetes() 	    | --
The digits dataset (classification)                  | load_digits() 	    | --
The Linnerud dataset (multivariate regression)       | load_linnerud() 	    | --
The wine dataset (classification)                    | load_wine() 	        | --
The breast cancer Wisconsin dataset (classification) | load_breast_cancer() | dataname='biopsy', package='MASS'

### Random Sample Generators

Besides the built-in datasets, the Scikit-learn's `datasets` module provides multiple generators that can generate random data for regression, classification, and clustering problems.

**`make_regression()`** generates a random regression problem. To generate a random regression problem with 5 samples, 4 features (2 of which are informative, that is, influence the target variable), and with 1 target variable run:


```python
X, y = datasets.make_regression(n_samples=5, n_features=4, n_informative=2, n_targets=1)
X, y
```
```
(array([[-0.42590826, -1.13659088, -1.12081439,  0.19618605],
        [-0.24469292,  1.49406562,  0.00402701,  0.0853733 ],
        [ 0.26415806, -0.89860911, -0.33905577, -0.51633174],
        [-1.9304862 ,  0.30020868,  0.76146937, -1.05332537],
        [ 0.41696969, -1.12000527,  0.70649028,  0.76996861]]),
 array([-64.48100936, -15.23036444,   5.17304557, -95.59148543,  49.97033047]))
```

**`make_classification()`** generates a random classification problem. To generate a random classification problem with 5 samples, 3 features (2 of which are informative and 1 is redundant), 2 classes, and with 1 cluster per class run:

```python
X, y = datasets.make_classification(n_samples=5, n_features=3, n_informative=2, n_redundant=1, n_classes=2, n_clusters_per_class=1)
X, y
```
```
(array([[ 1.12990679, -0.77494575, -0.33554705],
        [-1.16200073, -1.38196269,  1.07136609],
        [-0.28757222,  0.27740255,  0.05867687],
        [ 0.18949525,  0.60855967, -0.30244284],
        [ 1.65745753,  0.04606751, -0.88648095]]),
 array([1, 0, 0, 0, 1]))
```

**`make_blobs()`** generates a random clustering problem. To generate a random clustering problem with 5 samples, 3 centers, and 2 features run:

```python
X, y = datasets.make_blobs(n_samples=5, centers=3, n_features=2)
X, y
```
```
(array([[-0.1460543 ,  7.99240431],
        [-0.59781982,  5.73052323],
        [ 5.0929357 , -3.77332084],
        [ 4.56787662, -3.30370353],
        [ 7.89484287, -4.47653814]]),
 array([1, 1, 0, 0, 2]))
```

## Seaborn

Seaborn provides 13 datasets from its own [collection](https://github.com/mwaskom/seaborn-data/). The available datasets can be listed with the `get_dataset_names()` function:


```python
import seaborn as sns
sns.get_dataset_names()
```
```
    ['anscombe',
     'attention',
     'brain_networks',
     'car_crashes',
     'dots',
     'exercise',
     'flights',
     'fmri',
     'gammas',
     'iris',
     'planets',
     'tips',
     'titanic']
```

The data in a dataset can be accessed in form of a `pandas` `DataFrame` by calling the `load_dataset()` function with the name of the dataset as the argument:

```python
df_planets = sns.load_dataset('planets')
df_planets.head()
```
```
	method 			number 	orbital_period 	mass 	distance 	year
0 	Radial Velocity 	1 	269.300 		7.10 	77.40 		2006
1 	Radial Velocity 	1 	874.774 		2.21 	56.95 		2008
2 	Radial Velocity 	1 	763.000 		2.60 	19.84 		2011
3 	Radial Velocity 	1 	326.030 		19.40 	110.62 		2007
4 	Radial Velocity 	1 	516.220 		10.50 	119.47 		2009
```

Some datasets, such as anscombe and iris, seem to be from R collection and some are not. There is no any description of the datasets available. This reduces their usefulness.

## Summary

[`Statsmodels`](http://www.statsmodels.org), [`scikit-learn`](http://scikit-learn.org), and [`seaborn`](https://seaborn.pydata.org/) provide convenient access to a large number of datasets of different sizes and from different domains. In one or two lines of code the datasets can be accessed in a python script in form of a `pandas` `DataFrame`. This is particularly useful for quick experimenting with machine-learning algorithms and visualizations.

[Download this post as a Jupyter notebook](/resources/2017-12-26-Datasets_in_Python/Datasets_in_Python.ipynb)
