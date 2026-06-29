# CVSS-Prediction-Model-Validation

A prototype machine learning pipeline that parses National Vulnerability Database (NVD) JSON data to train and validate a model for predicting CVSS Base Scores. The model extracts a CVE's vector string, reading them individually, along with vulnerability descriptions, to measure how accurately linear regression models can predict severity ratings.

## What The Project Does

It executes an end-to-end 'scikit-learn' engineering pipeline that transforms unstructured text descriptions via hashing vectorizations while concurrently hot-encoding structural metrics. The current version focuses on fitting a linear regression model to the dataset and running validation checks to test prediction accuracy on a standard '0.0' to '10.0' scale. 

## Key Pipeline Features
* **Cross-Version Normalization:** Bridges data gaps between legacy CVSS v2 and modern CVSS v3,v3.1 & v4 data structures during preprocessing.
* **Hybrid NLP & Tabular Pipeline:** Combines textual context (vulnerability descriptions) with discrete metric features (attack vectors, privileges required, etc).
* **High-Throughput Vectorization:** Implements memory-efficient 'Hashing Vectorizer' to process 217k+ historical records smoothly
* **Bounded Scoring Logic:** Enforces mathematical scoring constraints via numpy clipping and ceil rounding to perfectly mirror standard NVD scoring.

## Tech Stack
* **Core Language:** Python
* **Data Processing** Pandas, NumPy, JSON, Glob
* **Machine Learning** Scikit-Learn (Pipelines, ColumnTransformers, HashingVectorizer, OneHotEncoder)
* **Visualization**: Seaborn, Matplotlib
