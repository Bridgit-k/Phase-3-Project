# SyriaTel Customer Churn Prediction 

## Business Problem
SyriaTel, a telecommunications company, is facing a challenge with customer retention.
Losing a customer ("churn") is costly, as acquiring new customers is significantly more expensive than retaining existing ones.

## The Goal
Build a machine learning model to predict which customers are at risk of leaving. 
This allows the business to intervene proactively with discounts or customer service outreach before the customer cancels.

## Data Understanding
The dataset contains information on approximately 3,000 customers, including:
* Demographics: Account length, location (State/Area Code).
* Usage: Minutes talked (Day/Evening/Night/International).
* Services: International Plan, Voicemail Plan.
* Target Variable: Churn (True/False).

Note: The dataset was checked for imbalances. Churners make up only ~14% of the population, requiring careful stratification during modeling.

## Methodology
We followed a standard iterative data science workflow:
* Preprocessing: Converted categorical variables (Plans) to binary (0/1) and removed non-predictive features (Phone Numbers).
* Modeling:Baseline: Logistic Regression (Scaled data).
* Final Model: Decision Tree Classifier (Tuned via GridSearchCV).
* Evaluation: We prioritized Recall as our primary metric.Why Recall? In churn prediction, a "False Negative" (missing a churner) is more expensive than a "False Positive" (giving a discount to a loyal customer). We want to catch as many churners as possible.

## Results & Evaluation
The tuning process yielded significant improvements in identifying at-risk customers.

Model                              Recall Score (Churn Class)  Interpretation
Logistic Regression (Baseline)     ~23%                         Missed the vast majority of churners.
Decision Tree (Final)              ~65%                         Successfully identified nearly 2/3rds of at-risk customers.

The Decision Tree model tripled our ability to catch churners compared to the baseline.

## Key Findings & Business Insights
By analyzing the Feature Importance of our final model, we identified the top drivers of churn:
### The "Bill Shock" Effect
Total Day Minutes was the first predictor of churn.
Loyal Customers: Average 175 minutes per day.
Churned Customers: Average 207 minutes per day.
Conclusion: The most active users are the ones leaving. 
This strongly suggests they are exceeding plan limits and facing high overage charges, prompting them to switch to competitors with "Unlimited" options.

### Customer Service Fatigue
Customer Service Calls was the second predictor.
Data shows a sharp increase in churn probability after the 3rd call to customer service.
Multiple calls indicate unresolved issues and frustration.

## Recommendations
Based on the data, we propose the following actionable steps for SyriaTel:
* Launch an "Unlimited Day" Plan: Target "Power Users" (those exceeding 200 minutes per day) with a promotional upgrade to a flat-rate plan. 
This prevents the "Bill Shock" that is currently driving them away.

* Implement a "3-Call" Red Flag: Update the call center software to automatically flag customers calling for the 3rd time. Route these calls immediately to a "Retention Specialist" empowered to offer solutions or discounts to resolve the friction.

* International Plan Review: Further investigate the pricing structure of international plans, as this was also identified as a key risk factor.

## Next Steps
* Cost-Benefit Analysis:
We have a model that finds churners. But does saving them cost more than letting them go?"
My next step would be to calculate the Return on Investment of this model. We need to determine if giving a $20 discount to the customers identified by the model is profitable compared to the revenue lost if they leave.

* Test the solutions you come up with in a small portion before implementing it to the whole business.
I recommend running a 3-month Pilot Program. We will take the top 1,000 customers identified as 'High Risk' by the model.
Group A (500 people): Gets the new 'Unlimited Plan' offer.
Group B (500 people): Gets nothing (Control Group).
The goal is to measure if the offer actually reduces churn rates or not.

For a detailed walkthrough of the code and analysis, please refer to the ipynb in this repository.
