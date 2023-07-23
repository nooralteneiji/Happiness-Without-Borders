```diff
- account for people irrationally scoring their happiness
```

# Dataset 
[World Happiness Report](https://worldhappiness.report/archive/)
- `country`: The name of the country for which the happiness data is reported.
- `year`: The year in which the happiness data is recorded.
- `GDP`: Gross Domestic Product per capita, which measures the economic output per person in a country.
- `socialSupport`: The level of social support and the presence of a support network in a person's life.
- `lifeExpectancy`: The average number of years a person is expected to live in good health, capturing the overall health and well-being of individuals in a country.
- `freedom`: The degree of political and social freedoms enjoyed by individuals in a country.
- `generosity`: The measure of generosity, including charitable donations and helping others, in a country.
- `corruption`: The perceived level of corruption and trustworthiness within the public sector of a country.
- 'happiness'

  

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

region_orig	region_orig_id	region_dest	region_dest_id	country_orig	country_dest	regionflow_1990	regionflow_1995	regionflow_2000	regionflow_2005	countryflow_1990	countryflow_1995	countryflow_2000	countryflow_2005

[UCDP Georeferenced Event Dataset](https://ucdp.uu.se/downloads/index.html#ged_global)

*Countries with less immigrants, more genetically pure?*


# Overview of Research Questions
**(1) Temporal Trends in Happiness and Migration:**
Let us set the stage by providing a broad understanding of how migration patterns and happiness scores have shifted over time. Recognizing the trends at a macro level can form the foundation for more specific exploration later on.
   - How have migration patterns changed over time in relation to shifts in the happiness scores of both source and destination countries?
   - Factor in global events: economic downturns (decrease in GDP) and conflicts 
    
**(2) Migration Effects on Host Country Happiness:**
Now that we understand the overarching patterns, it's logical to then focus on the specific implications of these patterns.
- How does an influx of migrants impact the happiness score of the host country in subsequent years? Adjust for economic impact, unemployment rates, and social integration programs.


**(3) Happiness and Genetic Diversity:**
After exploring the direct impact of migration on happiness, this question delves deeper into understanding if there's any inherent relationship between a country's happiness score and the genetic diversity of its population.
- Is there a correlation between a nation's average happiness score and the genetic diversity of its population? Control for socioeconomic factors and historical events that might have impacted both happiness and genetic diversity.

**(4) Genetics and Migration:**
Building on the knowledge of how happiness relates to genetic diversity, it's a fitting progression to then explore how genetic factors might influence or be influenced by migration patterns.
- Are there discernible patterns in allelic frequencies among countries with higher emigration rates as compared to those with lower rates? Consider adjusting for shared historical migrations or neighboring country influence.

# Q1: How have migration patterns changed over time in relation to shifts in the happiness scores of both source and destination countries?
## Data preprocesssing
- Widely available data on the number of people living outside of their country of birth do not adequately capture contemporary intensities and patterns of global migration flows[(Abel and Sanders, 2014)](https://www.science.org/doi/full/10.1126/science.1248676?ijkey=ypit4%2Fxi7wo4M&siteid=sci&keytype=ref).
- Stock data, measured at a given point in time as the number of people living in a country other than the one in which they were born, are more widely available and far easier to measure across countries than are flow data capturing movements over a period of time [(Abel and Sanders, 2014)](https://www.science.org/doi/full/10.1126/science.1248676?ijkey=ypit4%2Fxi7wo4M&siteid=sci&keytype=ref).
- However, flow data are essential for understanding contemporary trends in international migration and for determining relationships.
      - They used an innovative methodology to estimate bilateral flows between 196 countries from 1990 through 2010. The estimates reflect migration transitions and thus cannot be compared to annual movements flow data published by United Nations and Eurostat 2. The authors used statistical missing data methods to estimate the five-year migrant flows that are required to meet differences in migrant stock totals. For example, if the number of foreign-born in the United States increases between two time periods, they estimated the minimum migrant flows between the US and all other countries in the world that are required to meet this increase. For each country of birth, they estimated the minimum number of migrant flows required to match differences in stocks by assuming that people are more likely to stay than to move. This estimation procedure was replicated simultaneously for all 196 countries to estimate birthplace specific flow tables, resulting in a comparable set of global migration flows 3.

## Analysis 
1. **Trend Analysis**: We visualized the trend in average migration weights over time, and superimposed the trend in average happiness scores for both source and destination countries. This gives us an insight into the general global migration trend in relation to happiness.



3. **Difference in Happiness Scores**: We compared the distribution of differences in happiness scores (source - target) over time. If the distribution leans towards positive, it suggests people migrate to happier countries.

4. **Correlation Analysis**: Measure correlation coefficients between the difference in happiness scores and migration weights. A positive correlation might suggest that as the happiness difference increases, so does the migration weight.

5. **Economic Downturns**:
    - Identify years of global economic downturns (you might need external data for this or define it based on a decrease in average global GDP).
    - Analyze migration patterns during these years. Do more people migrate during economic downturns?
    - Check the relationship between happiness scores and migration during these years. Do people tend to move from countries with larger drops in GDP or happiness?

6. **Regional Conflicts**:
    - Identify major regional conflicts during the time frame (this would require external data).
    - See if there's a spike in migration from these conflict zones.
    - Analyze the happiness score trend in these zones compared to global average.

# Q2: How does an influx of migrants impact the happiness score of the host country in subsequent years? Adjust for economic impact, unemployment rates, and social integration programs.
For this research question, supervised machine learning will be used to build a regression model. We will use migration-related features, such as the number of migrants, economic impact, unemployment rates, and social integration programs, as independent variables to predict the happiness score of the host country in subsequent years.


# Q3: Is there a correlation between a nation's average happiness score and the genetic diversity of its population? Control for socioeconomic factors and historical events that might have impacted both happiness and genetic diversity.
We used a regression analysis to explore the correlation between a nation's average happiness score (dependent variable) and genetic diversity metrics (independent variables). The model was adjusted for socioeconomic factors and historical events.




# Q4: Are there discernible patterns in allelic frequencies among countries with higher emigration rates as compared to those with lower rates?
This question is focused on understanding patterns in allelic frequencies among countries with different emigration rates. Population genetics and statistical analyses was used for exploring the relationship between genetics and migration patterns.

















## Q1 Visualization 
### Circular migration plot 
representing the inter-relationships between data points in a graph. The nodes are arranged radially around a circle with the relationships between the data points drawn as arcs (or chords) connecting the nodes. The number of chords is scaled by a weight (migration flow).
This code was written based on this [source](https://holoviews.org/reference/elements/bokeh/Chord.html).

Country migration flow from 2010-2015.

![chord_diagram_country](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/Outputs/chord_diagram_country.png)




**References**
[Inspiration 1](http://download.gsb.bund.de/BIB/global_flow/) 

[Global migration datasheet](http://download.gsb.bund.de/BIB/global_flow/VID_Global_Migration_Datasheet_web.pdf)

![inspo](https://s3-eu-west-1.amazonaws.com/pfigshare-u-previews/15025469/preview.gif?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIYCQYOYV5JSSROOA/20230722/eu-west-1/s3/aws4_request&X-Amz-Date=20230722T162858Z&X-Amz-Expires=10&X-Amz-SignedHeaders=host&X-Amz-Signature=ce612851f3829e2033fe6baf0a073882eb8dbfeacfa380167a0823de20e47339)


![How to read flow plot](https://github.com/nooralteneiji/Happiness-Without-Borders/blob/main/FlowChord.png)

![circular chord plot example](https://www.science.org/cms/10.1126/science.1248676/asset/0c9e0fd7-57fa-4460-9c26-6b82230adf14/assets/graphic/343_1520_f2.jpeg)

References used to write code for chord diagram: [Used chapter 5 as it details how to create migrations plots in javascript and R](https://github.com/null2/globalmigration/blob/master/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf), [source 1](https://holoviews.org/reference/elements/bokeh/Chord.html), [source 2](https://stackoverflow.com/questions/65344303/circular-chord-diagram-in-python), [source 3](https://d3blocks.github.io/d3blocks/pages/html/Chord.html), [source 4 (guide for chord diagrams in R)](https://download.gsb.bund.de/BIB/global_flow/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf)













