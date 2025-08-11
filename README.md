# Determinants of Happiness: Analyzing the 2015 World Happiness Data

# Table of Contents
- [Project Overview](#project-overview)
- [Data and Statistical Software](#data-and-statistical-software)
- [ETL](#etl)
- [Data Analysis and Results](#data-analysis-and-results)
- [Conclusion and Recommendation](#conclusion-and-recommendation)


## Project Overview
This project was intended to analyze the world happiness data and produce a report to inform policy making. This objective was achieved by extracting, cleaning, wrangling, analyzing, and interpreting the results from the data. The stakeholders include public policy makers as well as various government officials. This project was intended to address the following questions:

- What is the relationship between Freedom and Happiness score?
- What is the relationship between corruption and Happiness score?
- What is the relationship between Life expectancy and Happiness score?
- What is the average happiness score per region?
- What is the effect of the predictors on the outcome variable, happiness?
---

## Data and Statistical Software
The dataset for the analysis was sourced from World Happiness Report. The dataset is stored in Kaggle. The analysis was based on the data for the year 2015. The happiness scores and ranking use data from the Gallup World Pool. RStudio will be used to analyse the data because of the following reasons:

- With a given dataset, any analysis made with R can be reproduced at any point in time by the managers or any other person interested in verifying the authenticity of the results.
- R comes with several packages which aid in all aspects of analysis ranging from descriptive analysis, inferential analysis, as well as making visualization.
- Moreover, R software is suitable for handling large datasets.

## ETL
The following tasks were performed to understand and prepare the data for analysis:
- Loading the data and inspecting the data using functions like ```summary()```, ```str()```, ```psych::describe()```, ```read()```, ```tail()```, etc.
- ```sum(is.na())``` was used to check for any missing value in the data.
- The number of ```countries``` per ```Region``` was computed and visualized using a bar chart. This is shown below: 
<img width="815" height="483" alt="image" src="https://github.com/user-attachments/assets/977c4609-6c04-4cf6-a28a-79e9d8e4338e" />

- Given that countries are nested in Regions, a unique ID was generated for each Region to aid in further statistical modelling.
- A box_plot was then created to visualize the dsitribution of happiness per Region.
<img width="701" height="484" alt="image" src="https://github.com/user-attachments/assets/992d89dd-ecab-49b3-95ed-fa6989746b1c" />

- ```geom_hist()``` from  ```ggplot``` was used to examine the distribution of the happiness score, the outcome variable.
<img width="735" height="481" alt="image" src="https://github.com/user-attachments/assets/c136e693-4705-4eda-aec8-1a471e180038" />

  - The bar graph it could be observed that the Region with the highest number of countries is Sub-Saharan Africa, and the Region with the lowest number of countries in the data is Australia and New Zealand.
  - From the box plot, it can be observed that Sub-Saharan African Region has the lowest level happiness, whiles Australia and New Zealand, Western Europe, and North America had the higher levels of happiness.

## Data Analysis and Results
To address the first three questions, correlation coefficients were computed and the relationship between the predictors were visualized using scatterplots.

- What is the relationship between Freedom and Happiness score?
<img width="677" height="479" alt="image" src="https://github.com/user-attachments/assets/2d256d75-1a94-4ace-a3b6-549ca5ca50f9" />

From the scatter plot above, it can be observed that there exists a positive correlation between Freedom and Happiness score across all Regions except Eastern Asia. That is, the higher the level of freedom, the higher the happiness score. By breaking the graph down by ```Regions```, it was found that surprisingly, there is an inverse relationship between freedom and happiness for Eastern Asia. It should however be noted that Eastern Asia is among the ```Regions``` with few observations (i.e., countries) in the dataset. The correlation coefficient for the entire data is 0.57, indicating a moderate positive correlation between Freedom and Happiness scores.

- What is the relationship between corruption and Happiness score?
<img width="678" height="475" alt="image" src="https://github.com/user-attachments/assets/5c229ca7-287a-4eb4-85a2-e8c9a311dc04" />

From the scatter plot above, it appears that there exists a weak correlation between corruption and happiness. The correlation coefficient of 0.40 for the entire dataset indicates a weak positive correlation between corruption and happiness.

- What is the relationship between Life expectancy and Happiness score?
<img width="672" height="470" alt="image" src="https://github.com/user-attachments/assets/a300e514-f7d2-482b-8144-c86a69567e54" />

From the scatter plot above, it appears that there exists a strong positive correlation between Life expectancy and Happiness score. Also, by breaking the scatter plot down by ```Regions```, it could be observed that apart from *Western Europe*, and *Central and Eastern Europe* which showed almost no correlation between life expectancy and happiness, a relatively strong positive correlation between the two variables was across all te other `Regions`. This is supported by a high correlation coefficient of 0.72.

- What is the average happiness score per region?
<img width="917" height="403" alt="image" src="https://github.com/user-attachments/assets/ef6d1eca-f1ee-408b-b5ce-33e95b63ff3d" />

<img width="660" height="480" alt="image" src="https://github.com/user-attachments/assets/3dfca57f-1b88-4972-8914-e33a61cea153" />

The table and graph above show that the `Region` with the highest average happiness score is “Australia and New Zealand” while the `Region` with the lowest average happiness score is “Sub-Saharan Africa”.

- What is the effect of the predictors on the outcome variable, happiness?
<img width="919" height="602" alt="image" src="https://github.com/user-attachments/assets/4cb80c56-f268-449b-8549-0c4d5171f52a" />

<img width="918" height="827" alt="image" src="https://github.com/user-attachments/assets/bfbfce63-78b7-42f1-9396-def35619c96b" />

<img width="918" height="767" alt="image" src="https://github.com/user-attachments/assets/a789092d-2a54-4fe1-8097-97f28d0cd354" />

<img width="916" height="722" alt="image" src="https://github.com/user-attachments/assets/020c87da-033e-4f9e-b68b-3050df2f5bf4" />

<img width="921" height="818" alt="image" src="https://github.com/user-attachments/assets/a4ad9ebf-9f79-499a-a991-0d2c0748d62a" />


The results from the multiple linear regression model, model1, showed that GDP per capita, Family, Life expectancy, and Freedom have a positive effect and statistically significant effect on happiness. However, this single level regression model ignores that fact that countries are nested within regions. In other words, this model did not consider the clustering effects. Countries within one region might have some unique common characteristics which distinguishes them from other regions. That is, theoretically, observations from countries within a specific region are expected to be correlated and this has to be taken into account. To address this problem, three different models were considered:

- Region-fixed effect model, `model2, by manually creating the Region dummy variables. This is same as the linear regression model with the inclusion of the factor, Region, as a predictor. We could have also used region_id as the factor.

- In `model3`, we used the plm package to run the Region fixed effect model. It should be noted that the results from model2 and model3 are the same as expected.

- In `model4` and `model5`, we run a multilevel model. `model4` is an intercept-only (i.e., null) model. This model was fitted to help compute the Intra-Class Correlation Coefficient (ICC). The `ICC` was found to be 0.62, indicating that about 62% of the total variance in the outcome variable can be explained by the clusters (i.e., regions). This further confirmed the need for considering the clusters in the analysis. Therefore, `model5`, a random intercept model, was fitted.

The results of all of these models (i.e., linear regression, fixed-effect model, and random-intercept model) were similar. Specifically, all models showed that GDP per-capita, Freedom, Family, and trust in government have positive and statistically significant effect on both happiness. That is, the higher the GDP per-capita, levels of freedom, positive family relationship, and trust in government the higher the level of happiness.


## Conclusion and Recommendation
This project was conducted to gain some insights from the World Happiness Data. The results showed that Sub-Saharan Africa experience the lowest level of happiness, while Australia and New Zealand, Western Europe, and North America experience higher levels of happiness. From the statistical models, it was found that freedom, life expectancy, GDP per capita, and Family have significant impact on the level of happiness in each sub-region. Also, Sub-Saharan Africa has the lowest average happiness score whilst Australia and New Zealand has the highest happiness score. It is therefore recommended that various leaders, especially, governments from the Sub-Sahara African countries should put in much effort to reduce corruption and increase the level of trust of the citizens in the government. Also, policies and programs should be put in place to ensure productivity within the country. This will result in an increase in GDP per-capita subsequently lead to an increase in the level of happiness.


