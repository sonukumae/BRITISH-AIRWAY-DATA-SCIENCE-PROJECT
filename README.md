# BRITISH-AIRWAY-DATA-SCIENCE-PROJECT
British Airways Data Science Job Simulation (Forage) – December 2025
Project overview
This repository contains work completed for the British Airways Data Science Job Simulation on Forage, focusing on how data science supports commercial and operational decision-making at scale.​

The simulation covers two main tasks:

Building a lounge eligibility lookup model to support airport planning at Heathrow Terminal 3.​

Developing a predictive model of customer holiday bookings using historical booking data.​

Task 1 – Lounge eligibility lookup
In this task, the goal was to estimate the percentage of passengers eligible for each lounge tier at Heathrow Terminal 3 without relying on exact future flight schedules or aircraft details.​

Objective
Create a reusable lookup table that estimates the share of passengers eligible for:

Tier 1: Concorde Room (hypothetical future tier at T3).

Tier 2: First Lounge.

Tier 3: Club Lounge.

Enable the Airport Planning team to forecast lounge demand under changing schedules and fleet strategies.​

Approach
Flights were grouped using scalable, schedule-agnostic categories:​

Time of day: Morning, Lunchtime, Afternoon, Evening.

Route type: Short-haul vs Long-haul.

Region: Europe, North America, Asia, Middle East.

For each group, lounge eligibility percentages were estimated as a share of total departing passengers, for example:​

Time of Day – Morning (e.g. LAX, IST, AMS): Tier 1 ≈ 0.27%, Tier 2 ≈ 3.52%, Tier 3 ≈ 13.48%.

Route Type – SHORT (e.g. FRA, IST, VIE): Tier 1 ≈ 0.34%, Tier 2 ≈ 4.40%, Tier 3 ≈ 16.85%.

Region – North America (e.g. LAX, ORD, JFK): Tier 1 ≈ 0.20%, Tier 2 ≈ 2.76%, Tier 3 ≈ 10.55%.

These percentages were derived from a representative sample schedule and designed to be applied as multipliers to any future flight list once flights are tagged by time-of-day, route type, and region.​

Key assumptions and scalability
Lounge eligibility patterns (premium cabins and frequent flyers) observed in the sample schedule are assumed to be structurally stable over time, even if exact routes or frequencies change.​

Time-of-day, route type, and region are robust drivers of premium demand and loyalty traffic and will remain relevant under future network changes.​

The output is a lookup table, not a per-flight model: any new schedule can be processed by assigning each flight to a group and multiplying seat counts by the relevant Tier 1–3 percentages.​

This method provides a flexible, scalable way to estimate lounge demand and to test scenarios such as increased long-haul flying, regional mix changes, or different daypart schedules.​

Task 2 – Customer booking prediction
In the second task, the focus shifted to commercial analytics: using customer booking data to predict which customers are likely to book a holiday.​

Objective
Predict the probability that a customer makes a holiday booking, using historical booking and flight data.

Identify which variables most strongly influence booking behaviour to inform proactive marketing and product strategy.​

Data exploration and preparation
Using the provided “Getting Started” Jupyter notebook as a base, the dataset (~50,000 records) was explored to understand distributions, data quality, and key variables.​
Important features included:​

Purchase lead time.

Flight details (route, departure hour).

Trip characteristics (length of stay).

Booking origin and customer preferences.

Data preparation steps (as described in the summary slide) included:​

Sampling 10,000 records for efficient experimentation.

Encoding categorical variables for tree-based modelling.

Preparing a supervised learning dataset with a binary booking outcome as the target.

Modelling approach
Algorithm: RandomForest Classifier, chosen for its good performance and built-in feature importance for interpretability.​

Validation: 5-fold cross-validation to obtain robust performance estimates.​

Evaluation metrics: ROC-AUC and Accuracy, alongside inspection of recall for the “booking” class.​

Reported performance from the summary slide:​

ROC-AUC: 0.75 (moderate discriminative performance).

Accuracy: 85%.

Booking recall: 7% (indicating that while overall accuracy is high, many positive bookings are still missed, likely due to class imbalance or decision threshold).

Feature importance and business insights
The RandomForest model highlighted several features as most predictive of booking likelihood:​

Purchase lead time.

Route.

Flight hour of day.

Length of stay.

Booking origin.

These findings suggest that booking timing, itinerary structure, and geography are critical signals for targeting marketing and offers earlier in the customer journey.​

Repository structure (suggested)
text
.
├─ data/
│  ├─ raw/                 # Original provided datasets (excluded or stubbed)
│  └─ processed/           # Cleaned/feature-engineered data (if saved)
├─ notebooks/
│  └─ customer_booking_model.ipynb
├─ lounge_eligibility/
│  └─ Lounge-Eligibility-Lookup-Template-Task-1-1.xlsx
├─ reports/
│  └─ Customer_Booking_Prediction_Summary.pptx
├─ src/
│  ├─ data_prep.py         # Cleaning and feature engineering scripts
│  ├─ train_model.py       # Model training & evaluation code
│  └─ lounge_lookup.py     # Helper functions to apply the lookup table
└─ README.md               # This file
How to reproduce
Clone the repository and create a Python environment with standard data science libraries (pandas, numpy, scikit-learn, matplotlib/seaborn).

Open notebooks/customer_booking_model.ipynb to run the data exploration, preprocessing, model training, and evaluation steps on the customer booking dataset.​

Use lounge_eligibility/Lounge-Eligibility-Lookup-Template-Task-1-1.xlsx as a template:

Tag any flight schedule by time of day, route type, and region.

Apply the Tier 1–3 percentages to estimate lounge-eligible passenger volumes per group.​

Skills demonstrated
Feature engineering and supervised learning with RandomForest on real-world style airline data.​

Model evaluation using cross-validation and metrics like ROC-AUC, accuracy, and recall.​

Interpreting feature importance to generate actionable commercial insights.​

Designing a scalable lookup-based model for operational planning under uncertain future schedules.​

Communicating results through a single-slide executive summary and structured Excel deliverables suitable for non-technical stakeholders.​
