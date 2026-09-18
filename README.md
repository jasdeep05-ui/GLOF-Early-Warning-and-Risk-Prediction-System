# GLOF-Early-Warning-and-Risk-Prediction-System
# 🌊 GLOF Risk Prediction — India

An end-to-end machine learning project for **Glacial Lake Outburst Flood (GLOF) risk prediction** across the Indian Himalaya.

The project uses environmental and geographic characteristics such as **elevation, lake area, glacier retreat rate, slope, rainfall, distance from glacier, and seismic activity** to classify glacial lakes into **high- or low-risk categories**.

An interactive **Streamlit dashboard** provides risk predictions, geographic visualizations, SHAP-based explanations, and illustrative alert information.

> **Project Status:** Proof of Concept
> This project demonstrates an end-to-end machine learning workflow and is **not a production-ready early-warning system**.

---

## 📌 Project Overview

Glacial Lake Outburst Floods occur when water stored in glacial lakes is suddenly released, potentially causing severe downstream flooding.

This project explores how machine learning can be used as a **risk-screening tool** for glacial lakes across six Himalayan regions of India:

* Jammu & Kashmir
* Ladakh
* Himachal Pradesh
* Uttarakhand
* Sikkim
* Arunachal Pradesh

The project covers the complete machine learning workflow:

**Data Generation → Data Preprocessing → Exploratory Data Analysis → Model Training → Model Evaluation → Explainable AI → Dashboard Deployment**

---

## 🎯 Objectives

* Develop a machine learning model for preliminary GLOF risk classification.
* Analyze environmental and geographic factors associated with potential risk.
* Compare multiple machine learning algorithms.
* Evaluate model performance using synthetic and held-out real-lake data.
* Provide interpretable predictions using **SHAP**.
* Build an interactive dashboard for visualization and risk assessment.
* Create a foundation for future integration with satellite imagery and real-time monitoring.

---

## 📊 Dataset

The dataset contains approximately **790 glacial lake records**, combining:

### Real Lakes

10 real glacial lakes were manually entered using information based on published reports and news coverage of documented events.

Examples include:

* **South Lhonak Lake** — associated with the October 2023 Sikkim GLOF
* **Chorabari Lake** — associated with the 2013 Kedarnath disaster
* **Parechu Lake** — associated with the 2005 outburst in Himachal Pradesh

### Synthetic Lakes

Approximately **780 synthetic lake records** were generated to expand geographical coverage because a sufficiently large publicly available dataset of real, labeled GLOF-risk observations was not available for this project.

Synthetic risk labels are generated using a weighted score based on factors including:

* Lake area
* Glacier retreat rate
* Slope
* Rainfall
* Distance from glacier
* Seismic activity

### ⚠️ Important Dataset Limitation

Because the synthetic risk labels are derived from the same features subsequently used by the machine learning models, strong performance on synthetic data **does not represent real-world predictive accuracy**.

To reduce this issue, the 10 real lakes are completely held out from:

* Training
* Validation
* Model selection

They are evaluated separately as an independent test set.

The current model correctly classifies **8 of the 10 real lakes (80%)**. However, this is a very small evaluation set and should be considered an **initial indication of generalization rather than a definitive real-world performance measurement**.

---

## 🧠 Machine Learning Models

Four classification algorithms are trained and compared:

1. **Logistic Regression**
2. **Decision Tree**
3. **Random Forest**
4. **Gradient Boosting**

The models are compared using validation performance, with **F1 score** used for model selection.

The selected model is then evaluated on:

* Held-out synthetic test data
* The 10 real lakes

The final selected model is saved for use by the Streamlit application.

---

## 🔄 Machine Learning Pipeline

```text
                    GLOF Dataset
                         │
                         ▼
                Data Preprocessing
                         │
                         ▼
              Exploratory Data Analysis
                         │
                         ▼
                Train / Validation Split
                         │
                         ▼
       ┌─────────────────────────────────┐
       │       Model Comparison          │
       │                                 │
       │  Logistic Regression            │
       │  Decision Tree                  │
       │  Random Forest                  │
       │  Gradient Boosting              │
       └─────────────────────────────────┘
                         │
                         ▼
                Best Model Selection
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
     Synthetic Test Set       10 Real Lakes
              │                     │
              └──────────┬──────────┘
                         ▼
                 Model Explanation
                       (SHAP)
                         │
                         ▼
               Streamlit Dashboard
```

---

## 🖥️ Interactive Dashboard

The project includes a Streamlit-based dashboard with several components.

### 🔮 Risk Prediction

Users can enter lake characteristics and receive a predicted GLOF risk classification.

### 🗺️ Lake Risk Map

Displays glacial lakes geographically and provides a visual representation of their predicted risk categories.

### 🔥 Risk Heatmap

Shows the geographical concentration of predicted risk across the study regions.

### 📈 Lake Growth Estimate

Provides an **illustrative lake-growth estimate** based on an assumed growth rate.

> This is currently a placeholder and does **not** analyze real satellite imagery.

### 🧩 Explainable AI

SHAP is used to provide feature-level explanations of model predictions and help understand which variables contribute to a prediction.

### 🚨 Alert System

Displays example alerts generated from the model's predictions on the existing dataset.

> These are **not real-time emergency alerts** and are not connected to a live monitoring system.

---

## 🧩 Explainable AI

The project incorporates **SHAP (SHapley Additive exPlanations)** to improve model interpretability.

Instead of presenting only a risk classification, the dashboard can show how different input features contributed to the prediction.

This provides greater transparency into the machine learning decision-making process.

---

## ⚠️ What This Project Is NOT

This project should **not** be interpreted as a deployed disaster-warning system.

It currently does not include:

* ❌ Real-time monitoring
* ❌ Live sensor feeds
* ❌ Real satellite imagery analysis
* ❌ Remote sensing-based lake expansion detection
* ❌ Operational emergency alerts
* ❌ A large real-world labeled GLOF dataset

The current implementation is a **machine learning proof of concept** that demonstrates how such a system could be developed.

---

## 📉 Limitations

### Synthetic Training Data

Most records are synthetically generated, and the labels are derived from a predefined scoring formula.

Therefore, high model performance on synthetic data should not be interpreted as real-world predictive accuracy.

### Limited Real-World Validation

Only 10 real lakes are currently available for independent evaluation.

The resulting 80% classification rate is therefore based on a very small sample.

### No Remote Sensing

The current system does not process satellite imagery or other remote-sensing data.

### No Real-Time Monitoring

The alert system uses existing model predictions rather than live environmental or monitoring feeds.

### Limited Feature Set

The current feature set focuses primarily on geographic and climatic variables.

Additional factors relevant to GLOF hazard assessment—such as **moraine dam characteristics, lake bathymetry, and detailed glaciological measurements**—are not currently included because suitable data was not available at the required scale.

### Model Selection

The notebook trains and compares multiple algorithms, and the model with the best validation F1 score is saved.

Therefore, the final saved algorithm may change if the dataset or implementation changes.

Fixed random seeds are used to improve reproducibility.

---

## 📁 Project Structure

```text
glof-risk-prediction/
│
├── README.md
├── requirements.txt
├── generate_dataset.py
├── GLOF_Risk_Prediction.ipynb
├── app.py
│
├── glof_dataset.csv
├── glof_model.joblib
├── glof_scaler.joblib
├── glof_feature_cols.joblib
├── glof_region_map.joblib
├── region_polygons.pkl
│
└── assets/
    └── screenshots/
```

---

## 📄 File Description

| File                         | Description                                                        |
| ---------------------------- | ------------------------------------------------------------------ |
| `generate_dataset.py`        | Generates the combined real + synthetic GLOF dataset               |
| `GLOF_Risk_Prediction.ipynb` | Data cleaning, EDA, model training, evaluation, and explainability |
| `app.py`                     | Streamlit dashboard                                                |
| `glof_dataset.csv`           | Project dataset                                                    |
| `glof_model.joblib`          | Selected trained machine learning model                            |
| `glof_scaler.joblib`         | Feature scaler used by applicable models                           |
| `glof_feature_cols.joblib`   | Expected feature column order                                      |
| `glof_region_map.joblib`     | Region encoding mapping                                            |
| `region_polygons.pkl`        | Geographic boundary polygons used for visualization                |

---

## 🛠️ Tech Stack

**Programming Language**

* Python

**Machine Learning**

* Scikit-learn
* Logistic Regression
* Decision Tree
* Random Forest
* Gradient Boosting

**Data Processing**

* Pandas
* NumPy

**Visualization**

* Matplotlib
* Seaborn
* Plotly

**Explainable AI**

* SHAP

**Dashboard**

* Streamlit

**Model Persistence**

* Joblib

**Development Environment**

* Jupyter Notebook

---

## ⚙️ Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/glof-risk-prediction.git
cd glof-risk-prediction
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Generate the dataset

```bash
python generate_dataset.py
```

### 4. Train the models

Open the notebook:

```bash
jupyter notebook GLOF_Risk_Prediction.ipynb
```

Run the notebook to perform preprocessing, model comparison, evaluation, and model saving.

### 5. Launch the dashboard

```bash
streamlit run app.py
```

The dashboard will then be available locally in your browser.

---

## 🚀 Future Work

The project can be extended into a more comprehensive GLOF monitoring and risk-assessment platform by:

* Integrating **Sentinel satellite imagery** or Google Earth Engine.
* Replacing the illustrative growth estimate with actual satellite-based lake-area change detection.
* Incorporating real-time environmental and monitoring data.
* Expanding the real-lake dataset.
* Integrating established glacial-lake hazard inventories.
* Adding time-series analysis for lake growth and environmental changes.
* Incorporating additional glaciological features such as moraine characteristics and lake bathymetry.
* Developing automated monitoring and notification infrastructure.

---

## 🌍 Real-World Context

The project uses documented GLOF-related events to demonstrate the importance of monitoring high-altitude glacial lakes.

Examples referenced during development include:

* **South Lhonak Lake — Sikkim, 2023**
* **Chorabari Lake — Uttarakhand, 2013**
* **Parechu Lake — Himachal Pradesh, 2005**

These examples provide real-world context for exploring the application of machine learning to environmental risk assessment.

---

## 📚 References

Project background and real-lake information were informed by published reports, news coverage, and publicly available information concerning documented GLOF events, including:

* South Lhonak Lake and the October 2023 Sikkim GLOF
* Chorabari Lake and the 2013 Kedarnath disaster
* Parechu Lake outburst, 2005

Additional references and data sources can be added as the project is expanded.

---

## 👩‍💻 Project

**GLOF Risk Prediction — India**

Machine Learning • Environmental Risk Assessment • Explainable AI • Streamlit

> Built as a proof-of-concept project exploring the application of machine learning to glacial lake risk assessment in the Indian Himalaya.
