# Uber Traffic & Pricing Dynamics Framework

This repository hosts a multi-source data integration pipeline and behavioral research report evaluating the structural correlation between urban traffic congestion, localized environmental anomalies, and the real-time surge-pricing mechanics deployed by ride-sharing platforms like Uber.

## 📌 Project Overview
Urban gridlock directly alters the supply-demand curves of ride-sharing ecosystems. When traffic throughput drops, vehicle circulation loops open up, causing vehicle availability to plummet while consumer demand builds up. 

This project implements an automated, timestamp-synchronized pipeline that aggregates disparate telemetry data (traffic volume, meteorological records, and public calendars) to create an integrated, ML-ready dataset for forecasting hourly bottleneck spikes at key road junctions.

## 🛠️ Data Integration Architecture
The data pipeline merges variables across identical timestamp indexes to handle three primary real-world data streams:
1. **Traffic Velocity Metrics:** Historic hourly volume metrics across localized road junctions.
2. **Meteorological Degradation Matrix:** Ingestion of temperature variations, precipitation (rain/snow fractions), humidity levels, and wind speed anomalies that trigger defensive driving.
3. **Socio-Cultural Anomalies:** Tracking high-density public events (concerts, sporting tournaments) and public holidays that re-route traditional weekday commuter patterns.

### Pipeline Features Implemented:
* **Missing Value Imputation:** Resolves sensor or logging dropouts using localized rolling median inputs grouped by junction.
* **Feature Scaling:** Implements MinMaxScaler optimization to bound all numerical features within a `[0, 1]` range, ensuring stable convergence metrics for downstream Machine Learning models (e.g., XGBoost, LSTMs).

## 📊 Dataset Structure
The generated `Integrated_Dataset.csv` contains the following structured attributes:
* `Timestamp`: Synchronized date-time boundary (hourly intervals).
* `Junction`: Specific roadway identification node.
* `Traffic_Volume`: Extrapolated baseline vehicle throughput.
* `Temperature_C` / `Precipitation_mm` / `Humidity_Pct` / `Wind_Speed_kmh`: Meteorological attributes.
* `Is_Event` / `Event_Type`: Encoded structural and community calendar anomalies.
* `*_Scaled`: Normalized variants of all core mathematical arrays.

## 📈 Key Research Insights
The analytical report included in this research indicates that gross marketplace pricing follows the structured baseline:

$$\text{Fare} = \text{Base Fare} + (\text{Cost per Minute} \times \text{Time}) + (\text{Cost per Mile} \times \text{Distance}) \times f_{\text{surge}}$$

* **Time Premium Inflation:** Congestion shifts the consumer pricing burden heavily toward the time component, protecting driver opportunity costs but causing high pricing volatility.
* **Precipitation Drops:** Heavy rain events show an average structural capacity degradation of $15\text{--}30\%$ across major urban junctions, triggering aggressive algorithmic surge pricing modifiers ($f_{\text{surge}}$) to re-establish supply equilibrium.

## 🚀 How to Run the Pipeline
Ensure you have `pandas`, `numpy`, and `scikit-learn` installed:
```bash
pip install pandas numpy scikit-learn
