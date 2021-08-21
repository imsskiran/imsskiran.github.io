---
layout: post
title:  "Bias-Variance trade-off: The Untold story"
date:   2021-06-07 11:09:13 +0530
categories: statistics machine-learning data-science
published: true
hidden: true
upcoming: true
---
The bias-variance trade-off is a foundational concept omnipresent in the machine learning curricullums. In many such foundational courses, it is explained as an interpretation of the relationship between a model's complexity and the difference between its training and validation errors. Hoewever, without the background of Estimation Theory, this widely applied concept is often misinterpreted in practice. Hence, in this post let's look at the math behind the bias, the variance and their relationship with the expected error of an estimator from the first principles.

- Insert the cover pic here-

<h2>The Estimaton<h2>
Imagine that you are interested to compute the simple average of scores made by an active sportsperson in their career. As the player is still active, you would only have a subset of the enitre scores ever made until the player's retirement. So, you wanted to guess the true average using the set of scores available thus far, deeming it reasonable.

In Estimation Theory, the "score" is a <strong>variable</strong>, the "true average" is the unknown <strong>parameter</strong> of the variable", the "subset of scores" is called a <strong>sample</strong>, the act of "guessing from available scores" is called <strong>estimation</strong>, the guessed value is called an <strong>estimate</strong> and finally "deeming the guess reasonable" is termed as the <strong>accuracy</strong> of the estimate.

With the formal terms defined, let's highlight some facts about the estimation example described above:
* The scores could be different but the average of all scores is constant and unique. Hence, certain paramters such as mean and variance of a random variable are constant, unique and can be computed accurately only when all scores are available
* The value of your estimate from sample scores may change as you record new scores. Hence, the estimator is a variable that takes multiple values as the sample changes

As you are bound to make multiple guesses with accumulation of more scores, the accuracy of this guessing process from a sample has to be a function of all the guessed values. Let's look at a popular illustration to understand how the accuracy can be quantified:

- Insert bulls eye bias-variance illustration here/ or ms dhoni scores -

In case 1, the estimates are close to the true value and also to each other
In case 2, the estimates are close to the true value but are very different from each other
In case 3, the estimates are far from the true values but close to each other
In case 4, the estimates are far from the true values and also different from each other

The accuracy of the estimator can be a combination of the average distance to true value and the spread of the estimator values, formally known as expected value and variance of the estimator respectively.

- Insert expected value and variance expressions here - 

<h2>The Bias and the Variance</h2>
Now, the bias of an estimator is defined as the difference between its expected value and true value being estimated
- Insert bias expression here - 

The variance of an estimator is simply its variance
- Insert variance expression here - 

Now, if you could come up with multiple estimators, how to select the best among them? The Estimation Theory says, the most efficient estimator is:
* Unbiased
* Has the lowest variance among all unbiased estimators
* Unique

Unbiased estimator will have its expected value matching with true value. The unbiased estimator with lowest variance will have estimates values close to each and hence close to the expected value, indicating that you are guessing right on an average and all your guesses are not too far from the true value. 

So the model with highest accuracy shall have apparently no bias and small variance. Then why is there a bias-variance trade-off?

<h2>The trade-off</h2>
