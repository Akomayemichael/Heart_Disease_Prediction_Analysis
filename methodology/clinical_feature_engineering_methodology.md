# Clinical Feature Engineering & Risk Stratification Methodology

## Project Context
Clinical datasets frequently store patient information using numeric or binary encodings for efficiency. While suitable for modeling, these encodings are not human-interpretable and can lead to misinterpretation in analytical dashboards.

This methodology documents how raw clinical codes were transformed into **human-readable, clinically meaningful features** using Power BI (DAX), following **established medical guidelines**. It also explains the logic behind the **High-Risk Patient Classification**, which supports preventive and diagnostic analysis.

---

## 1. Gender (Sex → Gender)

### Original Encoding
- `0` = Female  
- `1` = Male  

### Transformation
Converted to **Female / Male**

### Clinical Meaning
Biological sex is a major demographic determinant of cardiovascular risk.

### Effect
- Males tend to develop coronary artery disease earlier
- Females often present later with atypical or silent symptoms

### Analytical Purpose
- Improves dashboard readability
- Enables gender-based risk comparison

### Source
American Heart Association (AHA)

---

## 2. Chest Pain Type

### Original Encoding
| Code | Description |
|----|------------|
| 1 | Typical Angina |
| 2 | Atypical Angina |
| 3 | Non-Anginal Pain |
| 4 | Asymptomatic |

### Clinical Meaning
Classifies chest discomfort based on exertional characteristics.

### Effect
- Typical angina strongly indicates coronary artery disease
- Asymptomatic cases may represent silent ischemia

### Analytical Purpose
- Differentiates symptomatic vs silent disease
- Explains why diagnostics often outperform symptoms

### Source
Diamond & Forrester (1979), *New England Journal of Medicine*

---

## 3. Fasting Blood Sugar (FBS_over_120 → Diabetes Status)

### Original Encoding
- `0` = Normal  
- `1` = Elevated (>120 mg/dL)

### Clinical Meaning
Elevated fasting glucose suggests diabetes or prediabetes.

### Effect
- Accelerates atherosclerosis
- Increases likelihood of silent ischemia

### Analytical Purpose
- Identifies metabolic risk contributors
- Explains high-risk asymptomatic patients

### Source
American Diabetes Association (ADA)

---

## 4. Exercise-Induced Angina

### Original Encoding
- `0` = No  
- `1` = Yes  

### Clinical Meaning
Indicates chest pain occurring only during physical exertion.

### Effect
- Strong indicator of coronary artery narrowing
- Reflects oxygen supply-demand mismatch

### Analytical Purpose
- Functional ischemia indicator
- Strong predictor in stress-test analysis

### Source
ACC/AHA Exercise Testing Guidelines

---

## 5. Resting ECG Results (EKG_results)

### Original Encoding
| Code | Meaning |
|----|--------|
| 0 | Normal |
| 1 | ST-T Wave Abnormality |
| 2 | Left Ventricular Hypertrophy |

### Clinical Meaning
Assesses the heart’s electrical activity at rest.

### Effect
- ST-T abnormalities suggest ischemia
- LVH reflects chronic hypertension or structural disease

### Analytical Purpose
- Identifies electrical abnormalities
- Adds diagnostic depth

### Source
American Heart Association ECG Standards

---

## 6. ST Segment Depression (ST_depression)

### Original Encoding
Continuous numeric values (0.0 – 6.2 mm)

### Clinical Meaning
Measures the **depth of ST segment depression** during stress testing.

### Effect
- Greater depression = more severe myocardial ischemia
- ≥1.5–2.0 mm indicates high-risk disease

### Analytical Purpose
- Enables dose–response risk analysis
- One of the strongest quantitative predictors

### Source
ACC/AHA Stress Testing Guidelines

---

## 7. ST Segment Slope (Slope_of_ST)

### Original Encoding
| Code | Description |
|----|------------|
| 1 | Upsloping |
| 2 | Flat |
| 3 | Downsloping |

### Clinical Meaning
Describes the **shape of the ST segment** following depression.

### Effect
- Downsloping ST carries the highest ischemic risk
- Upsloping ST is often benign

### Analytical Purpose
- Qualitative risk refinement
- Complements ST depression magnitude

### Source
ACC/AHA ECG Interpretation Standards

---

## 8. Thallium Stress Test Results

### Original Encoding
| Code | Interpretation |
|----|---------------|
| 3 | Normal |
| 6 | Fixed Defect |
| 7 | Reversible Defect |

### Clinical Meaning
Represents myocardial perfusion during nuclear stress testing.

### Effect
- Fixed defect indicates prior myocardial infarction
- Reversible defect indicates active ischemia (highest risk)

### Analytical Purpose
- High diagnostic authority
- Strong predictor of disease severity and outcomes

### Source
American Society of Nuclear Cardiology (ASNC)

---

## 9. Number of Blocked Vessels (Fluoroscopy)

### Original Encoding
Values: 0–3

### Clinical Meaning
Counts the number of major coronary arteries with significant blockage.

### Effect
- Risk increases sharply with vessel count
- Strong correlation with mortality and intervention need

### Analytical Purpose
- Structural disease severity indicator
- Explains sharp escalation in disease rates

### Source
Coronary Angiography Clinical Standards

---

## 10. Heart Disease Status (Target Variable)

### Original Encoding
- `0` = Absence  
- `1` = Presence  

### Purpose
- Outcome variable for prevalence analysis
- Benchmark for risk stratification

---

## 11. High-Risk Patient Classification (Calculated Feature)

### Objective
Identify patients requiring **preventive attention**, not only those with confirmed disease.

### Risk Scoring Logic
Each patient receives one point for the presence of the following risk factors:

- Age ≥ 55 years  
- Total cholesterol ≥ 240 mg/dL  
- Elevated fasting blood sugar (>120 mg/dL)  
- Exercise-induced angina  
- Maximum heart rate < 120 bpm  
- ST depression ≥ 1.5 mm  
- Two or more blocked coronary vessels  

### Classification Rule
A patient is labeled **High Risk** if:
- Heart disease is confirmed  
**OR**
- At least **two independent risk factors** are present

### Clinical Rationale
Cardiovascular risk is cumulative. Many patients progress to severe disease before diagnosis, making early risk identification essential.

### Analytical Purpose
- Preventive screening
- Risk stratification
- Explains why high-risk prevalence exceeds confirmed disease prevalence

### Supporting Evidence
- Framingham Risk Model Concepts
- American Heart Association Risk Stratification Frameworks

---

## Summary
All feature transformations and classifications are grounded in **peer-reviewed clinical standards**. Converting coded medical variables into human-readable categories ensures interpretability, reduces analytical error, and aligns data analytics with real-world clinical reasoning.

This methodology forms the foundation for responsible healthcare analytics and trustworthy dashboard insights.
