# A/B Test for Mobile App Engagement - Data Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)

---

### Project Overview

This project aims to analyse the impact of a new recommendation feature on user engagement within a mobile app. An A/B test was conducted to compare the behaviour of users who had access to the recommendation feature (Group B - Treatment) versus those who did not (Group A - Control).

The key objectives of the analysis are:
- To determine if the new feature increases session length and user interactions.
- To analyse the feature usage and adoption rates within the treatment group.
- To provide actionable insights for improving user engagement and the app's functionality.

### Data Sources

The dataset includes user activity metrics recorded during the A/B test, specifically tracking the session length, interactions, and feature usage.

- **Mobile_App_Data.csv** — Contains user session data with the following key columns:
  - **User_ID**: Unique identifier for each user.
  - **Group**: Indicates whether the user is in the control group (A) or treatment group (B).
  - **Feature_Enabled**: A binary indicator (1 or 0) of whether the new recommendation feature was available.
  - **Session_Length**: Time spent by the user in the app (in minutes).
  - **Interactions**: The number of actions the user took during the session (e.g., clicks, scrolls).
  - **Used_Feature**: Indicates whether the user engaged with the new feature (1 for yes, 0 for no).

### Tools

- **Python on Google Colab Jupyter Notebook (pandas, scipy, matplotlib, seaborn)** — For data manipulation, statistical testing, and visualisation.
  - **pandas**: Used for loading, cleaning, and transforming the dataset.
  - **scipy.stats**: For conducting statistical tests like T-tests and Chi-Square tests.
  - **matplotlib and seaborn**: To create visualisations such as bar charts, box plots, and pie charts.

### Data Cleaning/Preparation

Steps performed to prepare the data for analysis:
1. **Loading the dataset**: The CSV file was loaded into a pandas DataFrame for manipulation and analysis.
2. **Handling missing values**: The dataset was inspected for missing values, and none were found.
3. **Data formatting**: Converted relevant columns to appropriate data types and grouped data based on the control/treatment groups for analysis.

### Exploratory Data Analysis

Initial questions investigated:
- How does the average session length compare between the control and treatment groups?
- Do users in the treatment group (with the recommendation feature) engage with the app more than those in the control group?
- What percentage of users in the treatment group use the new feature?

Key visualisations:
- **Average Session Length by Group**: Group B had a noticeably higher average session length compared to Group A.
- **Average Interactions by Group**: Users in Group B engaged more than those in Group A, with over triple the number of interactions.
- **Feature Usage in Treatment Group**: A pie chart showed that 45% of users in Group B actively used the new feature.

### Data Analysis

Statistical tests conducted:

- **T-Test for Session Length**:
  ```python
  t_stat, p_val = stats.ttest_ind(control_group['Session_Length'], treatment_group['Session_Length'])
  print(f'Session Length T-Test: t-statistic = {t_stat}, p-value = {p_val}')
This test compared session lengths between Groups A and B, revealing a statistically significant difference in time spent.

- **T-Test for Interactions**:
  ```python
  t_stat, p_val = stats.ttest_ind(control_group['Interactions'], treatment_group['Interactions'])
  print(f'Interactions T-Test: t-statistic = {t_stat}, p-value = {p_val}')
The test indicated a significant increase in the number of interactions in Group B versus Group A.

- **Chi-Square Test for Feature Usage**:
  ```python
  chi2_stat, p_val, dof, expected = stats.chi2_contingency(pd.crosstab(df['Group'], df['Used_Feature']))
  print(f'Chi-Square Test: chi2-statistic = {chi2_stat}, p-value = {p_val}')
This test showed that the usage rate of the new feature in Group B was statistically significant.

### Results/Findings

**Session Length**: Users in Group B (with the recommendation feature) spent significantly more time in the app compared to Group A (control). On average, Group B users spent 20 minutes, while Group A users spent around 10 minutes per session.

**Interactions**: Group B also had a significantly higher number of interactions, indicating that the new feature promotes greater user engagement.

**Feature Usage**: Despite the positive impact, only 45% of users in Group B interacted with the new feature, suggesting there is room to improve feature adoption.

### Recommendations

**Feature Rollout**: The new recommendation feature should be rolled out to all users, as it effectively increases both session length and user interactions.

**Improve Feature Adoption**: Investigate ways to increase feature usage, such as improving the feature's visibility, providing tutorials or onboarding, and gathering feedback from users who did not engage with it.

**Further Enhancements**: Explore how the recommendation engine can be expanded with more personalised content to further drive engagement.
