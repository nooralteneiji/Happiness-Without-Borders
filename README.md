# Home-sweet-home: determinants of migration flow 
---

# Datasets 
## [World Happiness Report](https://worldhappiness.report/archive/)
- `country`: The name of the country for which the happiness data is reported.
- `year`: The year in which the happiness data is recorded.
- `GDP`: Gross Domestic Product per capita, which measures the economic output per person in a country.
- `socialSupport`: The level of social support and the presence of a support network in a person's life.
- `lifeExpectancy`: The average number of years a person is expected to live in good health, capturing the overall health and well-being of individuals in a country.
- `freedom`: The degree of political and social freedoms enjoyed by individuals in a country.
- `generosity`: The measure of generosity, including charitable donations and helping others, in a country.
- `corruption`: The perceived level of corruption and trustworthiness within the public sector of a country.
- 'happiness'

  
## Migration flow 
[dataset](https://figshare.com/collections/Bilateral_international_migration_flow_estimates_for_200_countries/4470464)
- Provides an estimation of bi-lateral flow of migration, not captured by standard migration datasets (i.e., [Our World In Data](https://ourworldindata.org/migration)).

[csv from github](https://github.com/null2/globalmigration/blob/master/Data%20on%20the%20global%20flow%20of%20people_Version%20March2014.csv)

`year`, `origin`, `destination`, `type` (outward, return, transit)

Outward migrants move away from their country of birth. 

Return migrants move to their country of birth. 

Transit migrants move from and to countries, neither of which is their country of birth.

3 different estimations of migration flow are in the columns: 
- `da_min_open`(demographic accounting, open minimization method)
- `da_min_closed` (demographic accounting, closed minimization method)
- `da_pb_closed` (demographic accounting, pseudo baysian method)
   - We will only this estimation since [Abel and Cohen, 2019](https://www.nature.com/articles/s41597-022-01271-z)(https://www.nature.com/articles/s41597-019-0089-3) found the Pseudo-Bayesian demographic accounting method to be the best estimation of migration flow from migrant stock data (how many migrants are residing in a country during a specific point in time) published by the World Bank and United Nations.


**Why was this dataset was choosen and not UN/World Bank data?**
- **Inadequate Representation of Contemporary Migration**: 
  - Widely available data often don't accurately capture current global migration patterns [(Abel and Sanders, 2014)](https://www.science.org/doi/full/10.1126/science.1248676?ijkey=ypit4%2Fxi7wo4M&siteid=sci&keytype=ref).
  
- **Availability and Ease of Stock Data**:
  - Stock data, which counts people living in a different country than where they were born at a specific point in time, is easier to obtain and measure across countries compared to flow data which captures movement over a period of time [(Abel and Sanders, 2014)](https://www.science.org/doi/full/10.1126/science.1248676?ijkey=ypit4%2Fxi7wo4M&siteid=sci&keytype=ref).

- **Importance of Flow Data**:
  - Flow data is crucial to understand current international migration trends and establish relationships.
  
- **Methodology**: 
  - The authors estimated bilateral flows between 196 countries from 1990-2010.
  - The methodology represents migration transitions, making it distinct from annual movement data by the United Nations and Eurostat.
  - Using statistical missing data methods, they estimated five-year migrant flows necessary to account for differences in migrant stock totals.
  - An example: If foreign-born numbers in the US rise over two periods, they calculated the migrant flows needed between the US and other countries to match this increase.
  - They assumed people are more inclined to stay rather than move, thus estimating the minimum flow required to match stock differences for every birthplace.
  - This procedure was applied to all 196 countries, leading to a consistent set of global migration flows.

---

# Q1: What are the migration patterns?

## Trend analysis 
### Check distribution 
Before seeing if there is a statistically significant difference between the the migration types, we need to see if data normally distributed. This step is important as it will inform us which type of non-parametric test to use.

As we can see, migration data is skewed to the left. 

![distribution migration](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q1_distributionMigration.png)


### Check if significant deifferences between migration type 
Since we do not have a normal distribution and we want to test more than two groups, we will use a Kruskal-Wallis Test.

We do not need to do a test between the migration types and happiness scores since comparing them would not be meaningful.

We will compare the differences in migration weights for each pair of migration types (e.g., 'inwards' vs. 'outwards', 'inwards' vs. 'transit', 'outwards' vs. 'transit') and the differences in happiness scores between 'transit' and 'happiness_source' for each year separately.

The null hypothesis for the Kruskal-Wallis test is that the distributions of the two groups being compared are identical, while the null hypothesis for the Wilcoxon signed-rank test is that there is no difference between the paired samples. If the p-value is less than the significance level (<0.05), it indicates a statistically significant difference between the groups.

Based on the low p-values we reject the null hypothesis for all tests, indicating that there is a statistically significant difference in migration weights between each pair of migration types for each year. This means that the migration weights are not coming from the same distribution for all pairs of migration types and there are significant differences between them.


### Line graph: Viusalize migration trends as a function of time

![globaltrend](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q1_globalTrend.png)

The plot shows the trends and implications of migration weight and happiness over the years 2005, 2010, and 2015. The data is presented using two y-axes, with migration weight (transit_mean, return_mean, and outward_mean) represented on the left y-axis and happiness (happiness_source_mean and happiness_target_mean) represented on the right y-axis.

Trends for Migration Weight:
- Outward migration most popular.
- Transit Mean: This represents the average migration over the years between two countries which individuals are not originally. It shows a decreasing trend from around 1421 in 2005 to about 534 in 2010 and then slightly increasing to approximately 559 in 2015.

- Return Mean: This represents the average return migration weight over the years. It starts at around 4308 in 2005, decreases to approximately 3687 in 2010, and then continues to decline to about 3104 in 2015.

- Outward Mean: This represents the average outward migration weight over the years. It starts at approximately 9571 in 2005, decreases to around 7902 in 2010, and then further declines to about 7174 in 2015.

Implications:
The decreasing trends in transit mean, return mean, and outward mean migration weight indicate that there might have been changes in migration patterns over the years. The decrease in transit migration weight suggests a reduction in the number of people migrating between two countries which they are not originally from. Similarly, the decline in return and outward migration weights indicates a possible decrease in the number of people returning to their home countries or leaving their home countries, respectively.


### Circular Chord Diagram  
representing the inter-relationships between data points in a graph. The nodes are arranged radially around a circle with the relationships between the data points drawn as arcs (or chords) connecting the nodes. The number of chords is scaled by a weight (migration flow).
This code was written based on this [source](https://holoviews.org/reference/elements/bokeh/Chord.html).


**References**
[Inspiration 1](http://download.gsb.bund.de/BIB/global_flow/) 

References used to write code for chord diagram: [Used chapter 5 as it details how to create migrations plots in javascript and R](https://github.com/null2/globalmigration/blob/master/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf), [source 1](https://holoviews.org/reference/elements/bokeh/Chord.html), [source 2](https://stackoverflow.com/questions/65344303/circular-chord-diagram-in-python), [source 3](https://d3blocks.github.io/d3blocks/pages/html/Chord.html), [source 4 (guide for chord diagrams in R)](https://download.gsb.bund.de/BIB/global_flow/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf)


#### Which countries are people migrating to? 


**WE ARE ONLY LOOKING AT countries that send and recieve at least 0.5% of world's migrants**

*The chord graph code was written based on this [source](https://holoviews.org/reference/elements/bokeh/Chord.html).*

**Overall routes**

![chord_country](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q1_chord_diagram_countryRoute.png)

**Which countries are most people migrating to?**


*HOW TO READ THE GRAPH: Look at the largest nodes. They represent the destination country, so all chords coming from other countries indicate where the people are migrating from to reach the destination country.*

People are migrating to the UK, US, UAE, Canada, Austrailia, Germany, Russia, Saudia Arabia, Italy and Spain.

![country toward](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q1_chord_diagram_topCountryToward.png)

**Which countries are most people migrating away from?**

*HOW TO READ THE GRAPH:Look at the largest nodes. They represent  the country of origin, so all chords coming from other countries indicate where the people are migrating towards*

People are migrating away from Mexico, India, China, Bangladesh, Pakistan, Russia, Saudia Arabia, Syria, US, UK, Germany.

![country away](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q1_chord_diagram_topCountryAway.png)

#### Which regions are people migrating away from? 

*HOW TO READ THE GRAPH: Look at the largest nodes. They represent the country of origin, so all chords coming from other countries indicate where the people are migrating towards*

![region](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/chord_diagram_Region.png)  

#### Which sub-regions are people migrating away from? 

*HOW TO READ THE GRAPH: Look at the largest nodes. They represent the country of origin, so all chords coming from other countries indicate where the people are migrating towards*

![chord_subregion](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/chord_diagram_subRegion.png)


# Q2: What are the migration patterns with respect to country qualities?


## Are people migrating to better countries?

A handful of countries in the African continent expirence a better happiness score once they migrate and arrive at the destination country.

![world heatmap](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q2_WorldHappinessMap.png)


### Migrating to happier countries? 

**Movinge to happier country?**

![happier](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q2_chord_diagram_happier.png)

**Movinge to less happy country?**

![less happy](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q2_chord_diagram_lessHappy.png)


### More questions...
- Migrating to better GDP?
- Migrating to better life expectancy?
- Migrating to less corruption?
- Migrating to more freedom?
- Migrating to less violence attacks?

etc., etc., HOWEVER, the actual factors that come into play for the decision to migrate is much more interesting...

---

# Q3: Decoding the decision to migrate
Migration is a multifaceted phenomenon driven by a combination of economic, social, political, and environmental factors. The decision to migrate can be based on push factors (negative conditions encouraging or forcing individuals to leave a place) and pull factors (attractive conditions luring individuals to a new place).

We want to predict the percentage_weight of migration between countries.

The factors we will examine as drivers of migration:

- Economic Factors (GDP)
- Social Factors (social support)
- Quality of Life Factors (happiness, life expectancy)
- Political or Civic Freedoms (perception of corruption, freedom)
- Cultural or Social Values (generosity)
- Violence (number of violence events)    

**Factors from Dataset**:
    - **Push Factors**: Factors that may influence someone's decision to leave their home country.
        - `GDP_source`
        - `socialSupport_source`
        - `happiness_source`
        - `lifeExpectancy_source`
        - `corruption_source`
        - `freedom_source`
        - `generosity_source`
        - `source_total_violence`
        
    - **Pull Factors**: Factors that may attract someone to a new country.
        - `happiness_target`
        - `GDP_target`
        - `socialSupport_target`
        - `lifeExpectancy_target`
        - `freedom_target`
        - `generosity_target`
        - `corruption_target`
        - `target_total_violence`
    
    - **Differential Factors**: Comparing conditions between the source and target countries.
        - `happiness_difference`
        - `GDP_difference`
        - `socialSupport_difference`
        - `lifeExpectancy_difference`
        - `freedom_difference`
        - `generosity_difference`
        - `corruption_difference`
    
**Control Variables**:
    - These are variables that might affect the outcome (migration) but are not of primary interest. They can account for potential confounders or other variables that might distort the relationship between the main independent variables and the dependent variable (migration).
        - `year`: Temporal factors can influence migration.
        - `source`: Country-specific effects, such as policies, can be influential.
        - `sourceRegion` & `sourceSubRegion`: Regional factors, like regional economic policies or regional conflicts, might play a role.
        - `target`, `targetRegion`, & `targetSubRegion`: Migration might be influenced by the specificities of target places, such as their immigration policies or socio-cultural attitudes towards immigrants.

**Dependent variables**
        - `percentage_weight`, `weight`, and `total_weight`: These may capture the intensity or magnitude of migration. 

## Method 

**Random forest**: We are essentially creating multiple decision trees, where each tree gets a different subset of the data (via bootstrapping) and different pair of features. The decisons from all the trees will be taken in aggregate to create the prediction.

**Why?** Was proven to have second highest accuracy when compared to other supervised machine learning models [(Kaur et al., 2019)](https://www.mdpi.com/2076-3417/9/8/1613).


### Data Preprocessing
   
   - **Encode Categorical Variables**: RF can handle categorical data, but scikit-learn prefers numerical data. So, from our dataframe `violenceHappinessMigration_df`, we will encode:
      - `source`
      - `sourceRegion`
      - `sourceSubRegion`
      - `target`
      - `targetRegion`
      - `targetSubRegion`
      - `happiness_category` (ordinal encoding since it has a ranking)
      
   - **Handle Missing Data**: Ensure that there's no missing data. 

   - **Feature Scaling**:  RF isn't as sensitive to different scales (unlike SVM), and we do not plan to use other algorithms for comparison--so we will skip this step.
   
   - **Split into X and y**: We are trying to understand the relative impact of migration and want to compare across countries/regions of different sizes, so we will use `percentage_weight` rather than `weight`. This is becuase it accounts for the size of the population, making it possible to compare migration rates between large and small countries/regions on an equal footing. Additionally, it can give a clearer picture of the actual impact or significance of migration relative to the source population.
   
   - **Split into training and test set**: where 30% of the data is reserved for testing, and the rest (70%) is used for training.

### Hyperparameter Tuning

   - We used Grid Search with Cross-Validation to find optimal hyperparameters (e.g., number of trees, max depth of trees, min samples split).

MSE = `0.0336`.

This is a measure of the average squared difference between the actual target values (y_test) and the predicted values (y_pred) obtained from the RandomForestRegressor model.

In this case, the MSE value of 0.0336 indicates that the model has reasonably accurate predictions on the test set, with small errors in its predictions compared to the actual target values.


### Model Training and Validation

   - **K-Fold Cross Validation**: Implemented 10-fold validation to ensure that our model's performance is consistent across different partitions of your data.
   
   While Random Forests inherently utilize bootstrapping, it's essential to remember that this only offers an internal validation. On the other hand, the external k-fold cross-validation sheds light on different aspects of model performance.

**How 10-fold cross-validation works:** We split the training dataset into 10 equal "folds." During each of the 10 iterations, we train the model using 9 folds and validate it using the remaining fold. This way, every fold gets its turn as a validation set, enabling us to assess the model's performance across diverse data subsets.

So, why do go out of our way to add this approach?

- **Performance Insight**: With this method, we receive an array of performance metrics, in our case, ten distinct MSE values. The spread of these scores, captured by `std_mse`, offers a glance into the model's consistency. A low standard deviation suggests stability across varied data partitions, while a high one indicates potential inconsistencies.

- **Optimal Data Use**: Unlike the typical train-test split approach, where some data might remain untouched, k-fold cross-validation ensures we're both training and validating across the entire dataset.

- **Balancing Bias and Variance**: The spread of performance metrics across folds can hint at the model's sensitivity to specific data nuances.

- **A Check Against Overfitting**: While Random Forests have built-in mechanisms against overfitting, they aren't foolproof. Cross-validation aids in spotting signs of overfitting. A high variance in performance across folds might be a red flag.

- **Gauging Generalization**: By averaging performance over multiple data subsets, we gain a more trustworthy perspective on how well the model might perform on unseen data.

- **Harmonizing with GridSearchCV**: Remember our earlier GridSearchCV step? It also banked on cross-validation. Keeping the evaluation method consistent ensures we're comparing apples to apples.

In a nutshell, 10-fold cross-validation is our way of diving deeper into the model's performance, giving us a richer and more nuanced understanding than a simple train-test split would."

10-Fold Cross-Validation MSE:`0.0428 (+/- 0.0066)`

This score is the average of the MSEs from each of the 10 different train-test splits in the k-fold cross-validation. The variability (+/- 0.0066) gives an indication of the consistency of the model performance across different splits.

This average MSE provides a more generalized assessment of the model's performance. The variability indicates how much the performance might change based on different data splits.

   
### Model Performance
   

Overview of the model's performance:

MAE = `0.106`
- takes into account error magnitude 

- on average, the model's predictions are off by approximately 14.28% from the true values. In other words, the model is, on average, about 0.1428 units away from the true value.

MSE = `0.0339`
- variance of errors 
-  It penalizes larger errors more severely than smaller ones, meaning it's more sensitive to outliers than the MAE.

- our MSE value suggests that our model does a good job of fitting the data, as the value is relatively low.

- This is the MSE calculated after training the model on the entire training set and then testing it on a separate, held-out test set (the one we created with train_test_split).
- This score gives an indication of how the model, trained on the entire training dataset, performs on unseen data.
- previously we found the average of the MSEs from each of the 10 different train-test splits in the k-fold cross-validation.
    - The slight difference between these two MSE values is due to the variability inherent in the dataset and the training process. The fact that the two values are relatively close suggests that our model's performance is consistent and that it generalizes well to new data. The cross-validation MSE gives you a range of likely performances, and the test set MSE falls comfortably within this range, which is a good sign.

R^2 = `0.987`
- proportion of the total variation in the dependent variable that's explained by the independent variables 
- ranges from 0 to 1, where higher values are better, indicating that more variance is explained by the model.

- approximately 98.7% of the variability in the percentage_weight is explained by the model. This suggests that the model captures most of the variance in the data.
- **!!However!!**  with such high R^2 values we need to be cautious becuase it could be a sign of overfitting.
    - Given that we used k-fold cross-validation earlier, the risk is somewhat mitigated.

The Random Forest model has shown a very high R^2 score and relatively low error metrics, indicating that it performs well on the test set. The high R^2 score suggests that the features we have selected are very predictive of migration patterns (AKA percentage_weight). 

### Model Interpretation

#### Feature Importance

RF allows us to extract feature importance which tells us which variables are most influential in making predictions.
   
![feature importance](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q3_featureImportances.png)
   
This highlights the most influential factors in determining the migration patterns (as measured by `percentage_weight`).
   
##### Observations:

1. **Country-Specific Influences**: 
    - **Source Countries**: The model indicates that the source countries, specifically `source_Pakistan`, `source_India`, `source_Bangladesh`, `source_China`, and `source_Saudi Arabia`, are amongst the most important features in predicting migration patterns (`percentage_weight`).
    - **Target Countries**: Similarly, target countries like `target_Germany`, `target_India`, and `target_Bahrain` play significant roles.
    - These findings suggest that specific countries play a pivotal role in influencing global migration patterns.

2. **Economic & Societal Metrics**: 
    - Features like `GDP_source`, `lifeExpectancy_source`, and `happiness_source` are high up on the list, emphasizing the role of economic and societal well-being metrics in influencing migration decisions.

3. **Implicit Interactions and Patterns**: 
    - Some features like `source_Pakistan` and `source_India` have higher importances than general metrics like `GDP_source`. This suggests that there might be country-specific factors, beyond just GDP or happiness, influencing migration. 
    - There might be political, social, or environmental factors at play in these countries that drive migration.

4. **Climate & Environmental Considerations**: 
    - The presence of `target_climateIndex` and `source_climateIndex` indicates that environmental considerations might be playing a role in migration decisions. This could hint at factors such as climate change, environmental degradation, or natural disasters impacting migration patterns.
    
    
**What does it mean for the model to indicate that `source_Pakistan` is the most important predictor?**

The model is suggesting that the fact that a person is migrating from Pakistan is a strong indicator for the outcome variable, `percentage_weight`, at least within the scope of this model specifically. 

1. Relevance of `source_Pakistan`: If `source_Pakistan` emerges as one of the most influential predictors, it underscores that there are significant migration patterns (or weights) emanating from Pakistan. This could be due to a multitude of reasons: economic factors, societal unrest, geopolitical tensions, environmental challenges, or a combination of these and other factors.

2. Comparing to `GDP_difference`: The fact that `source_Pakistan` has a higher feature importance than `GDP_difference` suggests that the specific migration dynamics related to Pakistan might be more telling than the economic disparities (as measured by GDP differences) between source and target countries. It could imply:

   - Economic Factors: Even if the GDP difference between Pakistan and another country isn't vast, other intrinsic factors within Pakistan might be compelling its citizens to migrate. These factors could be unemployment rates, wage disparities, or local economic downturns that aren't fully captured by just looking at GDP.
   
   - Beyond Economics: Migration isn't solely driven by economic reasons. Political instability, religious or ethnic tensions, environmental factors, or educational opportunities can be substantial motivators. If the migration from Pakistan is more predictive than the GDP difference, it suggests that non-economic factors might be at play prominently in the case of Pakistan.

3. Holistic Interpretation: While `source_Pakistan` is highly predictive, it's crucial not to discount the role of other variables. For instance, `GDP_difference` might still play a significant role in migration patterns from other countries. Each predictor captures a unique facet of the broader migration landscape, and their collective interplay shapes the overall dynamics.


##### Link to Research Question:

**Factors Influencing Migration**: 
   - From the feature importance, it's clear that both source and target countries significantly influence migration decisions. Specific countries are highlighted, which means for a deeper understanding, we would need to investigate country-specific dynamics further.
   - Economic, societal, and environmental metrics play a crucial role in decision-making.

##### Implications:

1. **Geo-political Undertones and Migration Dynamics**:
    - **Emerging Economies and Migration**: The elevated significance of countries such as `source_Pakistan`, `source_India`, and `source_Bangladesh` may resonate with the broader political narrative of South Asia. The socio-political unrest, combined with the burgeoning youth population and economic constraints, might be catalyzing migration waves.
    - **Traditional Destinations**: The prominence of `target_Germany` underscores the traditional allure of Western Europe as a bastion of stability and economic opportunity. On the other hand, `target_Bahrain` suggests the continuation of the Gulf countries' role as sought-after destinations for labor migrants, particularly from South Asia.

2. **Economic Disparities and Societal Tensions**:
    - While GDP is often touted as a primary factor for migration, the relative significance of `GDP_source` juxtaposed against `happiness_source` and `lifeExpectancy_source` reflects a nuanced tapestry of migration. It underscores that migration is not just an economic decision but is profoundly intertwined with societal well-being and broader life satisfaction metrics.

3. **The Silent Narratives Beyond Macro Metrics**:
    - The disproportionate weightage of specific source countries, even over overarching economic indicators like `GDP_source`, is revelatory. It hints at deeper, often unspoken or under-represented narratives. For instance, the role of political instability, regional tensions, or societal fractures in countries like Pakistan and India might be overshadowing purely economic considerations.

4. **Environmental Factors and the New Migration Paradigm**: 
    - The emphasis on `target_climateIndex` and `source_climateIndex` is evocative of the emerging global narrative around climate-induced migration. It paints a picture of a world where environmental considerations, from degrading ecosystems to more immediate natural calamities, are becoming as central to migration decisions as traditional economic or political factors. The confluence of climate change and its socio-political repercussions cannot be understated in this new migration dynamic.   
   
#### Interaction Between Variables

   - Interactions between variables can be further explored. For example, why do certain source countries have higher importance than others? Is there an interaction between GDP, life expectancy, and specific countries?
   - The role of the climate index in both source and target countries needs further scrutiny. Is environmental migration becoming more prominent?
   
While RF doesn't explicitly give interaction terms like linear regression, high feature importance scores can sometimes hint at interactions. Further, partial dependence plots help visualize the relationship between the target and a set of features, and potentially highlight interactions.

Specifcally, Partial Dependence Plots (PDPs) can show the relationship between a feature and the target. We will look at the features with highest importance to show how migration weight changes with variations in a particular feature while keeping all other features fixed. 

![PPD plot](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q3_PPD.png)

[Source for understanding how to read PPD](https://christophm.github.io/interpretable-ml-book/pdp.html)

- Overall, as the values of these features increase, the model predicts a higher likelihood of migration.


- GDP of orginal country only has an influence on migration weight after a cerain point threshold is met (GDP =~ 10.5). Beyond this point, however, GDP does not hold as strong of an influence.
- Climate vulnerability has a influence at extremely low points, however, once the narrow range is exceeded, it does not have a influence until an index of ~0.5 is reached.

- destination countries "India" and "Germany" are associated with higher migration rates. Factors specific to these countries may be attracting more migrants, such as economic opportunities, social support, or other favorable conditions.  
  
#### Tree Visualization
Visualizing all trees might be overwhelming, so we will visualize best tree to understand the decision-making process.
      
![best tree](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q3_bestTree.png)
      
      
The structure of the decision tree provides insights into how different variables may be interacting and their collective influence on predicting migration weight. 

##### Observations:

1. **Prominence of Source Country**: 
   - The fact that `source_Pakistan` is the root node indicates that it's a major deciding factor in predicting migration weight. If a given migration flow doesn't involve Pakistan as the source, the next immediate question the tree asks pertains to migration involving `source_India`.
   
2. **Climate Concerns**: 
   - `ClimateIndex_difference` branches immediately after `source_Pakistan` and `source_India`. This showcases the significance of climate vulnerabilities as a motivating factor for migration, especially when combined with the specific circumstances of the originating country.
   - Further, `target_climateIndex` appears multiple times in subsequent branches. This underscores the role that the climate index of the target country plays in migration decisions. It's evident that the climate profile of both the source and destination countries interact to influence migration.

3. **Socio-Economic and Happiness Metrics**:
   - The branching based on `happiness of source country` under `source_India` implies that the general well-being or satisfaction level in the source country (India, in this instance) interacts with other factors in determining migration.
   
4. **Interaction Between Source and Target**: 
   - The presence of `target_India` in the tree's deeper layers indicates an interaction between climate vulnerabilities and the specific target country. This interaction might suggest that migrants from certain areas are more inclined to move to India when other conditions, such as climate vulnerabilities, align.

##### Answering Research Questions:

- **Primary Interactions**: The most significant interactions are evident in how branches diverge. For example, migrations from Pakistan are immediately contextualized by the difference in climate vulnerabilities between the source and target countries. This suggests an interaction between country-specific issues in Pakistan and environmental factors.
  
- **Secondary Interactions**: Further down the tree, the decision pathways diverge based on other countries or conditions (like happiness in the source country). This showcases secondary interactions. For instance, for migrations from India, the decision tree indicates that the choice of destination might be influenced by the happiness level in India combined with the climate index of the target country.

- **Nested Interactions**: The tree structure also suggests nested interactions. For instance, the choice of moving based on climate vulnerabilities is subsequently influenced by the specific target country (like `target_India`). 

##### Implications:

**Redefining Migration Causality**:
    - The dominant position of `source_Pakistan` in the decision-making hierarchy challenges prevailing macro-level theories of migration. Instead of broad-spectrum socio-economic factors, specific factors intrinsic to specific nation-states seem to be more important. We should thus approach the migration discourse with a degree of country-specific granularity rather than overly broad generalizations.

**The Environmental Turn in Migration Studies**:
    - The interactions also challenge a monolithic narrative of migration. It isn't just about economic opportunities or conflict. The tree suggests that factors such as climate change and well-being (happiness) play a crucial role and can't be ignored.

**The Well-being Paradox**:
    - The significant influence of the `happiness of source country`, especially under the branch of `source_India`, highlights the intricate balance between objective socio-economic indicators and subjective well-being assessments. It triggers the age-old debate in political philosophy about material well-being versus overall life satisfaction and how they influence individual and collective decision-making.

**Geopolitical Implications of Climate and Migration**:
    - The nested interaction, especially involving `target_India`, raises crucial geopolitical questions. It suggests that certain target countries are seen as refuges in light of climatic vulnerabilities. This has profound implications for India's foreign policy and its position in South-South cooperation on climate-induced migration. It's a clarion call for regional cooperation frameworks that preemptively address such migration surges, balancing humanitarian imperatives with national security concerns.
   

# Q4 Analyze Areas of Poor Performance

## Residual analysis 

![sub plots](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q3_residualAnalysis.png)

Residual vs. Predicted Value
- Residuals are randomly scattered around the horizontal axis
    - a linear regression model is appropriate for the data.
- residuals center on zero 
    - the model does not systematically overestimate or underestimate the dependent variable.
- some values are extremely above or below zero--> they are our outliers/bias in the predictions.

Histogram 
- shows that residuals are normally distributed
    - though some extreme values at zero.
    - the model's parameter estimates are likly to be efficient = narrower confidence intervals and better hypothesis testing validity.

Q-Q plot 
- visually determine how close the residuals are to a normal distribution
- tails deviate from the line

## Using DBSCAN to identify residuals 

![clusters](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q4_outlierFeatureImportances.png)


## Analyzing residuals 
The feature importance values for the outliers provide some crucial insights:

### Feature importance 

![feature importance](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/Q4_identifyCluster.png)
**Life Expectancy Difference**

With an importance score of `0.480889`, the difference in life expectancy between the source and target countries is the dominant feature for predicting migration percentages among the outlier cases. 

Implications:
- Migration decisions for these outlier groups are heavily influenced by the prospects of a better or worse life expectancy in the target country compared to their home country.
- This might suggest that health services, quality of life, or conditions that impact longevity (like conflict, famine, or disease) are critical determinants for these specific migratory movements.

**Climate Index Difference:

The difference in climate indices between source and target countries is the second most important feature with an importance of `0.123176`.

Implications:
- Environmental or climate factors are significant in migration decisions for these outliers. This can be related to climate change impacts, where certain regions are becoming less habitable due to rising temperatures, flooding, or other environmental changes.
- It reinforces the idea that environmental migrants or climate refugees might be a noteworthy segment within these outliers.

**Generosity Source:

Generosity from the source country has an importance score of `0.037300`.

Implications:
- The level of generosity or altruism in the source country might indicate a society's cohesiveness and the well-being of its inhabitants. If people are migrating from places with higher generosity, it may hint at other factors pushing them to migrate, like political unrest or economic challenges.
- Alternatively, it may suggest that in contexts where societal generosity is high but other living conditions are unfavorable, people might be more prone to seek better conditions elsewhere.

**GDP Difference:

The GDP difference between source and target countries has an importance of `0.036737`.

Implications:
- Economic factors, though not as dominant as life expectancy or climate for these outliers, still play a role. Migrants might be seeking better economic opportunities or escaping economic downturns in their home countries.

**Source Climate Index:

The climate index of the source country itself (not the difference) also holds some importance with a score of `0.031664`.

Implications:
- The specific environmental conditions in the source country are driving some migration patterns. If a source country has extreme climate conditions or is facing significant environmental challenges, its inhabitants might seek to relocate regardless of the target country's climate.

In summary, for these outlier cases, while economic conditions play a role, it appears that life quality (represented by life expectancy) and environmental factors are particularly dominant in influencing migration decisions. This might hint at specific push factors in the source countries that are driving these unique migration patterns.
   
### Interaction between variables 
Pairplot not very meaningful since few data points.

![pairplot](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q4_pairplot.png)

![matrix](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/Figures/q4_corMatrix.png)


# Concluding thoughts 

The data-driven findings, offer profound insights into the complex web of international migration. It's an interaction between economics, societal well-being, geopolitics, and now, environmental considerations. Migration, as this study suggests, is far from a monolithic phenomenon; it's a reflection of a world in flux, constantly reshaped by a plethora of forces, both overt and covert.


# Limitations 
- Selection Bias:
  - Migrants are a selective group, influenced by factors not fully captured in the data.
  - Optimism and adaptability may lead to biased migration results.

- Confounding Variables:
  - Other variables like culture, language, job opportunities, family support, and personal characteristics can influence both migration decisions and happiness outcomes.

- Cultural Magnetism and Soft Power:
  - The cultural allure and soft power of a destination can strongly influence migration decisions.
  - Factors such as art, cinema, literature, music, fashion, and academic or entrepreneurial ecosystems play a role in attracting migrants.

- Limited Granularity of Violence Dataset:
  - The violence dataset lacks city-specific information, which may lead to generalizations about the entire country's situation.
  - More granular data exists but could not be utilized due to differences in the level of unit of analysis with the happiness and migration data.

- Missing Countries in Internet Dataset:
  - The internet dataset may have missing information for some countries, potentially impacting the analysis of digital and technological footprints as migration determinants.

# Future directions 
- Delving Deeper into Migration Factors:
   - Focus on Pakistan's specific context and climate vulnerabilities in migration decisions.
   - Investigate historical, political, and social reasons for migration patterns.

- Digital and Technological Footprints as Migration Determinants:
   - Explore variables like internet freedom, digital infrastructure quality, and tech ecosystem vitality.
   - Study their influence on migration, especially among the young, urban, and skilled demographic.

- Correlation between Happiness Score and Genetic Diversity:
   - Conduct regression analysis to examine the relationship between a nation's happiness score and genetic diversity.
   - Control for socioeconomic factors and historical events that might impact both variables.

- Patterns in Allelic Frequencies and Emigration Rates:
   - Utilize population genetics and statistical analyses to identify patterns in allelic frequencies among countries with different emigration rates.

- Impact of Migrants on Host Countries:
   - Investigate how an influx of migrants impacts host countries in subsequent years.

- Changes in Migration Patterns and Happiness Scores:
   - Analyze migration patterns over time in relation to shifts in happiness scores of both source and destination countries.

- Specific Indicators for Climate-Driven Migration:
   - Examine sensitivity and exposure indicators related to climate change and migration.
   - Study natural capital dependency, projected changes in biome distribution, warm periods, flood hazards, and urban concentration.



























