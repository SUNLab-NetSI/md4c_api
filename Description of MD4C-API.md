# Description of the API for Mobility Data for Communities (MD4C)

## Intro:

The MD4C API is being developed as a public-facing infrastructure designed to convert mobility data (MD) into meaningful behavioral indicators. The API will support a wide range of users, including researchers, policymakers, and community leaders, by providing structured and accessible data on mobility patterns.

## Objectives:

- Provide accessible mobility insights: Convert raw mobility data into indicators that describe meaningful movement patterns across neighborhoods.
- Address privacy concerns: Ensure all data shared via the API is aggregated and anonymized.
- Reduce bias in mobility data: Account for demographic and behavioral biases in the dataset.
- Enhance usability: Develop a user-friendly platform accessible to non-data scientists.

## Scope
Mobility data has different dimensions depending on the observation time, the geographical area, and the type of activities involved in mobility. To ensure anonymity and privacy, the API will serve mobility data at an adequate granularity while preserving its statistical and analytical value.
- **Temporal Scope**
    - For statistical purposes, the API will provide aggregated monthly movement insights rather than real-time or daily individual-level data.
    - This aggregation ensures that trends over time can be analyzed while preventing the identification of individual movement patterns.
- **Geographical Scope**
    - For privacy reasons, mobility flows will only be computed at the Census Tract level.
    - Data will be aggregated and only be reported if sufficient individual observations exist underneath to prevent re-identification (k-anonymity).
- **Activity Scope**
    - Mobility flows will be classified based on the type of activity associated with the movement.
    - To protect privacy, the API will only provide high-level activity categories, such as:Food (e.g., restaurants, cafés), Shopping (e.g., retail stores, malls), Recreation (e.g., parks, entertainment venues), Work (e.g., office spaces, job sites), Transport (e.g., transit stations, airports)
- **Frequency**
    - When possible we will also give information about how many users are moving frequently between the areas and how many of the movements are “explorations”, i.e., visits to places never visited before by users.


## Metrics
In the initial phase of the API, we will serve the following key mobility metrics: 

### Mobility Flows from and to Census Areas (by Month and Category)

This metric provides aggregate movement data between Census Tracts, categorized by the type of activity, monthly, and frequency.

Data Schema Example
```json
{
  "month": "2025-01",
  "origin_census_tract": "25025010100",
  "destination_census_tract": "25025010200",
  "category": "Shopping",
  "num_visits": 1250,
  "avg_duration_minutes": 45,
  "frequent_users": 800,
  "exploratory_users": 450
}
```
where:
- month: The time period of aggregation.
- origin_census_tract: The home location of the movements.
- destination_census_tract: The destination of the movement.
- category: The high-level activity type (Food, Shopping, Recreation, Work, Transport).
- num_visits: The total number of trips recorded between the two locations.
- avg_duration_minutes: The average duration of visits for this category.
- frequent_users: Number of users who regularly move between these locations.
- exploratory_users: Number of users visiting POIs from this category in this census tract for the first time.