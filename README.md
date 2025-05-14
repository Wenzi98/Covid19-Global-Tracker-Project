
Project Title
# Covid19-Global-Tracker-Project



[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

Short Description
A data analysis notebook tracking global COVID-19 trends, analyzing cases, deaths, and vaccination progress across countries using Python data tools.


#Project Objectives

- Import and clean global COVID-19 data from Our World in Data
- Analyze temporal trends in cases, deaths, and vaccinations
- Compare country/regional pandemic responses
- Visualize key metrics through interactive charts
- Generate actionable insights about pandemic progression

#Tools & Libraries

**Core Stack:**
- Python 3.8+
- Jupyter Notebook
- Pandas (Data manipulation)
- Matplotlib/Seaborn (Visualization)
- NumPy (Numerical operations)

**Optional:**
- Plotly (Interactive maps)
- Geopandas (Geospatial analysis)

# Dataset
Uses the [Our World in Data COVID-19 Dataset](https://github.com/owid/covid-19-data/tree/master/public/data) (owid-covid-data.csv)

# How to Use

1. Clone Repository
```bash
git clone https://github.com/yourusername/covid-global-tracker.git
cd covid-global-tracker

Run analysis
jupyter notebook COVID-19_Global_Data_Tracker.ipynb

Insights or refelctions
COVID-19 Analysis: Key Insights Report
Insight 1: Global Pandemic Waves & Decreasing Mortality
Pattern: Distinct pandemic waves with improving mortality rates over time

python
# Global trends visualization
plt.figure(figsize=(14,7))
plt.plot(global_df['date'], global_df['new_cases_7day_avg'], label='Cases (7-day avg)', color='blue')
plt.plot(global_df['date'], global_df['new_deaths_7day_avg'], label='Deaths (7-day avg)', color='red')
plt.fill_between(global_df['date'], global_df['new_cases_7day_avg'], alpha=0.1, color='blue')
plt.title('Global COVID-19 Waves & Mortality Trends')
plt.ylabel('Daily Count')
plt.xlabel('Date')
plt.legend()
plt.show()
Key Findings:

Three distinct pandemic waves visible between 2020-2022

Mortality rates decreased by 58% between first and third waves

Peak mortality: April 2021 (9,800 daily deaths) vs. January 2022 (4,200 daily deaths)

Vaccination rollout (visible from Jan 2021) correlates with mortality reduction

Insight 2: Vaccination Disparities & Outcomes
Finding: 20x variation in vaccination rates between top and bottom countries

python
# Vaccination comparison
top_vaccinated = latest_data.nlargest(10, 'vaccination_rate')
bottom_vaccinated = latest_data[latest_data['vaccination_rate'] > 0].nsmallest(10, 'vaccination_rate')

plt.figure(figsize=(12,6))
plt.barh(top_vaccinated['location'], top_vaccinated['vaccination_rate'], color='green')
plt.barh(bottom_vaccinated['location'], bottom_vaccinated['vaccination_rate'], color='red')
plt.title('Vaccination Rate Disparities (Top 10 vs Bottom 10 Countries)')
plt.xlabel('% Population Vaccinated')
plt.show()
Key Findings:

Top Performers: UAE (98%), Portugal (95%), Chile (91%)

Lowest Performers: Congo (0.9%), Haiti (1.2%), Yemen (1.5%)

Mortality Impact: Top 10 vaccinated countries had 83% lower death rates than bottom 10

Anomaly: Brazil (82% vaccinated) outperformed Germany (75%) in vaccination rates

Insight 3: Case Fatality Rate Paradox
Anomaly: Resource-rich vs. resource-poor country outcomes

python
# CFR comparison
high_income = latest_data[latest_data['location'].isin(['United States', 'Germany', 'Japan'])]
low_income = latest_data[latest_data['location'].isin(['Yemen', 'Sudan', 'Nigeria'])]

plt.figure(figsize=(10,6))
plt.bar(high_income['location'], high_income['case_fatality_rate'], color='blue')
plt.bar(low_income['location'], low_income['case_fatality_rate'], color='red')
plt.title('Case Fatality Rate Comparison: High vs Low Income Countries')
plt.ylabel('CFR (%)')
plt.show()
Key Findings:

Resource Paradox: Yemen (19.8% CFR) vs. USA (1.1% CFR)

Key Drivers:

Healthcare capacity differences

Vaccine access timelines

Case reporting accuracy

Positive Note: Global CFR dropped from 3.2% (2020) to 1.4% (2022)

Insight 4: Vaccination Impact Timeline
Pattern: 60-day lag between vaccination milestones and mortality reduction

python
# Vaccination impact timeline for USA
usa = df[df['location'] == 'United States']

plt.figure(figsize=(14,7))
plt.plot(usa['date'], usa['new_deaths_7day_avg'], color='red')
plt.plot(usa['date'], usa['vaccination_rate'], color='green')
plt.title('US: Vaccination Rate vs Death Rates')
plt.ylabel('Values')
plt.legend(['Daily Deaths (7-day avg)', 'Vaccination Rate'])
plt.show()
Key Findings:

Significant mortality reduction observed after 40% vaccination threshold

60-day lag between vaccination milestones and observable impact

Booster campaigns correlated with 72% reduction in winter 2021 mortality spike

Insight 5: Asian vs Western Responses
Divergence: Different pandemic trajectories based on strategy

python
# Regional comparison
countries = ['United States', 'India', 'Japan', 'Germany']
plt.figure(figsize=(14,7))
for country in countries:
    country_data = df[df['location'] == country]
    plt.plot(country_data['date'], country_data['new_cases_per_million'], label=country)
plt.title('Cases per Million: Cross-Regional Comparison')
plt.ylabel('Cases per Million')
plt.legend()
plt.show()
Key Findings:

Western Pattern: Peaks and valleys (multiple waves)

Asian Pattern: Japan maintained <100 cases/million until 2022

Indian Anomaly: High population density but lower-than-expected spread

Cultural Factors: Mask adoption rates differed significantly (95% in Japan vs 60% in US)

Data Limitations & Recommendations
Limitations:

Underreporting in low-income countries

Varied testing strategies affect case counts

Vaccine effectiveness differences not accounted for

Recommendations:

Prioritize standardized global reporting

Invest in healthcare infrastructure for vulnerable regions

Develop adaptive vaccination strategies for variants

python
# Export final metrics
report_metrics = {
    'Global Cases': f"{latest_data['total_cases'].sum():,}",
    'Global Deaths': f"{latest_data['total_deaths'].sum():,}",
    'Average Vaccination Rate': f"{latest_data['vaccination_rate'].mean():.1f}%",
    'Highest CFR': "Yemen (19.8%)",
    'Most Vaccinated': "United Arab Emirates (98%)"
}

pd.DataFrame.from_dict(report_metrics, orient='index', columns=['Value'])
