# 🌾 Optimized Fertilizer Quantity Recommendation using Indian Soil Data

## 🧭 Overview
This project presents a machine learning-based solution for recommending optimal quantities of **Urea**, **DAP**, and **MOP** fertilizers using geospatial **soil texture** and **nutrient datasets** of India. The objective is to enhance fertilizer efficiency, promote sustainable agriculture, and assist agronomic decision-making using data-driven approaches.

## 📚 Problem Statement
Fertilizer misapplication—overuse or underuse—can degrade soil quality, reduce crop yield, and impact sustainability. To address this, we propose a system that learns from spatially distributed soil properties to recommend **personalized fertilizer strategies** for different Indian regions. The model inputs include:

- **Soil Texture Type** (categorical)
- **Organic Carbon Density** (float)
- **Average Soil Depth** (float)

## 🗂️ Dataset Description
- **Source**: [National Informatics Centre for Earth Sciences (NICES), ISRO Bhuvan](https://bhuvan-app3.nrsc.gov.in/data/download/index.php?c=p&s=NICES&p=isd&g=TS)
- **Data Format**: Raster `.asc` files for:
  - Soil Texture Types (Sandy, Loamy, Clayey, Clayskeletal)
  - Organic Carbon Density
  - Soil Depth Layers (0–25 cm, 25–50 cm, ..., 150–200 cm)
- **Data Coverage**: Geospatial coverage of soil properties across Indian agro-climatic zones
- **Data Processing**: All raster maps were converted into structured tabular data using `rasterio`, yielding ~400,000 geolocated soil records with numeric and categorical attributes

## 🛠️ Feature Engineering
| Feature                  | Description                                     |
|--------------------------|-------------------------------------------------|
| `SoilTexture`            | Inferred from texture masks (one-hot → label)  |
| `OrganicCarbonDensity`   | Mean carbon concentration from raster          |
| `AvgDepth`               | Mean of all soil depth layers                  |
| `Fertilizer Class Labels`| Generated using domain-based decision rules    |

Fertilizer recommendations were derived from domain knowledge rules and mapped to:
- `Low`, `Medium`, `High` fertilizer requirement classes

## 🤖 Machine Learning Models
The system was trained using two robust classifiers:

- **Random Forest Classifier** (baseline)
- **XGBoost Classifier** (final model)

All models were trained and tested on encoded features using an 80-20 split. Performance metrics were computed using precision, recall, and F1-score.

## ✅ Results
| Fertilizer | Accuracy | F1-Score | Class Balance        |
|------------|----------|----------|-----------------------|
| **Urea**   | 100%     | 1.00     | Balanced (L/M/H)      |
| **DAP**    | 100%     | 1.00     | Medium/High classes   |
| **MOP**    | 100%     | 1.00     | Balanced (L/M/H)      |

## 🌐 Web App Deployment
A user-facing interface was developed using **Gradio** within Google Colab.

### 🧪 Usage Instructions:
1. Open `fertilizer_notebook.ipynb` in Google Colab.
2. Run all cells to load models and launch the Gradio UI.
3. Input:
   - Soil Texture (dropdown)
   - Organic Carbon Density (slider)
   - Average Soil Depth (slider)
4. Output: Fertilizer recommendations for **Urea**, **DAP**, and **MOP**

## 🧾 Repository Structure
```
fertilizer-recommendation/
├── fertilizer_notebook.ipynb
├── models/
│   ├── xgb_urea.pkl
│   ├── xgb_dap.pkl
│   ├── xgb_mop.pkl
│   └── encoders/
│       ├── enc_texture.pkl
│       ├── enc_urea.pkl
│       ├── enc_dap.pkl
│       └── enc_mop.pkl
├── reports/
│   └── fertilizer_report.pdf
└── README.md
```

## 🎯 Future Scope
- Incorporate **dynamic weather parameters** (rainfall, humidity)
- Fine-tune recommendations based on **crop type and growth stage**
- Integrate into a mobile or web-based GIS tool
- Use satellite imagery for **real-time prediction**

## 👨‍💻 Author & Supervision
- **Author**: Piyush Gupta  
  M.L. Student, IIITDM Kurnool  
- **Supervisor**: Dr. Vishesh P. Gaikwad  
  Assistant Professor, CSE Department,SVNIT Surat.

📬 Contact: **gguptapiyush45@gmail.com**

> 📘 For academic/industry collaboration or queries, feel free to reach out.
