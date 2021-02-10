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
6. [Data Modelling](#modelling)
7. [Evaluation](#evaluation)
8. [References and links](#references)

## About Starbucks <a name="business_understanding"></a>
Starbucks Corporation is an American multinational chain of coffeehouses and roastery reserves headquartered in Seattle, Washington. As the world's largest coffeehouse chain, Starbucks is seen to be the main representation of the United States' second wave of coffee culture. Source: [Wikipedia](https://en.wikipedia.org/wiki/Starbucks).

## Objectives <a name="objectives"></a>
The task on hand orginates from a take-home assignment provided by Starbucks and was a portfolio excercise in Udemy's Data Science Nanodegree Program.
In this assignment Starbucks defines an experiment in which a selection algorithm for an advertising promotion was to be developed and evaluated.
In particular, this algorithm should predict which customers are more likely affected by a promotion to buy a specific $10-product. Each promotion costs $0.15, which is an important evaluation metric. Beside the algorithm it needed to be evaluated if the method generated suficient significance to proves the effectiveness of the method.

## Approach <a name="approach"></a>
As metric for the evaluation two rates were defined:

$$IRR = \frac{purch_{treat}}{cust_{treat}} - \frac{purch_{ctrl}}{cust_{ctrl}}$$
