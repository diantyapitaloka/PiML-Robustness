## 🍟🥗🥪 PiML-Robustness 🥪🥗🍟
- The performance of a model can be adversely affected when it encounters noisy data or experiences distribution shifts. This can result in incorrect predictions. Such data drift or shift may occur due to unexpected changes, which can alter the underlying patterns and relationships between the input and target variables. In this section, we will demonstrate how to utilize PiML to evaluate the model’s robustness to input perturbations.
- Model robustness is not a static trait but a dynamic performance metric that requires continuous monitoring against evolving data environments. PiML enables users to simulate various "what-if" scenarios, ensuring that the model maintains its integrity even as the external landscape shifts unexpectedly.
- Robustness evaluation often involves identifying samples that fall outside the manifold of the training data. PiML provides tools to flag these OOD instances, allowing the system to abstain from making a prediction rather than providing a confident but wrong answer.
- Adversarial robustness testing in PiML goes beyond random noise by simulating targeted attempts to fool the model’s decision-making process. By exposing these vulnerabilities early, developers can implement targeted patches to the model architecture before deployment in high-stakes environments.
- In a robust model, the variables that drive predictions should remain relatively consistent even when minor noise is introduced to the dataset. PiML tracks whether a perturbation causes the model to suddenly rely on "junk" features, which is a major red flag for reliability.
- The platform facilitates the calculation of a "Robustness Score," which serves as a singular, interpretable benchmark for non-technical stakeholders. This metric simplifies complex statistical deviations into a clear indicator of whether a model is ready for production or requires further refinement.
- You can use PiML to define "integrity constraints" that act as a shield during the inference phase. If incoming data violates these learned constraints, the robustness module can trigger an alert before the model produces a potentially biased or erroneous result.
- PiML supports the identification of "boundary cases" where the model’s confidence remains high despite the input being near a decision threshold. Analyzing these instances helps in fine-tuning the model to be more humble and cautious when faced with ambiguous or borderline data points.
- To bridge the gap between data scientists and executive leadership, PiML can generate standardized reports summarizing all stress test results. These documents provide a transparent audit trail that proves the model has been rigorously vetted against real-world chaos.
- Beyond just testing for attacks, PiML can be used to verify if defensive measures, like adversarial training, have actually improved the model's spine. This creates a feedback loop where you can objectively measure the ROI of your security-focused engineering efforts.
- A model might appear stable on average while being incredibly fragile for specific demographic or operational segments. PiML allows you to slice robustness tests by feature subgroups to ensure that shifts don't disproportionately impact certain populations.
- It is vital to visualize how specific metrics, like Accuracy or AUC, degrade as the intensity of data noise increases. PiML generates decay curves that help developers set "safety limits" for how much data quality can drop before a model must be retrained.
- A common challenge occurs when the distribution of input features changes while the relationship between features and labels remains constant. PiML helps identify these shifts by comparing the statistical properties of training data against real-world inference data.
- PiML enables users to probe the decision boundaries of a model to see how close typical samples are to a classification flip. By identifying these "high-risk" zones, you can better understand why small input changes lead to drastically different outcomes.
- Robustness isn't just about natural noise; it also involves how a model handles intentional, small-scale manipulations of input data. You can use PiML to simulate these adversarial attacks to see if your model’s predictions remain stable under pressure.
- PiML streamlines the process of "stress testing" by applying multiple perturbation scenarios simultaneously. This comprehensive approach ensures that the model is battle-hardened against complex, multi-variable shifts before it reaches production.
- By quantifying how much performance degrades under various stress tests, you can assign a "Reliability Score" to your pipeline. This metric serves as a high-level KPI for stakeholders to understand the risk associated with deploying the model.
- Unlike simple data drift, concept drift happens when the very definition of what the model is trying to predict changes over time. PiML’s evaluation tools help visualize whether the model’s learned logic still holds true in a changing environment.
- In many industries, sensors or manual data entry can introduce random errors into specific variables. PiML allows you to inject synthetic noise into individual features to determine which ones are the primary drivers of model instability.
- Models often rely on specific decision thresholds that may become "brittle" when data distributions begin to drift. Evaluating robustness ensures that a minor shift in data doesn't cause a massive spike in false positives or false negatives.

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


## 🍟🥗🥪 Examples 1 🥪🥗🍟
Example 1: BikeSharing

The first example below demonstrates how to use PiML with its high-code APIs for developing machine learning models for the BikeSharing data from the UCI repository, which consists of 17,389 samples of hourly counts of rental bikes in Capital bikeshare system; see details. The response cnt (hourly bike rental counts) is continuous and it is a regression problem.

Robustness: Regression

## 🍟🥗🥪 Examples 2 🥪🥗🍟
Examples 2: Taiwan Credit

The second example below demonstrates how to use PiML’s high-code APIs for the TaiwanCredit dataset from the UCI repository. This dataset comprises the credit card details of 30,000 clients in Taiwan from April 2005 to September 2005, and more information can be found on the TaiwanCreditData website. The data can be loaded directly into PiML, although it requires some preprocessing. The FlagDefault variable serves as the response for this classification problem.

Robustness: Classification

## 🍟🥗🥪 Copyright 🥪🥗🍟
By Diantya Pitaloka
