## 🍟🥗🥪 PiML-Robustness 🥪🥗🍟## 
The performance of a model can be adversely affected when it encounters noisy data or experiences distribution shifts. This can result in incorrect predictions. Such data drift or shift may occur due to unexpected changes, which can alter the underlying patterns and relationships between the input and target variables. In this section, we will demonstrate how to utilize PiML to evaluate the model’s robustness to input perturbations.

## 🍟🥗🥪 Algorithm Details 🥪🥗🍟## 
The robustness test assesses model performance to small changes in the covariate space. It proceeds as follows.

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/ba736658-3c4a-4ca2-92b7-e0711cb60e32)

This process is iterated ten times for all the test samples, with performance metrics recorded for each repetition. It is important to note that the assumption is made that the response remains unchanged throughout. Perturbation can be applied to both numerical and categorical features. The forthcoming sections will illustrate the perturbation methods for numerical and categorical features, respectively.

## 🍟🥗🥪 Perturbation For Numerical Features 🥪🥗🍟## 
For numerical features, we provide the following two perturbation options.

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/8c7ee2c7-fb73-4668-b5f9-7a90eee07cee)

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/fd1339ce-0386-4027-a9bd-887b6ad36797)

Let’s take into account a data point with a value of 3, along with its corresponding quantile value of 0.7. On the quantile scale, a small noise of 0.12 is generated and added to the original quantile value of 0.7. This sum yields a resulting value of 0.82, which is then rounded to the nearest available value, namely 0.8. Finally, the perturbed quantile is transformed back to the original scale, resulting in a value of 40.

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 A 🥪🥗🍟## 

## 🍟🥗🥪 Copyright 🥪🥗🍟## 
By Diantya Pitaloka
