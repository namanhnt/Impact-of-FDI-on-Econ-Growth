# Impact of FDI on Economic Growth of Asian Developing Countries

![FDI](https://github.com/user-attachments/assets/c025c975-9b94-4272-bf21-5645bfb8248d)

## I. Introduction
My interest in studying the relationship between foreign direct investment (FDI) and economic growth sparked during my Master’s studies. While working on my econometrics dissertation, I became curious about why many developing countries in Asia have experienced rapid economic growth over the past few decades and how international investment has influenced that progress.

In recent centuries, Asia has become one of the most notable emerging markets for global investment. According to the World Investment Report 2025 ([UNCTAD](https://unctad.org/publication/world-investment-report-2025?utm_source=chatgpt.com)), the region received the highest level of FDI inflows worldwide, with $605 billion invested in 2024. This raised an interesting question for me: Does foreign investment truly help economies grow, or do fast-growing economies simply attract more foreign investors?

The project focuses on analyzing the panel data of 13 Asian developing countries in the span of 2000-2023. In this remake of my Master's dissertation, I have expanded the variable selection and included a new regression model, namely two-way fixeded effect model. The study now also includes automated data extraction from the World Bank API. This README provides a brief overview of the project, while the full data preparation, exploratory analysis, and regression results can be found in the three Jupyter Notebooks.

## II. Methodology
This study is based on the [Solow growth framework](https://corporatefinanceinstitute.com/resources/economics/solow-growth-model/), which explains economic growth through the accumulation of key production factors. In the basic Solow model, output is determined by capital and labour, meaning that increases in these inputs can raise the level of production and income in an economy. In this project, economic growth is represented by GDP per capita, while gross capital formation and labour force are used as proxies for capital and labour inputs. The model is then expanded by including FDI, trade openness, electricy access, goverment effectiveness and tertiary-level human capital as additional explanatory variables. FDI can contribute to economic growth by bringing capital, technology transfer, and managerial knowledge, while trade openness reflects the role of international integration in improving productivity and market efficiency. Access to electricity represents the level of infrastructure development that supports economic activity, government effectiveness captures the quality of public institutions and policy implementation, and tertiary education enrollment serves as a proxy for human capital development. The model is expressed as:

$$
\ln GDP_{it} =
\beta_0 +
\beta_1 \ln GCF_{it} +
\beta_2 \ln Labour_{it} +
\beta_3 \ln FDI_{it} +
\beta_4 Trade_{it} +
\beta_5 ElecAccess_{it} +
\beta_6 GovEffect_{it} +
\beta_7 SchoolEnroll_{it} +
\varepsilon_{it}
$$

*Where:*
- *i denotes country*  
- *t denotes year*
- *β₀ denotes the intercept term*  
- *εᵢₜ denotes the error term, varying across countries and time*
- GDP, GCF, Labour, and FDI are expressed in logarithmic form for heteroskedasticity reduction

Four panel regression models are used: Pooled OLS, One-way Fixed Effects, Two-way Fixed Effects, and Random Effects models. The Hausman test and F-test for time effects are applied to determine the most appropriate model. In addition, the Dumitrescu–Hurlin panel Granger causality test is used to explore the direction of causality between FDI and economic growth across countries.

## III. Data Gathering
In this project, I use macroeconomic data from the World Bank through its public data API. The World Bank provides a wide range of economic indicators for countries around the world, such as foreign direct investment, GDP, trade, infrastructure, and institutional quality. These datasets are compiled from national statistical agencies and international organizations, making them a reliable source for cross-country economic analysis.

<img width="1413" height="418" alt="image" src="https://github.com/user-attachments/assets/4f9db9fd-7601-4b41-af04-4d865a1c7195" />

Regarding the country selection, I have excluded Uzbekistan, Thailand, Jordan, Sri Lanka, Kazakhstan, Kyrgyzstan, Turkmenistan, Mongolia, and Myanmar from the dataset due to their substantial missing data, with over 30% of observations missing.

To ensure the consistency of data for the modelling, a small number of missing observations across several variables were addressed using linear interpolation within each country over time. Interpolation works by inferring the missing values through patterns or trends in the data.

## IV. Empirical Results

### 4.1. Correlation Matrix
<img src="https://github.com/user-attachments/assets/14a02910-a787-46a2-b7c5-b73af6471979" width="70%">

- Log GDP per capita has a moderate positive correlation with log FDI (0.31) => Support the hypothesis that higher FDI inflows are generally associated with higher GDP.
- Stronger positive correlations are also seen between GDP per capita and institutional or development indicators, such as electricity access (0.60), government effectiveness (0.66), school enrollment (0.78) => Justify the inclusion of these control variables in the model, as they appear closely linked to economic performance.

Overall, the matrix does not indicate severe multicollinearity among the main regressors. The regression analysis will formally test these relationships in the next part, using within-country variation over time.

### 4.2. Regression Model Results
<img width="905" height="593" alt="image" src="https://github.com/user-attachments/assets/52ccf54a-5505-4e79-a23d-9fdf8a15c927" />

**(1)** Pooled OLS

The pooled OLS model treats the panel dataset as a single sample and does not control for country or time heterogeneity. The results show that gross capital formation, FDI, government effectiveness, and school enrollment are positively associated with GDP per capita, while labour has a negative and significant coefficient. However, these results should be interpreted cautiously because pooled OLS does not control for unobserved country-specific factors.

**(2)** One-Way Fixed Effects (FE)

The FE model controls for country-specific characteristics. Gross capital formation remains strongly positive and significant, and school enrollment continues to show a positive impact on income levels. The effect of FDI becomes weaker, suggesting that part of the relationship observed in pooled OLS may be driven by country-specific factors.

**(3)** Two-Way Fixed Effects (2FE)

The two-way FE model additionally controls for time effects shared across countries. In this specification, FDI becomes statistically insignificant, while gross capital formation remains strongly positive, highlighting the importance of domestic investment. Government effectiveness becomes significant, suggesting that institutional quality supports economic performance.

**(4)** Random Effects (RE)

The RE model assumes country-specific effects are uncorrelated with the explanatory variables. Under this model, FDI becomes positive and significant again, while gross capital formation, electricity access, and school enrollment also show significant positive relationships with GDP per capita.

***Comparison with my former work***

<img width="596" height="508" alt="image" src="https://github.com/user-attachments/assets/babe0cce-b99a-49a4-ae77-c5d18f3554ac" />

Compared with my earlier academic work, the pooled OLS, Fixed Effects, and Random Effects models all showed FDI as positive and statistically significant. However, the extended model in this project introduces additional controls for infrastructure (electricity access), institutional quality (government effectiveness), and human capital (tertiary school enrollment). Furthermore, once both country and time effects are controlled for in the Two-Way Fixed Effects model, the coefficient of FDI becomes statistically insignificant. This suggests that after accounting for more factors across countries and global time shocks, FDI does not show a strong impact on GDP per capita.

### 4.3. Test Results

#### 4.3.1. Hausman Test
<img width="304" height="72" alt="image" src="https://github.com/user-attachments/assets/9fde9065-ddbf-4b49-966d-a3370cbc72b9" />

Since the p-value is below the 5% significance level, the null hypothesis that the unobserved country-specific effects are likely correlated with the explanatory variables is rejected. Therefore, the Random Effects estimator would be biased and inconsistent.

Based on this result, **the Fixed Effects models are preferred**, as they provide more reliable estimates for this panel data setting.

#### 4.3.2. F-test For Time Effects
<img width="279" height="74" alt="image" src="https://github.com/user-attachments/assets/ad7d5a8b-c166-455f-96ab-8c8c220b5fdd" />

Since the p-value is well below the 5% significance level, the null hypothesis that all time fixed effects are jointly equal to zero is rejected. This means that year-specific effects are statistically significant and should be included in the model.

Based on the two test results above, **the Two-Way Fixed Effects model (2FE) is the most approriate model** for this panel dataset.

#### 4.3.4. Dumitrescu-Hurlin Granger Non-causality Test
<img width="587" height="399" alt="image" src="https://github.com/user-attachments/assets/5d473334-405b-4992-8285-a2f7f514397f" />

**(a)** reported the null hypothesis that FDI does not Granger-cause economic growth. The results show that the null hypothesis is rejected at lag 1 and lag 3, as both the Z-bar and Z-bar tilde statistics are statistically significant at the 5% level. This indicates that past values of FDI contain useful information for predicting GDP per capita in the sample countries. In contrast, the test results at lag 2 are not statistically significant, meaning that the predictive relationship is not consistently present at every lag length. Overall, the findings suggest that FDI has short-run and medium-run predictive effects on economic growth, although the strength of this relationship may vary across different lag structures.

**(b)** tested the null hypothesis that economic growth does not Granger-cause FDI. The results also show strong evidence of causality at lag 1 and lag 3, where both the Z-bar and Z-bar tilde statistics are highly significant. This suggests that higher economic growth can help predict future FDI inflows, which is consistent with the idea that faster-growing economies tend to attract more foreign investment. However, similar to the previous results, lag 2 does not show statistical significance, suggesting that the relationship is not uniform across all lag lengths.

Overall, this finding indicates a bidirectional dynamic relationship between FDI and economic growth, where each variable helps predict the other over time.

## V. Conclusion

The regression results provide mixed evidence regarding the role of FDI in economic growth. In the pooled OLS model, FDI appears positive and statistically significant, suggesting that higher FDI inflows are associated with higher levels of GDP per capita. However, this model does not control for unobserved country characteristics or time-specific effects. Once country heterogeneity is controlled for in the Fixed Effects model, the coefficient of FDI becomes smaller and only weakly significant. When both country and time effects are included in the Two-Way Fixed Effects model, which is the preferred specification according to the Hausman test and the F-test for time effects, the coefficient of FDI becomes statistically insignificant. This suggests that after accounting for structural differences across countries and global time shocks, FDI does not show a strong contemporaneous structural impact on GDP per capita. In contrast, gross capital formation remains consistently positive and highly significant across models, highlighting the importance of domestic investment in supporting economic growth. Institutional quality, represented by government effectiveness, also appears to play a meaningful role in some specifications.

In Dumitrescu–Hurlin panel Granger non-causality test, the results indicate evidence of a bidirectional dynamic relationship between the two variables. Specifically, past values of FDI are found to help predict future economic growth at certain lag structures, while past economic growth also helps predict future FDI inflows. This finding suggests that although the structural regression model does not show a strong same-period effect of FDI on GDP per capita, FDI may still influence economic performance through dynamic and delayed channels. In other words, the contribution of FDI to economic growth may take time to materialize through mechanisms such as technology transfer, knowledge spillovers, and improvements in productivity. At the same time, stronger economic growth can attract additional foreign investment, creating a feedback relationship between the two variables.

Overall, the empirical findings suggest that the relationship between FDI and economic growth in Asian developing economies is dynamic and conditional rather than purely immediate. While FDI alone may not generate a significant short-term structural impact once country and global factors are controlled for, it still plays a role in shaping future economic performance. These results also highlight the importance of complementary factors such as domestic capital formation, institutional quality, and human capital in determining how effectively countries can benefit from foreign investment. Therefore, policies aimed at attracting FDI should be accompanied by improvements in economic institutions, infrastructure, and human capital development to enhance the absorptive capacity of host economies and maximize the long-term benefits of foreign investment.
