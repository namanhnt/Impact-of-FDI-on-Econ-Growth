# Impact of FDI on Economic Growth of Asian Developing Countries

![FDI](https://github.com/user-attachments/assets/c025c975-9b94-4272-bf21-5645bfb8248d)

## I. Introduction
My interest in studying the relationship between foreign direct investment (FDI) and economic growth sparked during my Master’s studies. While working on my econometrics dissertation, I became curious about why many developing countries in Asia have experienced rapid economic growth over the past few decades and how international investment has influenced that progress.

In recent centuries, Asia has become one of the most notable emerging markets for global investment. According to the World Investment Report 2025 ([UNCTAD](https://unctad.org/publication/world-investment-report-2025?utm_source=chatgpt.com)), the region received the highest level of FDI inflows worldwide, with $605 billion invested in 2024. This raised an interesting question for me: Does foreign investment truly help economies grow, or do fast-growing economies simply attract more foreign investors?

The project focuses on analyzing the panel data of 13 Asian developing countries in the span of 2000-2023. In this remake of my Master's dissertation, I have expanded the variable selection and included a new regression model. The study now also includes automated data extraction from the World Bank API. This README provides a brief overview of the project, while the full data preparation, exploratory analysis, and regression results can be found in the three Jupyter Notebooks.

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

Four panel regression models are used: Pooled OLS, One-way Fixed Effects, Two-way Fixed Effects, and Random Effects models. The Hausman test and F-test for time effects are applied to determine the most appropriate model. In addition, the Dumitrescu–Hurlin panel Granger causality test is used to explore the direction of causality between FDI and economic growth across countries.

## III. Data Gathering
In this project, I use macroeconomic data from the World Bank through its public data API. The World Bank provides a wide range of economic indicators for countries around the world, such as foreign direct investment, GDP, trade, infrastructure, and institutional quality. These datasets are compiled from national statistical agencies and international organizations, making them a reliable source for cross-country economic analysis.

<img width="1413" height="418" alt="image" src="https://github.com/user-attachments/assets/4f9db9fd-7601-4b41-af04-4d865a1c7195" />

Regarding the country selection, I have excluded Uzbekistan, Thailand, Jordan, Sri Lanka, Kazakhstan, Kyrgyzstan, Turkmenistan, Mongolia, and Myanmar from the dataset due to their substantial missing data, with over 30% of observations missing.

To ensure the consistency of data for the modelling, a small number of missing observations across several variables were addressed using linear interpolation within each country over time. Interpolation works by inferring the missing values through patterns or trends in the data.

## IV. Results

### Exploratory Data Analysis
- **Hanoi Hourly AQI Level (From March 2023 to March 2024)**
- **Hanoi Hourly AQI Level (From March 2023 to March 2024)**

### Regression Analysis
- **Hanoi Hourly AQI Level (From March 2023 to March 2024)**
- **Hanoi Hourly AQI Level (From March 2023 to March 2024)**

