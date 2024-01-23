## 🍟🥗🥪 PiML-Robustness 🥪🥗🍟
The performance of a model can be adversely affected when it encounters noisy data or experiences distribution shifts. This can result in incorrect predictions. Such data drift or shift may occur due to unexpected changes, which can alter the underlying patterns and relationships between the input and target variables. In this section, we will demonstrate how to utilize PiML to evaluate the model’s robustness to input perturbations.

## 🍟🥗🥪 Algorithm Details 🥪🥗🍟
The robustness test assesses model performance to small changes in the covariate space. It proceeds as follows.

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/ba736658-3c4a-4ca2-92b7-e0711cb60e32)

This process is iterated ten times for all the test samples, with performance metrics recorded for each repetition. It is important to note that the assumption is made that the response remains unchanged throughout. Perturbation can be applied to both numerical and categorical features. The forthcoming sections will illustrate the perturbation methods for numerical and categorical features, respectively.

## 🍟🥗🥪 Perturbation For Numerical Features 🥪🥗🍟
For numerical features, we provide the following two perturbation options.

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/8c7ee2c7-fb73-4668-b5f9-7a90eee07cee)

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/fd1339ce-0386-4027-a9bd-887b6ad36797)

Let’s take into account a data point with a value of 3, along with its corresponding quantile value of 0.7. On the quantile scale, a small noise of 0.12 is generated and added to the original quantile value of 0.7. This sum yields a resulting value of 0.82, which is then rounded to the nearest available value, namely 0.8. Finally, the perturbed quantile is transformed back to the original scale, resulting in a value of 40.

## 🍟🥗🥪 Perturbation for Categorical Variable 🥪🥗🍟

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/f0ca875e-ee1e-4cf2-858b-10c05368e767)


## 🍟🥗🥪 Usage 🥪🥗🍟
To perform a robustness test using the model_diagnose function, you have two options: “robustness_perf” and “robustness_perf_worst”. The former evaluates the model’s robustness under perturbation overall testing samples, while the latter only assesses the model’s robustness on the worst test samples. The following arguments are required to run the robustness test:

1. perturb_method: This parameter determines the perturbation method for numerical features. The default option is “raw”, which involves adding normal noise to the covariates for perturbation. Alternatively, you can choose “quantile”, which perturbs the data in the quantile scale.
2. perturb_features: Specify the features to be perturbed. By default, this is set to None, which means all features will be perturbed. You can also provide a list of feature names if you only want to perturb selected features.
3. perturb_size: This parameter represents the perturbation step or magnitude. It determines the amount of perturbation applied to the data.
4. metric: Select the performance metric to be used for evaluation. Supported metrics depend on the type of task. For binary classification, the options are “ACC” (accuracy), “AUC” (Area Under the Curve), and “F1” (F1 score). For regression tasks, the options are “MSE” (Mean Squared Error), “MAE” (Mean Absolute Error), and “R2” (R-squared).
5. alpha: This parameter specifies the proportion of worst samples to consider when evaluating the performance against perturbation sizes.

As an illustrative example, let’s consider a FIGS model applied to the BikeSharing dataset.

## 🍟🥗🥪 Robustness on the whole test sample 🥪🥗🍟
To assess the models’ performance against noise, we set the parameter show to “robustness_perf”.

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/bf3ddf4c-ecc1-4593-88a7-8d7fdb782c70)

In the figure above, the x-axis represents the noise level, indicating the magnitude of perturbation applied to the data. The y-axis displays the test set performance of the model after perturbation. The box plot illustrates the results obtained from ten repetitions of the experiment. When the noise level is set to 0.0, there is no perturbation applied, resulting in no variation in the model’s performance. As the noise level increases, we observe a degradation in the model’s performance, which is expected. The full plot captures the model’s performance at each noise level, providing an overview of how the model’s performance changes with increasing perturbation.

In the second example, we will specifically perturb two features: hr and atemp. The remaining settings will be kept the same as in the first example. This means we will use the same perturbation method, perturbation step, and performance metric. By perturbing a smaller number of features, the observed degradation in model performance is expected to be smaller compared to the first example where all features were perturbed.

![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/ff7b9a25-383a-41bb-8637-ffa3f46da4e5)

In summary, these plots can be used to assess model robustness under different input perturbation settings, as illustrated in the examples above. The extent to which a model’s performance drops under input perturbation serves as an indication of its robustness. A robust model will exhibit minimal performance degradation when subjected to perturbations.

## 🍟🥗🥪 Robustness on worst test samples 🥪🥗🍟
In addition to the robustness test on all test samples, we can also test model robustness on worst-performing test samples. To achieve this, we will identify the top 
 (alpha=0.3) of test samples with the largest absolute residuals. These samples are considered the worst-performing because they have the highest discrepancies between the predicted values and the actual values. Next, we will apply the perturbations to these samples. The perturbation method and perturbation step will remain the same as previously discussed.

 ![image](https://github.com/diantyapitaloka/PiML-Robustness/assets/147487436/16217a4a-631f-43a8-b18f-19297018d509)

 The x-axis shows the noise level (perturbation size), and the y-axis is the model performance (MSE). Under perturbation, we observe that the worst test sample performance is much worse than that of the full test sample. The drop in model performance also increases with the increase in noise level. This plot tells us how poorly the model may perform under the input perturbation and worst cases.


## 🍟🥗🥪 Examples 🥪🥗🍟
Example 1: BikeSharing

The first example below demonstrates how to use PiML with its high-code APIs for developing machine learning models for the BikeSharing data from the UCI repository, which consists of 17,389 samples of hourly counts of rental bikes in Capital bikeshare system; see details. The response cnt (hourly bike rental counts) is continuous and it is a regression problem.

Robustness: Regression

Examples 2: Taiwan Credit

The second example below demonstrates how to use PiML’s high-code APIs for the TaiwanCredit dataset from the UCI repository. This dataset comprises the credit card details of 30,000 clients in Taiwan from April 2005 to September 2005, and more information can be found on the TaiwanCreditData website. The data can be loaded directly into PiML, although it requires some preprocessing. The FlagDefault variable serves as the response for this classification problem.

Robustness: Classification

## 🍟🥗🥪 Copyright 🥪🥗🍟## 
By Diantya Pitaloka
