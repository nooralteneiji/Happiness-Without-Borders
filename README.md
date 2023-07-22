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

`year`, `origin`, `destination`, `type` (outward, return, transit)

3 different estimations of migration flow are in the columns: 
- `da_min_open`(demographic accounting, open minimization method)
- `da_min_closed` (demographic accounting, closed minimization method)
- `da_pb_closed` (demographic accounting, pseudo baysian method)
   - We will only this estimation since [Abel and Cohen, 2019](https://www.nature.com/articles/s41597-022-01271-z](https://www.nature.com/articles/s41597-019-0089-3)) found the Pseudo-Bayesian demographic accounting method to be the best estimation of migration flow from migrant stock data (how many migrants are residing in a country during a specific point in time) published by the World Bank and United Nations.



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



## Visualization 
### Circular migration plot (less developed --> more developed)
[Inspiration](http://download.gsb.bund.de/BIB/global_flow/)

![circular chord plot example]([https://www.science.org/cms/10.1126/science.1248676/asset/0c9e0fd7-57fa-4460-9c26-6b82230adf14/assets/graphic/343_1520_f2.jpeg)


References used to write code for chord diagram: [source 1](https://holoviews.org/reference/elements/bokeh/Chord.html), [source 2](https://stackoverflow.com/questions/65344303/circular-chord-diagram-in-python), [source 3](https://d3blocks.github.io/d3blocks/pages/html/Chord.html), [source 4 (guide for chord diagrams in R)](https://download.gsb.bund.de/BIB/global_flow/VID%20WP%20Visualising%20Migration%20Flow%20Data%20with%20Circular%20Plots.pdf)













