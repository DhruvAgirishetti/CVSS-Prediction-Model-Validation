# CVSS Score Prediction Model

A prototype machine learning pipeline that parses National Vulnerability Database (NVD) JSON data to train and validate a model for predicting CVSS Base Scores. The model extracts a CVE's vector string, reading them individually, along with vulnerability descriptions, to measure how accurately linear regression models can predict severity ratings.

**Project Status:** Phase 1 (Model Validation) is complete. This prototype serves as a foundation for a live prediction engine, which will be integrated into a full-scale project. 

## What The Project Does

It executes an end-to-end 'scikit-learn' engineering pipeline that transforms unstructured text descriptions via hashing vectorizations while concurrently hot-encoding structural metrics. The current version focuses on fitting an optimized LightGBM gradient-boosted tree regressor to the dataset and running validation checks to test prediction accuracy on a standard '0.0' to '10.0' scale. 

## Key Pipeline Features
* **Cross-Version Normalization:** Bridges data gaps between legacy CVSS v2 and modern CVSS v3, v3.1 & v4 data structures during preprocessing.
* **Hybrid NLP & Tabular Pipeline:** Combines textual context (vulnerability descriptions) with discrete metric features (attack vectors, privileges required, etc).
* **High-Throughput Vectorization:** Implements a "TF-IDF Vectorizer" to look at important words in the descriptions, making the model more accurate compared to using a "Hashing Vectorizer," which suffered from hash collisions and risked breaking the model by introducing empty feature space when the allocated size exceeded what was actually used in reality. 
* **Bounded Scoring Logic:** Enforces mathematical scoring constraints via numpy clipping and ceil rounding to perfectly mirror standard NVD scoring.

## Tech Stack
* **Core Language:** Python
* **Data Processing** Pandas, NumPy, JSON, Glob
* **Machine Learning** LightGBM, Scikit-Learn (Pipelines, ColumnTransformers, TfidfVectorizer, OneHotEncoder)
* **Visualization**: Seaborn, Matplotlib

## Performance Metrics & Output

The Pipeline splits the parsed data into an 80/20 split for training & validation. It automatically prints out statistical evaluation metrics vs. the real baseline values to prove its accuracy:
* **The Dataset split:** Training size: 194683 | Validation size: 48660

* --- MODEL VALIDATION METRICS ---
* **Training Data R² Score:   0.9850**
* **Validation Data R² Score: 0.9815**
* **Variance Gap:             0.0035**

* --- MODEL PERFORMANCE METRICS ---
* **Mean Absolute Error (MAE): 0.1136**
* **Mean Squared Error (MSE):  0.0643**
* **R-squared (R²) Score:      0.9797**
<img width="989" height="590" alt="Plot Final_Publish" src="https://github.com/user-attachments/assets/41e24166-9f48-4c80-a163-00cfb0ebac53" />









