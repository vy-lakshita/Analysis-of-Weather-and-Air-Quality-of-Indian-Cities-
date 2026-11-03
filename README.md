

# Analysis of Weather and Air Quality of Indian Cities

This project explores how pollutants and geographical conditions affect air quality across 74 Indian cities. It applies multivariate techniques in R (PCA, Factor Analysis, K-means clustering) to find the factors behind air pollution and group cities with similar profiles.

🔗 **[View the full report (website)](https://vy-lakshita.github.io/Analysis-of-Weather-and-Air-Quality-of-Indian-Cities-/)**

<img width="1344" height="960" alt="cluster visualization" src="https://github.com/user-attachments/assets/88a719e2-0efe-444d-98c0-fa7564e0e6fc" />

## Repository Contents

| File | Description |
|------|-------------|
| `Air.Rmd` | R Markdown source with all code and analysis |
| `Air.pdf` | PDF version of the report |
| `index.html` | HTML report (served via GitHub Pages) |
| `indian_weather_data.csv` | Dataset: one weather and air-quality snapshot per city |

## Dataset

74 cities and 24 columns, including:

- **Location:** latitude, longitude
- **Weather:** temperature, feels-like, pressure, humidity, cloud cover, visibility, wind speed, wind degree and direction, weather code
- **Pollutants:** CO, NO₂, O₃, SO₂, PM2.5, PM10

There are no missing values.

## Tools

R with `tidyverse`, `ggplot2`, `factoextra`, `psych`, `corrplot`, `plotly`, `maps`, `ggrepel`, `GGally`, `gridExtra`, `webshot2`.

## Techniques Used

- **Data preparation**
  - Split the data into numeric and categorical variables.
  - Standardised the numeric variables with `scale()` before PCA.
- **Principal Component Analysis (PCA)**
  - Used `princomp` on the scaled data.
  - Selected components with the eigenvalue > 1 rule.
  - Inspected loadings, scree plot, variable biplot and cos² plots.
- **Factor Analysis**
  - Checked suitability with the KMO test and Bartlett's test of sphericity.
  - Chose the number of factors from a scree plot.
  - Fitted 4 factors with varimax rotation and regression scores.
- **Feature engineering**
  - Added factor scores as new variables: `pollutants`, `geographic_cond`, `weather_cond`, `ozone`.
  - Binned weather codes and visibility into categories.
  - Assigned each city to a region of India from its lat/lon.
- **Exploratory Data Analysis**
  - Correlation heatmap, PM2.5 map of India, top-20 PM10 and PM2.5 bar charts coloured by wind direction.
  - Scatter plots of temperature vs PM2.5 and temperature vs pressure.
  - Interactive 3D plot (`plotly`) of wind speed, temperature and PM2.5.
- **K-means clustering**
  - Clustered cities on three factor scores: pollutants, weather and geography.
  - Chose k with the elbow and silhouette methods.
  - Ran k = 4 with `nstart = 25` and a fixed seed.

## Analysis

### PCA
- The first 5 components explain about **84%** of the variance, and the first 2 explain about **56%**.
- Component 1 is pollutant-dominated. Pollutants rise as wind speed and temperature fall.
- Component 2 is weather-dominated. Higher pollutant levels go with lower visibility.
- All pollutants cluster together in the biplot, so they are strongly positively correlated.

### Factor Analysis
- KMO is about 0.69 or higher, and Bartlett's test gives p ≈ 1e-293, so the data suits factor analysis.
- The four factors are:
  1. **Pollutants:** CO, O₃, SO₂, PM2.5, PM10
  2. **Geographic conditions:** latitude, longitude, pressure
  3. **Weather conditions:** weather code, humidity, visibility
  4. **Ozone:** NO₂, wind speed
- Communalities are high, so the factors represent the variables well.

### Correlations
- PM2.5, PM10, CO and SO₂ are strongly correlated, and NO₂ moderately.
- Temperature and feels-like are strongly correlated.
- Pressure is negatively correlated with temperature and feels-like.

## Key Insights

- **Northern cities** (Noida, Delhi, Faridabad, Kanpur, Lucknow, Patna, Agra, Karnal) are the most polluted. Likely contributors are **stubble burning**, low wind speed and unfavourable weather.
- **Coastal and water-adjacent cities** (Ahmedabad, Vadodara, Vapi, Mumbai, Chennai) have low pollution, helped by **proximity to the coast or a water body**.
- **Tourist and hill towns** (Dehradun, Shimla, Sangli, Udaipur, Bikaner) have little heavy industry and low pollution.
- **Manufacturing hubs** (Ambala, Thanesar, Karnal, Agra) are polluted. In Agra, tourism may also add to CO and NO levels.
- Other contributors in the north include livestock farming, heavy use of chemical fertilisers and pesticides, vehicle emissions, poor waste disposal and industrial non-compliance.

## Recommended Actions

- Promote **sustainable agricultural practices** (for example the Pusa bio-decomposer) and raise farmer awareness.
- Enforce **stricter rules and penalties** on industries that do not treat gases before release.
- Encourage **carpooling, household waste management and public transport**.
- **Incentivise crop diversification** with financial assistance for farmers.
- Develop **region-specific policies** for clusters of highly polluted cities with similar geography and weather.

## Limitations

- The data is a single snapshot per city, so there is no time-series or seasonal analysis.
- The causes listed in Key Insights (such as stubble burning) are interpretations and were not tested in the data.

## How to Run

1. Install R and RStudio.
2. Install the packages listed under Tools.
3. Open `Air.Rmd` and knit it to HTML or PDF.

## Author

Lakshita
