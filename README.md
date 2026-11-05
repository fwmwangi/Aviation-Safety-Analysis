# Commercial Aviation Safety Analysis

## 1. Business Problem

Our consulting firm was contracted by an aviation and airline insurer to evaluate the safety profiles of various commercial and private aircraft. The client's primary objective is to minimize risk by identifying airplane manufacturers (Makes) and specific airplanes (Models) that exhibit:

1. A low rate of total aircraft destruction in the event of an incident.
2. A low likelihood of fatal or serious passenger injuries.

Additionally, the client requested an analysis of external variables to better understand general risk factors that impact flight safety. This analysis will guide the insurer's underwriting guidelines and risk assessment models for modern, professionally built aircraft.

## 2. Data Overview & Preparation

The analysis is based on the National Transportation Safety Board (NTSB) aviation accident database. To ensure the recommendations apply to the client's target market (active, professionally built aircraft), the following strict data cleaning and filtering protocols were applied:

* **Timeframe:** Filtered for events from 1983 onwards to account for a maximum 40-year airframe lifespan.
* **Build Type:** Excluded amateur-built aircraft (`Amateur.Built == 'No'`).
* **Aircraft Type:** Restricted strictly to airplanes (`Aircraft.Category == 'Airplane'`).

### 2.1 Key Metrics Constructed

* **Estimated Occupants:** Calculated by summing all reported injuries and uninjured passengers.
* **Injury Severity Rate:** The fraction of fatal and serious injuries over the total estimated occupants (`fatal_serious_fraction`).
* **Destruction Rate:** A binary indicator (1 = Destroyed, 0 = Minor/Substantial Damage) to evaluate airframe survivability.

## 3. Exploratory Data Analysis (EDA) & Methodology

Due to the catastrophic but rare nature of aviation accidents, the injury data is highly zero-inflated (the majority of incidents result in zero serious injuries). Relying purely on mean averages is statistically dangerous. Therefore, our EDA utilized robust statistical measures and visualizations to understand the structure of the data:

* **Minimum Sample Sizes:** Makes were required to have a minimum of 50 historical events, while specific models required at least 20 events (10 for large jets) to be considered statistically robust.
* **Distributional Analysis:** Horizontal bar charts were paired with Violin and Strip plots to visualize the true spread of the injury rates, proving that the low averages were not just artifacts of outliers.

## 4. Recommendations & Findings

### 4.1 Recommended Manufacturers and Specific Airplanes

Based on the passenger threshold of 20, we recommend the following airframes for the insurer's portfolio:

**Small Aircraft (<= 20 Occupants):**
* **Recommended Manufacturers (Makes):** Cessna, Piper, and Beech have established massive historical flight volumes while maintaining exceptionally low severe injury fractions and destruction rates.
* **Recommended Specific Airplanes (Models):** The Cessna 172, Cessna 152, and Piper PA-28 variants stand out as the safest specific airframes for private and small commercial policies.
* *Supporting Evidence:* `images/small_models_injury.png` and `images/small_makes_violin.png`.

**Large Aircraft (> 20 Occupants):**
* **Recommended Manufacturers (Makes):** Boeing, McDonnell Douglas, and Airbus represent the safest large-scale manufacturers.
* **Recommended Specific Airplanes (Models):** The Boeing 737 series demonstrates an incredibly dense clustering of zero-injury events across thousands of incidents, making it a highly insurable commercial airframe.
* *Supporting Evidence:* `images/large_models_injury.png` and `images/large_makes_strip.png`.

### 4.2 Relationship Between Incident Factors and Safety Outcomes

To further assist underwriting, we analyzed two key factors at play in aviation incidents:

**Factor 1: Weather Condition (VMC vs. IMC)**
* **Analysis:** Accidents occurring in Instrument Meteorological Conditions (IMC - poor visibility/weather) show a drastically higher mean injury severity and aircraft destruction rate compared to Visual Meteorological Conditions (VMC).
* **Recommendation:** The insurer should mandate strict IFR (Instrument Flight Rules) certification and modern avionics requirements for policies covering flight in IMC.
* *Supporting Evidence:* See `images/weather_factor.png` for injury and destruction rate comparisons.

**Factor 2: Engine Type**
* **Analysis:** Reciprocating engines (common in older, smaller aircraft) carry the highest rates of destruction and passenger injury. Turbo Fan and Turbo Jet engines (common in modern commercial aviation) are significantly safer.
* **Recommendation:** Premium discounts can confidently be applied to commercial fleets utilizing modern Turbo Fan engines.
* *Supporting Evidence:* See `images/engine_factor.png` for summary statistics and distributions by engine class.

## 5. Repository Structure

```text
.
├── README.md                                  # Project overview and conclusions
├── data/                                      
│   ├── AviationData.csv                       # Original NTSB raw data (not tracked in Git if large)
│   ├── USState_Codes.csv                      # State code lookup
│   └── aviation_cleaned.csv                   # Cleaned dataset ready for EDA
├── notebooks/                                 
│   ├── Aviation_Accidents_Cleaning.ipynb      # Phase 1: Pandas data wrangling & cleaning
│   └── Aviation_Accidents_Data_Analysis.ipynb # Phase 2: EDA, Statistics, & Visualizations
└── images/                                    # Exported visualization PNGs
    ├── makes_injury_rates.png
    ├── small_makes_violin.png
    ├── large_makes_strip.png
    ├── small_models_injury.png
    ├── large_models_injury.png
    ├── weather_factor.png
    └── engine_factor.png
    