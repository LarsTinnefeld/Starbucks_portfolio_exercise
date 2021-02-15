# Starbucks Portfolio Exercise
An optimization strategy based on ML prediction and statistical evaluation

**Lars Tinnefeld**, 2021-02-07

![Starbucks](https://opj.ca/wp-content/uploads/2018/02/New-Starbucks-Logo-1200x969.jpg)

## Table of content
1. [About Starbucks (Business understanding)](#business_understanding)
2. [Objectives](#objectives)
3. [Approach](#approach)
4. [Data](#data)
5. [Data preparation](#preparation)
6. [Statistical evaluation of the experiment](#ab_test)
7. [Data Modelling](#modelling)
8. [Evaluation](#evaluation)

## About Starbucks <a name="business_understanding"></a>
Starbucks Corporation is an American multinational chain of coffeehouses and roastery reserves headquartered in Seattle, Washington. As the world's largest coffeehouse chain, Starbucks is seen to be the main representation of the United States' second wave of coffee culture. Source: [Wikipedia](https://en.wikipedia.org/wiki/Starbucks).

## Objectives <a name="objectives"></a>
The task on hand orginates from a take-home assignment provided by Starbucks and was a portfolio excercise in Udemy's Data Science Nanodegree Program.
In this assignment Starbucks defines an experiment in which a selection algorithm for an advertising promotion was to be developed and evaluated.
In particular, this algorithm should predict which customers are more likely affected by a promotion to buy a specific $10-product. Each promotion costs $0.15, which is an important evaluation metric. Beside the algorithm it needed to be evaluated if the method generated suficient significance to proves the effectiveness of the method. The tasks in detail are:

**Task 1)**

Analyze the results of the experiment and identify the effect of the treatment on product purchase and Net Incremental Revenue (NIR).

**Task 2)**

Build a model to select the best customers to target that maximizes the Incremental Response Rate (IRR) and Net Incremental Revenue (NIR).

## Approach <a name="approach"></a>
At the beginning of the exercise it is necessary to investigate if the data is imbalanced. This is required to identify potential causes for wrong or misleading results.

For the evaluation of the analysis two metrics were defined:

**Incremental Response Rate (IRR)**

<a href="https://www.codecogs.com/eqnedit.php?latex=IRR&space;=&space;\frac{purch_{treat}}{cust_{treat}}&space;-&space;\frac{purch_{ctrl}}{cust_{ctrl}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?IRR&space;=&space;\frac{purch_{treat}}{cust_{treat}}&space;-&space;\frac{purch_{ctrl}}{cust_{ctrl}}" title="IRR = \frac{purch_{treat}}{cust_{treat}} - \frac{purch_{ctrl}}{cust_{ctrl}}" /></a>

**Net Incremental Revenue (NIR)**

<a href="https://www.codecogs.com/eqnedit.php?latex=NIR&space;=&space;\left&space;(&space;10&space;*&space;purch_{treat}&space;-&space;0.15&space;*&space;cust_{treat}&space;\right&space;)&space;-&space;10&space;*&space;purch_{ctrl}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?NIR&space;=&space;\left&space;(&space;10&space;*&space;purch_{treat}&space;-&space;0.15&space;*&space;cust_{treat}&space;\right&space;)&space;-&space;10&space;*&space;purch_{ctrl}" title="NIR = \left ( 10 * purch_{treat} - 0.15 * cust_{treat} \right ) - 10 * purch_{ctrl}" /></a>


**Approach for task 1)**

Calculating IRR and NIR show if there is impact (IRR) and if this impact would lead to a benefitial outcome (NIR). Further, a statistical method to prove that there is sufficient significance for the validation of the test result will be needed. This was not directly part of the original task but is required in my view in order to statistically prove if the experiment results have enough evidence to be valid. For this, a 95% confidence interval needs to be defined (right-sided in this case).


**Approach for task 2)**

The available dataset is used to define and flag the trarget group (customers who received the promotional offer and also purchased) as a new feature in the dataset. This new feature represents the binary target variable "y", while the 7 additional features are used as input variables "X". This represet the training dataset for machine learning classifiers in order to predict good candidates. Following classifiers are used to optimize the results:
- Support Vector Machine
- Naive Bayes
- Random Forest

Each of the results needs to be evaluated with an error matrix and classification metrics (precision, recall and f1-score on a per-class basis).

## Data <a name="data"></a>

RangeIndex: 84534 entries, 0 to 84533
Data columns (total 10 columns):

| # |  Column | Non-Null Count | Dtype |
| --- | --- | --- | --- |
| 0 | ID | 84534 non-null | int64 |
| 1 | Promotion | 84534 non-null | object |
| 2 | purchase | 84534 non-null | int64 |
| 3 | V1 | 84534 non-null | int64 |
| 4 | V2 | 84534 non-null | float64 |
| 5 | V3 | 84534 non-null | float64 |
| 6 | V4 | 84534 non-null | int64 |
| 7 | V5 | 84534 non-null | int64 |
| 8 | V6 | 84534 non-null | int64 |
| 9 | V7 | 84534 non-null | int64 |


## Data preparation <a name="preparation"></a>
A check proved that the data came in as clean dataset (no missing values or outliers).

**Investigating Imbalace**

When comparing the sizes of the groups of people that purchased versus people that didn't purchase, it becomes clear that there is an imbalance that likely can affect the classifier.

![Countplot](https://github.com/LarsTinnefeld/Starbucks_portfolio_exercise/blob/main/Imbalance.png?raw=true)

The statitistical prove of the significance (s. notebook for code):

- **Z-score: 15.9**
- **P-value: 0.0**

With those values there is not question that the imbalance is significant. That is in line with the visual representation of the bar charts above.


## Statistical evaluation of the experiment <a name="ab_test"></a>
For the validation of the experiment outcome statistical hypothesis testing was used. The compared proportions were the purchase rates for each group.

**Purchase proportion of control group:**

<a href="https://www.codecogs.com/eqnedit.php?latex=p_{control}&space;=&space;\frac{n_{purch,control}}{n_{control}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_{control}&space;=&space;\frac{n_{purch,control}}{n_{control}}" title="p_{control} = \frac{n_{purch,control}}{n_{control}}" /></a>

**Purchase proportion of treated group:**

<a href="https://www.codecogs.com/eqnedit.php?latex=p_{treat}&space;=&space;\frac{n_{purch,treat}}{n_{treat}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_{treat}&space;=&space;\frac{n_{purch,treat}}{n_{treat}}" title="p_{treat} = \frac{n_{purch,treat}}{n_{treat}}" /></a>

**Pooled proportion:**

<a href="https://www.codecogs.com/eqnedit.php?latex=p_{treat}&space;=&space;\frac{n_{purch,treat}&space;&plus;&space;n_{purch,control}}{n_{treat}&space;&plus;&space;n_{treat}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?p_{pool}&space;=&space;\frac{n_{purch,treat}&space;&plus;&space;n_{purch,control}}{n_{treat}&space;&plus;&space;n_{treat}}" title="p_{treat} = \frac{n_{purch,treat} + n_{purch,control}}{n_{treat} + n_{treat}}" /></a>

**Standard error:**

<a href="https://www.codecogs.com/eqnedit.php?latex=S_{e}&space;=&space;\sqrt{p_{pool}&space;*&space;\left&space;(&space;1&space;-&space;p_{pool}&space;\right)&space;*&space;(\frac{1}{n_{control}}&space;-&space;\frac{1}{n_{treat}})}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?S_{e}&space;=&space;\sqrt{p_{pool}&space;*&space;\left&space;(&space;1&space;-&space;p_{pool}&space;\right)&space;*&space;(\frac{1}{n_{control}}&space;-&space;\frac{1}{n_{treat}})}" title="S_{e} = \sqrt{p_{pool} * \left ( 1 - p_{pool} \right) * (\frac{1}{n_{control}} - \frac{1}{n_{treat}})}" /></a>


**Z-score:**

<a href="https://www.codecogs.com/eqnedit.php?latex=Z&space;=&space;\frac{p_{control}&space;-&space;p_{treat}}{S_{e}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Z&space;=&space;\frac{p_{control}&space;-&space;p_{treat}}{S_{e}}" title="Z = \frac{p_{control} - p_{treat}}{S_{e}}" /></a>

The calculated z-score is **12.47**. This is an extreme high value. It is not required to calculate the p-value. The resulting p-value for the alternative hypothesis will be close to 0. This means that there is almost no evidence that the experiment result can be explained by the control group statistic (Null hypothesis rejected). The experiment result is statistically significant and a good base for further analysis.

**IRR: 0.009**

**NIR: -2334.6**

**Anser to Task 1)**

**IRR shows that there is an observable impact of the experiment. Hypothesis testing proves that the experiment results are statistically significant. The experiment has therefore an measurable impact. NIR shows a negative number. This means that the experiment impact is not big enough to result in a monetary benefit.**


## Data modelling <a name="modelling"></a>
The data were split into two dataframes:
- y: The new binomial (1/0) feature (group which has purchase and treat True)
- X: Features V1 to V7

---
**Support Vector Machine**

The classifier was setup with the default settings and trained with the data.
Resulting confusion matrix:

|     | Predicted: No | Predicted: Yes |
| --- | --- | --- |
| **Actual: Yes** | 83813 | 0 |
| **Actual: No** | 721 | 0 |

Classification report:

|     | Precision | Recall | F1-score | Support |
| --- | --- | --- | --- | --- |
| **0** | 0.99 | 1.00 | 1.00 | 83534 |
| **1** | 0.00 | 0.00 | 0.00 | 721 |
| **accuracy** |  |  | 0.99 | 84534 |
| **macro avg** | 0.50 | 0.50 | 0.50 | 84534 |
| **weighted avg** | 0.98 | 0.99 | 0.99 | 84534 |

**This result is shows, that the model is not predicting correctly. All predictions are negative.**

---
**Naive Bayes Classifier**

The classifier was setup with the default settings and trained with the data.
Resulting confusion matrix:

|     | Predicted: No | Predicted: Yes |
| --- | --- | --- |
| **Actual: Yes** | 83813 | 0 |
| **Actual: No** | 721 | 0 |

Classification report:

|     | Precision | Recall | F1-score | Support |
| --- | --- | --- | --- | --- |
| **0** | 0.99 | 1.00 | 1.00 | 83534 |
| **1** | 0.00 | 0.00 | 0.00 | 721 |
| **accuracy** |  |  | 0.99 | 84534 |
| **macro avg** | 0.50 | 0.50 | 0.50 | 84534 |
| **weighted avg** | 0.98 | 0.99 | 0.99 | 84534 |

**This result is exactly the same. All predictions are negative.**

---
**Random Forest**

The classifier was setup with the default settings and trained with the data.
Resulting confusion matrix:

|     | Predicted: No | Predicted: Yes |
| --- | --- | --- |
| **Actual: Yes** | 83813 | 0 |
| **Actual: No** | 721 | 0 |

Classification report:

|     | Precision | Recall | F1-score | Support |
| --- | --- | --- | --- | --- |
| **0** | 0.99 | 1.00 | 1.00 | 83534 |
| **1** | 0.00 | 0.00 | 0.00 | 721 |
| **accuracy** |  |  | 0.99 | 84534 |
| **macro avg** | 0.50 | 0.50 | 0.50 | 84534 |
| **weighted avg** | 0.98 | 0.99 | 0.99 | 84534 |

**Same result, all predictions are negative. This proves that there is a fundamental problem with the data. I assume that this is the result of the above discovered imbalance in the data.**

The effect of imbalanced data can be best seen in the below chart. Samples from C0 always have a higher probability than C1. This is the reason why all of the above used models always predict 0. For more information on imbalanced data check [Baptiste Rocca's article in Towards Data Science](https://towardsdatascience.com/handling-imbalanced-datasets-in-machine-learning-7a0e84220f28).

![Chart](https://miro.medium.com/max/1000/1*XASKuQuNP6ynLvKBN3TkyQ.jpeg)

*Chart: Baptiste Rocca*


![Chart_2](https://miro.medium.com/max/700/1*4YVk2qmNam23rcX1xuyx7Q.jpeg)

*Chart: Baptiste Rocca

---
**Dealing with imbalanced data**

I will try three methods:
- Upsampling
- Downsampling
- AUROC (Area Under ROC Curve)

---
**Upsampling**

I'm using the `resampling` method in `sklearn's utils` class to scale the minority group (our target class) up to the level of the majority group.

Applying the new dataset to the Naive Bayes classifier:

Resulting confusion matrix:

|     | Predicted: No | Predicted: Yes |
| --- | --- | --- |
| **Actual: Yes** | 27047 | 56766 |
| **Actual: No** | 95 | 626 |

Classification report:

|     | Precision | Recall | F1-score | Support |
| --- | --- | --- | --- | --- |
| **0** | 1.00 | 0.32 | 0.49 | 83534 |
| **1** | 0.01 | 0.87 | 0.02 | 721 |
| **accuracy** |  |  | 0.33 | 84534 |
| **macro avg** | 0.50 | 0.60 | 0.25 | 84534 |
| **weighted avg** | 0.99 | 0.33 | 0.48 | 84534 |

**Recall and F1 score for both categories is low. Precision for positive class is very low. This better than before but still not a good approach.**

---
**Downsampling**

I'm using the `resampling` method in `sklearn's utils` class to scale the majority group down to the level of the minority group.

Applying the new dataset to the Naive Bayes classifier:

Resulting confusion matrix:

|     | Predicted: No | Predicted: Yes |
| --- | --- | --- |
| **Actual: Yes** | 30654 | 53159 |
| **Actual: No** | 113 | 608 |

Classification report:

|     | Precision | Recall | F1-score | Support |
| --- | --- | --- | --- | --- |
| **0** | 1.00 | 0.37 | 0.54 | 83534 |
| **1** | 0.01 | 0.84 | 0.02 | 721 |
| **accuracy** |  |  | 0.37 | 84534 |
| **macro avg** | 0.50 | 0.60 | 0.28 | 84534 |
| **weighted avg** | 0.99 | 0.37 | 0.53 | 84534 |

**This result is not much better.**

---
**AUROC (Area Under ROC Curve)**

I'm using the `roc_auc_score` method in `sklearn's metrics` class to evaluate the outcome.

**Modified data: Score 0.633**

**Original data: Score 0.638**

There is no good effect on the process. I will go with the updampling method. The result can be optimized by balancing the degree of scaling but in general this would be the model we will chose for now.

**Anser to Task 2)**

**We greated a process to deal with the imbalanced data and predict customers which are better candidats to target with a promotion event. There is still some more work to do, because the predition results are not optimal. But as the challenges are defined we know how to address them.**
